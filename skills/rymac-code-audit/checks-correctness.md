# Correctness & Future-Error Checklist

Bugs now and things likely to break later, for React/Vite/Tailwind/GSAP sites, Next.js, and static HTML/JS/TS. Each item: **why it's a risk → how to spot it (grep signals) → fix**, ranked **HIGH / MED / LOW**. Greps assume ripgrep (`rg`), `-i` case-insensitive, `-n` line numbers.

## Contents
1. JavaScript / TypeScript correctness
2. React pitfalls
3. GSAP / animation cleanup
4. TypeScript quality
5. Error handling & resilience
6. Dead / risky code
7. Environment & config
8. Dependencies
9. Accessibility bugs that are also correctness issues
10. HTML / CSS correctness
11. Browser compatibility & future-proofing
12. Build, lint & test hygiene
13. Security basics
14. Data / state / performance correctness
15. Quick automated sweep

---

## 1. JavaScript / TypeScript Correctness

### 1.1 Floating / unhandled promises `[HIGH]`
- **Why:** An uncaught rejection becomes `unhandledRejection` — can crash Node, silently drops errors and leaves state half-updated in the browser.
- **Spot:** `rg -n "\.then\(" ` with no `.catch`; async calls used as bare statements (`rg -n "^\s*(fetch|axios|api|supabase|db)\."`); async funcs called without `await`. ESLint `@typescript-eslint/no-floating-promises`.
- **Fix:** `await` inside try/catch, attach `.catch()`, or `void promise` when fire-and-forget is intentional.

### 1.2 Missing `await` `[HIGH]`
- **Why:** Function returns a pending promise; code reads `undefined`/stale data, ordering breaks, errors escape the surrounding try/catch.
- **Spot:** `if (fetchX())` (a promise is always truthy); `.json()` not preceded by `await`. ESLint `require-await`.
- **Fix:** Add `await`; make the enclosing function `async`.

### 1.3 Async work in `.forEach` / non-awaited loops `[MED]`
- **Why:** `array.forEach(async …)` does not wait; the loop finishes before async work completes and errors are swallowed.
- **Spot:** `rg -n "forEach\(async"`; `rg -n "\.map\(async"` where the promises aren't `Promise.all`-ed.
- **Fix:** `for…of` with `await`, or `await Promise.all(arr.map(async …))`.

### 1.4 Loose equality `== / !=` `[MED]`
- **Why:** Coercion surprises (`0 == ''`, `[] == false`). Latent, surfaces on edge inputs.
- **Spot:** `rg -n "[^=!<>]==[^=]"` and `rg -n "!=[^=]"`. ESLint `eqeqeq`.
- **Fix:** `===`/`!==`. Allow `x == null` only via `eqeqeq: ["error","always",{null:"ignore"}]`.

### 1.5 Unguarded null/undefined access `[HIGH]`
- **Why:** `Cannot read properties of undefined` is the most common runtime crash. API data, `querySelector`, refs, `.find()` results are all nullable.
- **Spot:** `rg -n "\.find\("` then property access; `querySelector` without a null check; deep chains `a.b.c.d`; `JSON.parse(` without try/catch; destructuring possibly-undefined props.
- **Fix:** Optional chaining `a?.b?.c`, `?? fallback`, early-return guards. TS `strictNullChecks`.

### 1.6 Optional-chaining gaps `[MED]`
- **Why:** `a?.b.c` guards only `b`; `.c` still throws. Precedence traps mixing `?.` with `??`/arithmetic.
- **Spot:** `rg -n "\?\.\w+\.\w+"` (chain that stops guarding).
- **Fix:** Guard the whole chain `a?.b?.c`; parenthesize mixed `??`/`||`/math.

### 1.7 Off-by-one / array bounds `[MED]`
- **Spot:** `rg -n "<= .*\.length"`; `rg -n "\[\s*\w+\s*-\s*1\s*\]"`; `rg -n "\[i\+1\]"`.
- **Fix:** `< length`, guard boundary indices, prefer `.at(-1)` for the last element.

### 1.8 Empty / swallowing catch blocks `[HIGH]`
- **Why:** `catch(e){}` hides real failures — silent data loss, undebuggable.
- **Spot:** `rg -n "catch\s*\([^)]*\)\s*\{\s*\}"`; `.catch(() => {})`; comment-only catches.
- **Fix:** Log with context, surface an error state, or rethrow. Never leave empty.

### 1.9 Uncaught exceptions in callbacks `[MED]`
- **Why:** Throws inside `addEventListener`/`setTimeout`/`.then` bypass surrounding try/catch and React error boundaries.
- **Spot:** Risky ops (`JSON.parse`, `.split`, property access) inside those callbacks.
- **Fix:** Wrap callback bodies in try/catch; add global `window.onerror` / `unhandledrejection` reporting.

### 1.10 `parseInt` without radix / number coercion `[LOW]`
- **Spot:** `rg -n "parseInt\([^,)]*\)"`; `Number(`/`+` on unvalidated input.
- **Fix:** `parseInt(x, 10)`; validate `Number.isNaN`.

### 1.11 `var` / function-scope leaks `[LOW]`
- **Spot:** `rg -n "\bvar\s"`. ESLint `no-var`, `prefer-const`.
- **Fix:** `const`/`let`.

### 1.12 Mutating shared/param objects `[MED]`
- **Spot:** `rg -n "\bdelete \w+\."`; `.sort()`/`.reverse()` on props/state (mutate in place).
- **Fix:** Copy before mutating (`[...arr].sort()`); treat inputs as immutable.

---

## 2. React Pitfalls

### 2.1 Incorrect `useEffect` dependency array `[HIGH]`
- **Why:** Missing deps → stale closures / effects that don't re-run; wrong deps → infinite loops. Top source of "works then silently stops updating."
- **Spot:** `rg -n "useEffect\("` and inspect arrays; `}, [])` on effects reading props/state; effects with no array (run every render). ESLint `react-hooks/exhaustive-deps`.
- **Fix:** Include every reactive value, or memoize with `useCallback`/`useMemo`. Don't silence the rule without justification.

### 2.2 Missing effect cleanup → memory leaks `[HIGH]`
- **Why:** Listeners/timers/subscriptions/observers/GSAP contexts added on mount but never removed accumulate across route changes → leaks, duplicate handlers, "setState on unmounted component."
- **Spot:** `rg -n "addEventListener"` without matching `removeEventListener` return; `setInterval|setTimeout` without clear; `IntersectionObserver|ResizeObserver|MutationObserver` without `.disconnect()`; `.subscribe(` without `.unsubscribe()`.
- **Fix:** Return a cleanup fn from `useEffect` (remove/clear/disconnect), using the same callback reference.

### 2.3 Missing / index-as-`key` `[MED]`
- **Why:** Missing keys → reconciliation bugs; index keys reuse wrong elements on reorder/filter (stale inputs, glitchy animations).
- **Spot:** `rg -n "\.map\("` and check for `key=`; `rg -n "key=\{i(ndex)?\}"`.
- **Fix:** Stable unique id. Index acceptable only for static, never-reordered lists.

### 2.4 Direct state mutation `[HIGH]`
- **Why:** Mutating then `setState` skips re-render (same reference) or corrupts state.
- **Spot:** `rg -n "\.push\(|\.splice\(|\.pop\(|\.shift\("` near state; `state.x =`; `.sort()`/`.reverse()` on state.
- **Fix:** New references: `setArr([...arr, item])`, `setObj({...obj, k:v})`, or Immer.

### 2.5 `setState` during render `[HIGH]`
- **Spot:** setter calls not inside a handler/effect (`rg -n "set[A-Z]\w+\("`); `onClick={handleClick()}` (called, not passed).
- **Fix:** Move to handler/effect; pass the reference `onClick={handleClick}`.

### 2.6 Stale closures `[MED]`
- **Spot:** `setInterval`/`setTimeout`/handlers reading state with `[]` deps; `useCallback` with missing deps.
- **Fix:** Functional updates `setX(prev => …)`, `useRef` for latest value, or correct deps.

### 2.7 Conditional / early-return hooks `[HIGH]`
- **Why:** Violates Rules of Hooks → "Rendered fewer hooks than expected," crashes when the condition flips.
- **Spot:** `rg -n "if.*\{[^}]*use[A-Z]"`; hooks after `if (!x) return`; hooks in loops/callbacks. ESLint `react-hooks/rules-of-hooks`.
- **Fix:** Call all hooks unconditionally at top; put the condition inside the hook.

### 2.8 Controlled/uncontrolled input switching `[MED]`
- **Spot:** `value={x}` where `x` starts `undefined`/`null`.
- **Fix:** Initialize to `''`/`false`, or use `defaultValue`; never mix.

### 2.9 Unmemoized deps causing loops/perf `[LOW-MED]`
- **Spot:** inline `{}`/`[]`/`() =>` passed to memoized children or effect deps.
- **Fix:** `useMemo`/`useCallback`; hoist constants out of the component.

### 2.10 Hydration mismatches (Next.js / SSR) `[MED]`
- **Why:** `Date.now()`, `Math.random()`, `window`/`localStorage` in render differ server vs client → "Hydration failed," flashing UI.
- **Spot:** `rg -n "localStorage|sessionStorage|window\.|document\."` in component bodies (not effects); `new Date()`/`Math.random()` in render.
- **Fix:** Read browser-only values in `useEffect`; gate with a `mounted` flag or `next/dynamic` `ssr:false`.

---

## 3. GSAP / Animation Cleanup

### 3.1 Tweens & ScrollTriggers not killed on unmount `[HIGH]`
- **Why:** GSAP tweens/timelines and each `ScrollTrigger` persist globally after unmount → target detached DOM, stack up on re-mount, throw "target not found," leak memory / jank on SPA route changes.
- **Spot:** `rg -n "gsap\.(to|from|fromTo|timeline)"` and `rg -n "ScrollTrigger.create|scrollTrigger:"` with no cleanup; GSAP effects with no return function.
- **Fix:** `useGSAP()` from `@gsap/react` (auto-reverts), or `const ctx = gsap.context(() => {…}, ref); return () => ctx.revert();`.

### 3.2 `gsap.matchMedia()` not reverted `[MED]`
- **Spot:** `rg -n "matchMedia\("` without a stored handle + `.revert()` in cleanup.
- **Fix:** `const mm = gsap.matchMedia(); … return () => mm.revert();`

### 3.3 Animating null refs `[MED]`
- **Spot:** `rg -n "\.current"` used as GSAP targets without a null guard; refs on conditionally rendered elements.
- **Fix:** Guard `if (!ref.current) return;` inside `useGSAP`/`useLayoutEffect`; scope selectors to a container ref.

### 3.4 ScrollTrigger not refreshed after dynamic content `[LOW]`
- **Why:** Positions computed before images/fonts load → triggers fire at wrong scroll positions (also a mobile issue when the URL bar resizes).
- **Fix:** `ScrollTrigger.refresh()` after load, or `invalidateOnRefresh: true`.

---

## 4. TypeScript Quality

### 4.1 Strict mode off `[HIGH]`
- **Spot:** `rg -n "\"strict\"" tsconfig*.json` (missing/`false`); check `strictNullChecks`, `noImplicitAny`.
- **Fix:** `"strict": true` (migrate incrementally, `strictNullChecks` first).

### 4.2 `any` overuse `[MED]`
- **Spot:** `rg -n ":\s*any\b|<any>|as any|any\[\]"`. ESLint `@typescript-eslint/no-explicit-any`.
- **Fix:** `unknown` + narrowing, generics, or real interfaces.

### 4.3 `@ts-ignore` / `eslint-disable` `[MED]`
- **Spot:** `rg -n "@ts-ignore|@ts-nocheck|eslint-disable"`.
- **Fix:** Fix the underlying type; if unavoidable use `@ts-expect-error` + comment.

### 4.4 Non-null assertions `!` / unsafe casts `[MED]`
- **Spot:** `rg -n "\w+!\."` (non-null then access); `rg -n "\bas\s+\w"`; `as unknown as`.
- **Fix:** Runtime guards / narrowing instead of `!`; validate at boundaries.

### 4.5 Untyped API boundaries `[HIGH]`
- **Why:** `.json()` returns `any`; unchecked shape means backend changes crash the UI with no compile signal.
- **Spot:** `rg -n "await .*\.json\(\)"` assigned without a type/validator.
- **Fix:** Validate with zod/valibot at the boundary; handle schema mismatch as an error state.

---

## 5. Error Handling & Resilience

### 5.1 No React error boundaries `[HIGH]`
- **Why:** One render throw unmounts the whole tree → white screen, no recovery.
- **Spot:** `rg -rn "componentDidCatch|getDerivedStateFromError|ErrorBoundary"` absent; no `error.tsx`/`global-error.tsx` in a Next.js `app/`.
- **Fix:** Error boundaries around routes/sections (react-error-boundary / Next.js `error.tsx`) with a reset.

### 5.2 Unhandled fetch/network errors `[HIGH]`
- **Why:** `fetch` does **not** reject on 4xx/5xx — only on network failure. Ignoring `res.ok` treats an error page as data.
- **Spot:** `rg -n "await fetch\("` then check for `if (!res.ok)`; `.json()` called unconditionally; no try/catch.
- **Fix:** Check `res.ok`, branch/throw on failure, handle timeouts (`AbortController`).

### 5.3 Missing loading / error / empty states `[MED]`
- **Spot:** data components with only a success branch; `data.map` with no guards.
- **Fix:** Handle loading, error, empty, and success.

### 5.4 No global error/rejection reporting `[LOW-MED]`
- **Spot:** no `window.addEventListener('error'|'unhandledrejection')` and no error monitor.
- **Fix:** Add global handlers and/or Sentry-style monitoring.

---

## 6. Dead / Risky Code

### 6.1 `console.log` / `debugger` left in `[MED]`
- **Spot:** `rg -n "console\.(log|debug|warn|info)"`; `rg -n "\bdebugger\b"`. ESLint `no-console`, `no-debugger`.
- **Fix:** Remove or route through a logger stripped in production.

### 6.2 Unused variables / imports / files `[LOW-MED]`
- **Spot:** ESLint `no-unused-vars`; `npx knip` / `ts-prune` (dead exports/files); `npx depcheck` (unused deps).
- **Fix:** Delete; prefix intentionally-unused with `_`.

### 6.3 Commented-out code `[LOW]`
- **Spot:** `rg -n "^\s*//\s*(const|let|function|return|import|if|<)"`.
- **Fix:** Delete — git preserves history.

### 6.4 TODO / FIXME / HACK markers `[LOW]`
- **Spot:** `rg -n "TODO|FIXME|HACK|XXX|@deprecated"`.
- **Fix:** Triage into issues; resolve HACK/FIXME near release.

### 6.5 Magic numbers / strings `[LOW]`
- **Spot:** repeated literals in logic; `setTimeout(fn, 3600000)`.
- **Fix:** Named constants with units (`ONE_DAY_MS`).

---

## 7. Environment & Config

### 7.1 Hardcoded secrets / API keys in client code `[HIGH — also security]`
- **Why:** Anything in front-end JS ships to the browser and is public. Only `VITE_`/`NEXT_PUBLIC_` vars are meant to be public; a *secret* under those prefixes is exposed in the bundle.
- **Spot:** `rg -ni "api[_-]?key|secret|token|password|bearer|private[_-]?key" --glob '!*.md'`; `rg -n "sk-[A-Za-z0-9]|AIza[0-9A-Za-z_-]{35}|AKIA[0-9A-Z]{16}"`; secrets under `NEXT_PUBLIC_`/`VITE_`; grep the built bundle `rg -n "sk-|secret" dist/`.
- **Fix:** Move secrets server-side; rotate any exposed key immediately; client holds only truly-public keys.

### 7.2 Committed `.env` files `[HIGH]`
- **Spot:** `git ls-files | rg "\.env"` (should be empty except `.env.example`); `.gitignore` contains `.env*`.
- **Fix:** Gitignore, purge history (`git filter-repo`), rotate secrets, commit `.env.example` with blanks.

### 7.3 Missing env-var fallbacks / validation `[MED]`
- **Why:** `process.env.X` undefined → `https://undefined/api`, silent misconfig.
- **Spot:** `rg -n "process\.env\.|import\.meta\.env\."` without a default or startup check.
- **Fix:** Validate required env at startup (zod); safe fallbacks only.

### 7.4 Hardcoded localhost / URLs / IPs `[MED]`
- **Spot:** `rg -n "localhost|127\.0\.0\.1|http://"` in `src/`.
- **Fix:** Environment-based config; enforce `https`.

### 7.5 Public source maps in prod `[LOW]`
- **Spot:** `*.map` in `dist/`; `build.sourcemap: true`.
- **Fix:** Disable, or upload privately to the error monitor.

---

## 8. Dependencies

### 8.1 Known-vulnerable deps (CVEs) `[HIGH]`
- **Spot:** `npm audit --production`; `npm audit --json | rg "high|critical"`; `osv-scanner`.
- **Fix:** `npm audit fix`, bump direct deps, `overrides` for transitive fixes.

### 8.2 Outdated / deprecated packages & APIs `[MED]`
- **Spot:** `npm outdated`; install-time deprecation warnings; `rg -n "componentWillMount|componentWillReceiveProps|ReactDOM.render\(|findDOMNode"`; `substr`, `document.write`.
- **Fix:** Upgrade on a schedule; migrate off deprecated APIs; replace unmaintained packages.

### 8.3 Unpinned versions without lockfile `[MED]`
- **Spot:** missing/uncommitted lockfile; `rg -n "\"latest\"|\"\\*\"" package.json`.
- **Fix:** Commit the lockfile; `npm ci` in CI; avoid `latest`/`*`.

### 8.4 Duplicate / conflicting deps `[LOW-MED]`
- **Why:** Two copies of React/GSAP → "Invalid hook call," doubled bundle.
- **Spot:** `npm ls react` (multiple versions); peer-dep warnings; `npx dedupe`.
- **Fix:** Deduplicate/hoist, align versions.

---

## 9. Accessibility Bugs That Are Also Correctness Issues

### 9.1 Inputs without labels `[MED]`
- **Spot:** `rg -n "<input|<select|<textarea"` with no `<label htmlFor>`/`aria-label`. jsx-a11y `label-has-associated-control`.
- **Fix:** Associate a label or `aria-label`.

### 9.2 Buttons / links without accessible names `[MED]`
- **Spot:** `rg -n "<button[^>]*>\s*<(svg|img|i)"` (icon-only); empty `<a></a>`.
- **Fix:** `aria-label` or visually-hidden text.

### 9.3 Images missing `alt` `[MED]`
- **Spot:** `rg -n "<img"` without `alt=`; Next `<Image` without `alt`.
- **Fix:** Descriptive `alt`, or `alt=""` for decorative.

### 9.4 Invalid interactive nesting `[MED]`
- **Why:** `<a>`/`<button>` nested, `<div>` in `<p>`, `<li>` outside `<ul>` → React hydration errors, broken semantics.
- **Spot:** nested interactive elements; block elements inside `<p>`.
- **Fix:** Correct nesting.

### 9.5 Click handlers on non-interactive elements `[LOW-MED]`
- **Spot:** `rg -n "<div[^>]*onClick"`. jsx-a11y `no-static-element-interactions`.
- **Fix:** Use `<button>`, or add `role`, `tabIndex`, key handlers.

---

## 10. HTML / CSS Correctness

### 10.1 Duplicate IDs `[MED]`
- **Spot:** `rg -on "id=\"[^\"]+\"" | sort | uniq -d`; W3C Nu validator.
- **Fix:** Unique IDs; classes for styling.

### 10.2 Broken / placeholder links `[MED]`
- **Spot:** `rg -n "href=\"#\"|href=\"\"|href=\"javascript:"`.
- **Fix:** Real URL, or a `<button>` for actions; `#` only for genuine in-page anchors.

### 10.3 Broken image / asset `src` `[MED]`
- **Spot:** `rg -n "src=\"\"|src=\"#\"|placeholder|example\.com|via.placeholder|lorem"`; verify local paths resolve.
- **Fix:** Correct paths; add width/height; `onError` fallback for dynamic.

### 10.4 Unclosed / malformed tags `[LOW-MED]`
- **Spot:** W3C validator; framework build errors.
- **Fix:** Validate; self-close void elements in JSX.

### 10.5 `target="_blank"` without `rel="noopener"` `[MED — security]`
- **Why:** Opened page can hijack the tab via `window.opener` (reverse tabnabbing).
- **Spot:** `rg -n "target=\"_blank\""` without `rel=` containing `noopener`.
- **Fix:** Add `rel="noopener noreferrer"`.

### 10.6 z-index chaos / hardcoded px layout `[LOW]`
- **Spot:** `rg -n "z-index:\s*\d{4,}"`; `rg -n "width:\s*\d{3,}px|height:\s*\d{3,}px"`; Tailwind `w-[1200px]`. (See mobile checklist for the responsive angle.)
- **Fix:** z-index scale/tokens; relative units, `max-width`, `clamp()`.

### 10.7 `!important` overuse `[LOW]`
- **Spot:** `rg -n "!important"`.
- **Fix:** Fix specificity/source order instead.

---

## 11. Browser Compatibility & Future-Proofing

### 11.1 Deprecated / removed web APIs `[MED]`
- **Spot:** `rg -n "document\.write|escape\(|unescape\(|\.substr\(|window\.event|navigator\.userAgent"`; synchronous XHR.
- **Fix:** Modern replacements (`substring`/`slice`, `textContent`, feature detection).

### 11.2 Vendor-prefix-only CSS `[LOW]`
- **Spot:** `rg -n "-webkit-|-moz-|-ms-"` without the standard property alongside; no autoprefixer.
- **Fix:** Autoprefixer/PostCSS; a `browserslist`.

### 11.3 Missing `browserslist` / polyfill strategy `[LOW]`
- **Spot:** no `browserslist` in `package.json`/`.browserslistrc`.
- **Fix:** Define supported browsers explicitly.

---

## 12. Build, Lint & Test Hygiene

### 12.1 No linter / not enforced `[HIGH]`
- **Why:** Most of §1–2 is auto-detectable by ESLint; without it, they ship.
- **Spot:** no `.eslintrc*`/`eslint.config.*`; missing `react-hooks` + `jsx-a11y` + `@typescript-eslint`; no `lint` script; CI doesn't run it.
- **Fix:** Add ESLint with those plugins; run in CI as a blocking check.

### 12.2 No type-check in CI `[HIGH]`
- **Why:** Vite/Next often don't type-check — TS errors ship unless `tsc --noEmit` runs.
- **Spot:** no `typecheck` script; `next build` with `typescript.ignoreBuildErrors: true`.
- **Fix:** Add `tsc --noEmit` to CI; never `ignoreBuildErrors`/`eslint.ignoreDuringBuilds`.

### 12.3 Build errors suppressed `[HIGH]`
- **Spot:** `rg -n "ignoreBuildErrors|ignoreDuringBuilds|--no-verify|CI=false"`; file-top `eslint-disable`.
- **Fix:** Remove suppressions; fix the errors.

### 12.4 No formatter `[LOW]`
- **Spot:** no Prettier/Biome config.
- **Fix:** Prettier/Biome + format-on-save + CI check.

### 12.5 Absent / skipped tests, no CI `[MED]`
- **Spot:** no test runner; `rg -n "\.(skip|only)\(|xit\(|xdescribe\("`; no `.github/workflows`.
- **Fix:** Smoke tests for critical paths; fail CI on `.only`; run tests + lint + typecheck in CI.

---

## 13. Security Basics (light touch — a deep security pass is separate)

### 13.1 `dangerouslySetInnerHTML` / `innerHTML` with untrusted data → XSS `[HIGH]`
- **Spot:** `rg -n "dangerouslySetInnerHTML|\.innerHTML\s*=|insertAdjacentHTML|document\.write"`.
- **Fix:** Avoid; sanitize with DOMPurify; render as text.

### 13.2 `eval` / `new Function` / dynamic code `[HIGH]`
- **Spot:** `rg -n "\beval\(|new Function\(|setTimeout\(\s*[\"']"` (string-arg timers).
- **Fix:** Remove; use real functions/parsers.

### 13.3 Sensitive data in `localStorage` / logs `[MED]`
- **Spot:** `rg -n "localStorage.setItem\(.*(token|jwt|secret|password)"`; `console.log` of auth/user objects.
- **Fix:** HttpOnly cookies for tokens; never log secrets/PII.

---

## 14. Data / State / Performance Correctness

### 14.1 Fetch race conditions `[HIGH]`
- **Why:** Rapid param changes fire overlapping requests; a slow earlier response resolves last and overwrites correct data.
- **Spot:** `useEffect` fetching on a changing dep with no ignore flag / `AbortController`.
- **Fix:** `AbortController` in cleanup, an `ignore` guard, or React Query/SWR.

### 14.2 Missing debounce / throttle `[MED]`
- **Spot:** `rg -n "addEventListener\(\s*[\"'](scroll|resize|mousemove|input)"`; `onChange` firing network calls with no debounce.
- **Fix:** Debounce/throttle, `requestAnimationFrame` for scroll, `passive:true`.

### 14.3 Unbounded lists / no virtualization `[MED]`
- **Spot:** `.map` over large/streamed data with no pagination/virtualization; arrays only `.push`-ed.
- **Fix:** Virtualize (react-window/virtual), paginate, cap buffers.

### 14.4 Timers/RAF not cancelled `[MED]`
- **Spot:** `rg -n "requestAnimationFrame"` without `cancelAnimationFrame`; `setInterval` without clear.
- **Fix:** Cancel in cleanup.

### 14.5 Derived state duplicated in state `[LOW-MED]`
- **Spot:** `useState` initialized from props then never updated.
- **Fix:** Compute during render (memoize if costly); one source of truth.

---

## 15. Quick Automated Sweep (run first)

```bash
# Lint / types / audit
npx eslint . --max-warnings=0
npx tsc --noEmit
npm audit --production
npx knip            # dead files/exports/deps
npx depcheck        # unused deps

# Fast greps (ripgrep)
rg -n "console\.(log|debug)|\bdebugger\b"                     # left-in debug
rg -n "catch\s*\([^)]*\)\s*\{\s*\}"                            # empty catch
rg -ni "api[_-]?key|secret|password|token|sk-|AKIA"           # secrets
rg -n "localhost|127\.0\.0\.1|http://"                        # hardcoded/insecure URLs
rg -n "TODO|FIXME|HACK|XXX"                                    # markers
rg -n "as any|:\s*any\b|@ts-ignore|\w+!\."                     # TS escape hatches
rg -n "dangerouslySetInnerHTML|\.innerHTML|eval\("            # XSS/eval
rg -n "target=\"_blank\""                                      # check rel=noopener
rg -n "addEventListener"                                       # verify cleanup exists
rg -n "gsap\.(to|from|timeline)|ScrollTrigger"                # verify kill/revert
rg -n "\.map\(" -A1 | rg -v "key="                            # list items missing key
rg -n "<img" | rg -v "alt="                                   # images missing alt
git ls-files | rg "\.env$"                                    # committed env files
```

**Triage order:** Fix all **HIGH** (crashes, leaks, exposed secrets, no error boundary, unhandled fetch, floating promises, hook violations, GSAP leaks, CVEs, suppressed build/type errors, XSS/eval, race conditions) before **MED**, then **LOW** (hygiene, style). Static tools (ESLint `react-hooks`/`jsx-a11y`/`@typescript-eslint`, `tsc --noEmit`, `npm audit`, `knip`/`depcheck`) cover most HIGH/MED automatically; use grep for what they miss (GSAP cleanup, empty catches, hardcoded URLs/secrets, magic numbers).
