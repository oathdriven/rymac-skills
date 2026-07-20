---
name: rymac-code-audit
description: Runs a thorough, multi-lens code audit of a web build — finding (1) bugs and future-error risks, (2) performance / site-speed / Core Web Vitals problems, (3) technical-SEO and crawlability issues that stop search engines indexing the site, and (4) responsive / mobile-compatibility problems that break layouts on phones. Produces a severity-ranked report with file:line locations and concrete fixes. Use when the user asks to "audit this build", "audit the site", "run a code audit", "check my site for errors", "find bugs before launch", "why is my site slow", "improve site speed", "why isn't my site getting indexed", "SEO audit", "why does my site break on mobile", "mobile / responsive audit", or "check mobile compatibility". Works on React/Vite, Next.js, and static HTML sites. Make sure to use this skill whenever the user wants a build reviewed for errors, speed, search-engine visibility, or mobile responsiveness.
argument-hint: [path to build (default: cwd)] [lenses: all|correctness|performance|seo|mobile]
---

# Code Audit

Audit a web build across four independent lenses and return one severity-ranked report. This is a **read-only** review — never edit the audited code; report findings and fixes so the user decides what to change.

The full, grep-oriented checklists live in supporting files — have each lens read its own file, then work through it against the target codebase:

- `${CLAUDE_SKILL_DIR}/checks-correctness.md` — bugs now + future-error risks (JS/TS, React, GSAP cleanup, error handling, deps, security basics, build hygiene)
- `${CLAUDE_SKILL_DIR}/checks-performance.md` — site speed, Core Web Vitals (LCP / INP / CLS), bundle, images, fonts, third-party scripts, caching
- `${CLAUDE_SKILL_DIR}/checks-seo.md` — crawlability + technical SEO (rendering/CSR, robots/noindex, sitemaps, canonical, metadata, internal linking, soft 404s)
- `${CLAUDE_SKILL_DIR}/checks-mobile.md` — responsive / mobile compatibility (viewport, horizontal overflow, tap targets, hover-only UI, 100vh, touch keyboards, breakpoints)

## The four lenses

| Lens | Answers | Primary signals |
|------|---------|-----------------|
| **Correctness** | "What is broken now or will break later?" | ESLint/tsc/`npm audit` + greps for unhandled promises, effect leaks, empty catches, hardcoded secrets |
| **Performance** | "What weighs the site down?" | Bundle analyzer + Lighthouse + greps for full-lib imports, unsized images, render-blocking/third-party scripts |
| **SEO / crawlability** | "What stops crawlers getting through?" | Raw-HTML inspection + greps for CSR-only content, noindex, HashRouter, JS-only nav, canonical/meta issues |
| **Responsive / mobile** | "What breaks on a phone?" | Greps for missing viewport, fixed px widths, `w-[…px]`, hover-only nav, `100vh`, sub-16px inputs, tiny tap targets |

## Workflow (copy this checklist and tick it off)

- [ ] **1. Scope the build** — resolve the target path from `$ARGUMENTS` (default: cwd) and detect the stack before auditing.
- [ ] **2. Run the sweep** — one pass per applicable lens (fan out subagents for a full audit).
- [ ] **3. Verify** — confirm every Critical/High by reading the real code; drop grep false positives.
- [ ] **4. Runtime checks (optional)** — if a URL or served build is available, run the curl/view-source/device-emulation checks the static pass can't answer.
- [ ] **5. Report** — one severity-ranked document with a scorecard, file:line, why, and fix.

### Step 1 — Scope the build

Detect what you are auditing so you only run relevant checks and can read config accurately:

- **Stack:** `package.json` (deps + scripts), and presence of `vite.config.*` (Vite SPA), `next.config.*` / `app/` / `pages/` (Next.js), or plain `index.html` with no build (static). No `package.json` → treat as static HTML/CSS/JS.
- **Key files to locate up front:** entry HTML (`index.html`, `app/layout.*`), router setup, `public/` (robots.txt, sitemap, assets), deploy config (`vercel.json`, `netlify.toml`, `_headers`, `.htaccess`, `next.config`), `tsconfig.json`, lint config, `tailwind.config.*`, lockfile.
- **Applicable lenses:** default `all`. If `$ARGUMENTS` names a lens, run only that. SEO/crawlability matters most for public-facing marketing sites and least for internal dashboards — say so if you down-weight it. Mobile applies to almost every site.

### Step 2 — Run the sweep

For a **full audit (default), fan out one subagent per lens, in parallel** (send the Agent calls in a single message). Give each subagent: the absolute path to its `checks-*.md` file, the target directory, and this instruction —

> Work through every item in the checklist file against the code under `<target>`. Use Grep/Glob/Read (and the listed CLI tools where available). For each real issue return: **severity** (Critical/High/Medium/Low), **file:line**, a one-line **issue**, a one-line **why it matters**, and the **fix**. Only report issues you actually located in this codebase — no generic advice. Return the findings list as your final message.

For a **single-lens or quick audit**, run that one checklist inline yourself instead of spawning an agent.

Run the deterministic tools first where the stack supports them — they find the most with the least guessing (exact commands live in the check files):

- Correctness: `npx eslint . --max-warnings=0`, `npx tsc --noEmit`, `npm audit --production`, `npx knip` / `npx depcheck`
- Performance: `npx lighthouse <url>` (or PageSpeed Insights), bundle analyzer (`rollup-plugin-visualizer` / `@next/bundle-analyzer`), inspect built `dist`/`.next` asset sizes
- SEO: inspect built HTML (`dist/index.html`) for real content vs empty `<div id="root">`, read `public/robots.txt` + sitemap
- Mobile: `npx lighthouse <url> --form-factor=mobile`, inspect `tailwind.config` breakpoints, grep for the fixed-width / overflow signals in the check file

If a tool is missing, note it as a gap ("no linter configured") — that is itself a finding — and fall back to the greps.

### Step 3 — Verify before reporting

Grep hits are leads, not findings. Before a finding reaches the report, **open the file and confirm it is real** in this codebase — a `console.log` behind a `if (dev)` guard, an empty catch that genuinely re-throws elsewhere, a `w-[400px]` that already has a `max-w-full` sibling, or a `noindex` that is correctly env-gated to staging are not bugs. Verify every Critical/High personally; spot-check Medium/Low. Prefer a shorter list of confirmed issues over a long list of maybes — false positives destroy trust in the audit.

### Step 4 — Runtime checks (optional, only if a URL / served build exists)

Some facts can't be read from source. If the user gives a URL or the build is served locally, confirm:

- `curl -I <url>/a-page-that-does-not-exist` → a `200` is a **soft 404** (SPA bug).
- `curl -sL <url> | rg -i "<h1|og:image|canonical|name=.robots"` → is content/meta in the **raw** HTML, or only injected by JS?
- `curl -I <url>` → check for an `X-Robots-Tag: noindex` header and `Cache-Control` / `Content-Encoding` (compression) on assets.
- **Mobile:** view the served site at 375px width (and 320px) in a device emulator / the browser tools — check for horizontal scroll, overlapping fixed elements, unreadable text, and cut-off tap targets. This is the fastest way to catch the "had to go back and fix mobile" class of bug before it ships.

Skip this step (and say so) if there's no running site — the static audit still stands.

### Step 5 — Report

Deliver one document. Lead with the scorecard and the Critical/High items; detail follows. Offer to write it to `audit-report.md` in the target, or to publish it as a shareable Artifact.

## Severity model

| Severity | Means | Examples |
|----------|-------|----------|
| **Critical** | Broken / exposed / invisible in production | Site not crawlable (CSR with no prerender), `noindex` shipped to prod, secret/API key in client bundle, white-screen with no error boundary, layout unusable on mobile (horizontal scroll hides content / nav unreachable) |
| **High** | Real bug, leak, or major regression risk | Unhandled fetch/promise, GSAP/effect not cleaned up (leak), unsized LCP image, full-library import bloating the bundle, soft 404s, missing viewport meta, hover-only navigation with no touch fallback |
| **Medium** | Correctness edge case, notable slowdown, SEO gap, or mobile roughness | `useEffect` deps wrong, missing canonical/meta, un-debounced handler, `any` on an API boundary, sub-16px inputs (iOS zoom), fixed px widths, tap targets under 44px |
| **Low** | Hygiene / polish / future-proofing | `console.log` left in, magic numbers, commented-out code, missing `browserslist`, `100vh` where `100dvh` is safer |

## Report format

```markdown
# Code Audit — <target> (<stack>)  ·  <date>

## Scorecard
| Lens | Critical | High | Medium | Low | Verdict |
|------|:--:|:--:|:--:|:--:|--------|
| Correctness         | 0 | 2 | 4 | 3 | ⚠ fix before launch |
| Performance         | 0 | 1 | 3 | 2 | ⚠ |
| SEO / crawl         | 1 | 1 | 2 | 0 | ✗ crawlers blocked |
| Responsive / mobile | 0 | 2 | 3 | 1 | ⚠ breaks under 400px |

**Top 3 things to fix first:** <the highest-leverage items across all lenses>

## Findings

### 🔴 Critical
- **[SEO] SPA ships empty HTML — content is invisible to crawlers** · `dist/index.html`
  - Why: Googlebot's first wave and all non-JS crawlers (social, AI) see only `<div id="root">`; the site is effectively unindexed.
  - Fix: add a prerender/SSG step (vite-react-ssg / react-snap) or move to SSR.

### 🟠 High
- **[Mobile] Nav is hover-only — unreachable on touch devices** · `src/components/Nav.tsx:31`
  - Why: the dropdown opens on `onMouseEnter`; phones have no hover, so those links can't be opened.
  - Fix: toggle on click/tap (and keyboard focus); test at 375px.
- **[Correctness] Unhandled fetch error** · `src/api/user.ts:42`
  - Why: `fetch` doesn't reject on 4xx/5xx; an error page is parsed as data.
  - Fix: check `res.ok`, wrap in try/catch, add an error state.

### 🟡 Medium  ·  ⚪ Low
(same shape, grouped)
```

## Critical rules

1. **Read-only.** Audit and report; do not modify the audited code unless the user explicitly asks in a separate request.
2. **Verify before you claim.** Every Critical/High must be confirmed against the actual code, with a real `file:line`. No hallucinated locations.
3. **Only findings in *this* codebase.** No generic "you should also…" lists — if it isn't present here, it isn't a finding.
4. **Rank by leverage, not by count.** A short report of real problems beats an exhaustive one padded with noise.
5. **Match the stack.** Down-weight or skip checks that don't apply (e.g. React/GSAP checks on a static HTML site; deep SEO on an internal dashboard) and say why. Mobile applies almost everywhere — don't skip it.

Treat `$ARGUMENTS` as the target path and optional lens filter. Default to auditing the current working directory across all four lenses.
