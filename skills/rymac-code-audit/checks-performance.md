# Performance & Site-Speed Checklist

Site speed and Core Web Vitals for React/Vite/Tailwind/GSAP sites, Next.js, and static HTML. Each item: **why → how to spot (grep/file signals) → fix → impact rank**. Greps assume ripgrep (`rg`).

## Contents
0. Core Web Vitals targets
1. Render-blocking resources
2. JavaScript bundle size
3. Images
4. Fonts
5. Third-party scripts
6. GSAP / animation
7. Caching & delivery
8. Network / request waterfall
9. CSS
10. React-specific
11. Next.js-specific
12. Build-config red flags
13. Measurement tools
14. Grep cheat-sheet

---

## 0. Core Web Vitals — the targets everything maps to

Measured at the **75th percentile** of real users. A metric passes only if ≥75% of page views are "good."

| Metric | Good | Needs work | Poor | Measures |
|---|---|---|---|---|
| **LCP** (Largest Contentful Paint) | **≤ 2.5 s** | ≤ 4.0 s | > 4.0 s | when the biggest above-the-fold element paints |
| **INP** (Interaction to Next Paint) | **≤ 200 ms** | ≤ 500 ms | > 500 ms | worst-case latency across **all** interactions |
| **CLS** (Cumulative Layout Shift) | **≤ 0.1** | ≤ 0.25 | > 0.25 | unexpected layout movement |

**INP officially replaced FID in March 2024** — it measures every click/tap/keypress end-to-end, so it is far stricter. Any audit still citing FID is outdated. Diagnostics: **TTFB** (< 800 ms), **FCP**, **TBT** (< 200 ms, lab proxy for INP).

What hurts each:
- **LCP** ← slow TTFB, render-blocking CSS/JS, unoptimized/huge hero image, lazy-loaded LCP image, late webfonts.
- **INP** ← long main-thread tasks, heavy handlers, third-party scripts, large hydration, un-debounced handlers, big re-renders.
- **CLS** ← images/video/iframes without dimensions, injected banners, webfont swap (FOUT), late-loaded content.

---

## 1. Render-blocking resources `[HIGH]`
- **Why:** CSS in `<head>` blocks first paint; synchronous `<script>` blocks the parser. Directly delays FCP/LCP.
- **Spot:** `<script src=` in `<head>` **without** `defer`/`async`; multiple blocking `<link rel="stylesheet">`; CSS `@import url(...)` (serial chains).
- **Fix:** `defer` (ordered) / `async` (independent) on scripts; inline critical CSS, lazy-load the rest; replace `@import` chains with bundler imports.

## 2. JavaScript bundle size `[HIGH]`
- **Why:** JS is the most expensive byte-for-byte (download + parse + compile + execute). Drives INP/TBT, delays LCP. Keep initial JS well under ~300 KB gzipped.
- **Spot:**
  - No bundle analysis: `rollup-plugin-visualizer` (Vite) / `@next/bundle-analyzer` absent = never measured.
  - **Full-library imports** (biggest quick win): `import _ from 'lodash'` (use `lodash/debounce` or native); `import moment from 'moment'` (use `date-fns`/`dayjs`/`Intl`); `import * as Icons`; wholesale `@mui/material`, `antd`, `three`, `chart.js`.
  - No code splitting: absence of `import(`, `React.lazy`, `next/dynamic`.
  - Duplicate deps: `npm ls <pkg>` shows multiple versions.
- **Fix:** Add a visualizer; split by route; dynamic-`import()` heavy widgets on interaction/viewport; replace heavy libs; ensure tree-shaking (ESM, `sideEffects:false`).

## 3. Images `[HIGH]` (usually the LCP element)
- **Why:** Largest bytes + #1 CLS cause when unsized.
- **Spot:**
  - Missing dimensions → CLS: `<img` without `width=`/`height=` (or CSS `aspect-ratio`); same for `<video>`/`<iframe>`.
  - Legacy formats: `.jpg`/`.png` in `<img src>`/CSS/`/public` — flag any image > ~200 KB, especially heroes. AVIF ~50% smaller than JPEG; WebP ~25–35%.
  - No responsive `srcset`/`sizes`.
  - **LCP image lazy-loaded or de-prioritized**: hero `loading="lazy"` or missing `fetchpriority="high"`.
  - Nothing lazy below the fold.
  - Next.js: raw `<img>` instead of `next/image`; `unoptimized`; missing `priority` on the hero; missing `sizes` on `fill`.
- **Fix:** Hero/LCP → `fetchpriority="high"`, not lazy, optionally `<link rel="preload" as="image">`. Serve AVIF→WebP→JPEG (`<picture>` / `next/image`). Always set width/height. `loading="lazy"` below the fold. `srcset`+`sizes` for responsive. Next.js `next/image` with `priority` on the LCP image.

## 4. Fonts `[MED]`
- **Why:** Webfonts block text paint (FOIT) or shift layout on swap (FOUT → CLS); Google Fonts adds a third-party connection on the critical path.
- **Spot:** `@font-face` missing `font-display: swap`; `fonts.googleapis.com` `<link>`/`@import`; no `<link rel="preload" as="font" crossorigin>`; many weights/styles; no subsetting; Next.js not using `next/font`.
- **Fix:** Self-host (or `next/font`), `font-display: swap`, preload the one critical font (`crossorigin`), subset, and set a metric-matched fallback (`size-adjust`) to minimize swap shift.

## 5. Third-party scripts `[HIGH]` (top INP killer)
- **Why:** Analytics, tag managers, chat, embeds run on the main thread — the leading cause of poor INP.
- **Spot:** `googletagmanager.com`, `google-analytics`, `gtag(`, `connect.facebook.net`, `hotjar`, `clarity.ms`, `intercom`, `drift`, `segment`, `mixpanel`, YouTube/Vimeo `<iframe>`, Calendly/Typeform embeds; third-party `<script>` without `async`/`defer`; heavy embeds loaded on page load; duplicate analytics.
- **Fix:** `async`/`defer`; load non-essential on idle (`requestIdleCallback`). **Facades** for heavy embeds (poster/"Load chat" button → real widget on click, e.g. `lite-youtube-embed`). Consider **Partytown** (run analytics in a web worker). Next.js `next/script` with `strategy="lazyOnload"`/`"afterInteractive"`. Delete unused tags.

## 6. GSAP / animation `[MED]` (CLS + INP + jank)
- **Why:** Animating layout properties forces reflow every frame; heavy scroll handlers inflate INP/CLS. Marketing sites lean on this.
- **Spot:**
  - Non-composited tweens: `gsap.to/from/fromTo` or `@keyframes` animating `top`/`left`/`width`/`height`/`margin`. Prefer `transform` (`x`/`y`/`scale`/`rotate`) + `opacity`.
  - **Layout thrashing:** `offsetWidth`/`getBoundingClientRect`/`scrollHeight` reads interleaved with style writes inside loops/handlers.
  - `will-change` on many/large elements or left on permanently.
  - Many `ScrollTrigger` instances, `scrub` without throttle, heavy `onUpdate`.
  - Scroll/resize/mousemove handlers without throttle/`{ passive: true }`.
  - Missing `prefers-reduced-motion` support.
- **Fix:** Animate only `transform`/`opacity`; batch reads; use GSAP's RAF (don't create competing loops); throttle `onUpdate`; `{ passive: true }`; apply `will-change` sparingly and remove on complete; wrap in `gsap.matchMedia()` with a `(prefers-reduced-motion: reduce)` branch. Reserve space for animated elements (CLS).

## 7. Caching & delivery `[MED/HIGH]` (repeat visits + TTFB)
- **Spot (headers + host config):** hashed assets served without `Cache-Control: public, max-age=31536000, immutable` (check `netlify.toml`/`vercel.json`/`_headers`/nginx/CDN); no Brotli/gzip (`Content-Encoding`); HTML with a too-long cache; no CDN; HTTP/1.1 only.
- **Fix:** Immutable long cache for hashed assets, short/revalidated for HTML, Brotli+gzip, CDN, HTTP/2 or HTTP/3. On Vercel/Netlify most is default — verify it wasn't overridden.

## 8. Network / request waterfall `[MED]`
- **Spot:** no `preconnect`/`dns-prefetch` to required origins; no `preload` for the hero image / key font; long request chains (font←CSS←CSS; JS→config→data); many small unbundled assets; un-preconnected image CDN.
- **Fix:** `preconnect` critical cross-origins, `preload` the LCP image + primary font, flatten chains. Don't over-preload (competes with the LCP resource).

## 9. CSS `[MED]`
- **Spot:**
  - **Tailwind purge misconfig:** v3 `content: []` empty/too narrow/too broad. In v4 (Vite plugin, module-graph scan) **runtime-built class strings** (`` `text-${color}-500` ``) aren't detected — grep for dynamic class construction; safelist or avoid.
  - Large hand-written CSS, unused legacy stylesheets, whole UI-kit CSS barely used.
  - `@import` chains; big unused `@keyframes`.
- **Fix:** Correct `content` globs (v3) / rely on the Vite plugin (v4); avoid runtime class strings; remove dead stylesheets; DevTools Coverage to quantify unused CSS.

## 10. React-specific `[MED]`
- **Spot:** `useEffect` data waterfalls (one fetch triggers the next); unstable props to memoized children (inline `{}`/`[]`/`() =>`, unmemoized context values); expensive render computations without `useMemo`; big lists without virtualization; large client components importing heavy libs on every page; un-debounced high-frequency handlers. (React 19 + React Compiler may auto-memoize — check before recommending manual memo.)
- **Fix:** Parallelize/collocate fetching (loader/RSC), `useMemo`/`useCallback` for memoized-child props, `React.memo` on hot components, virtualize long lists, lazy-load heavy components, debounce input handlers, yield long tasks (`scheduler.yield()`).

## 11. Next.js-specific `[MED/HIGH]`
- **Spot:** `"use client"` on components that don't need interactivity (drags the subtree to the client — push it to leaves); client-side `useEffect`+`fetch` where a Server Component would do; not using `next/image`/`next/font`/`next/script`; `force-dynamic`/`cookies()`/`no-store` on pages that could be static/ISR (slow TTFB); large `getServerSideProps`; missing `loading.js`/Suspense streaming.
- **Fix:** Default to Server Components; isolate interactivity in small client components; use `next/image`/`next/font`/`next/script`; make marketing pages static or ISR (`export const revalidate`); stream slow data; SSR only when truly per-request.

## 12. Build-config red flags `[MED]`
- **Spot:** prod source maps (`build.sourcemap: true` / `productionBrowserSourceMaps: true`); dev build shipped (`NODE_ENV` not production, `build.minify: false`); `console.log`/`debugger` in the prod bundle; large uncompressed assets in `/public`; missing `sideEffects` defeating tree-shaking; deploy serving a dev server instead of `dist`/`.next`.
- **Fix:** Disable prod source maps (or restrict to error-tracker upload), ensure production + minification, strip console/debugger (`esbuild.drop`/Terser `drop_console`), pre-compress, verify tree-shaking.

## 13. Measurement tools
- **Lighthouse** (`npx lighthouse <url>`): lab, mobile throttled — good for CI. Lab TBT ≠ field INP.
- **PageSpeed Insights** (pagespeed.web.dev): shows **field** CrUX (real 75th-percentile CWV) + lab. Field is what Google ranks on — best single "are we passing" check.
- **Chrome DevTools:** Performance (long tasks, layout shifts, INP), Network (waterfall, sizes, headers/compression), Coverage (unused CSS/JS), Web Vitals overlay.
- **WebPageTest:** filmstrip, waterfall, TTFB breakdown, multi-location.
- **Bundle analyzers:** `rollup-plugin-visualizer` (Vite), `@next/bundle-analyzer` (Next).
- All run fine on Windows/PowerShell. Always test with **mobile throttling** — a fast dev machine masks mobile problems.

## 14. Grep cheat-sheet
```
# Render-blocking / third-party
<script src=            (in <head>, no defer/async)
@import url(
googletagmanager|gtag(|google-analytics|connect.facebook|hotjar|clarity|intercom|drift|segment|mixpanel
# Heavy JS imports
import .* from 'lodash'      (not lodash/x)
import .* from 'moment'
import \* as
React.lazy|next/dynamic|import\(     (absence = no code splitting)
rollup-plugin-visualizer|@next/bundle-analyzer   (absence = never measured)
# Images / CLS
<img (no width=/height=)
\.(jpg|jpeg|png)   (no <picture>/AVIF/WebP; check file sizes)
loading="lazy" on hero  |  missing fetchpriority="high"
# Fonts
fonts.googleapis.com
@font-face (no font-display)
next/font   (absence in Next projects)
# GSAP / animation
gsap.*(to|from|fromTo).*(top|left|width|height|margin)
offsetWidth|getBoundingClientRect  (inside loops/handlers)
will-change
prefers-reduced-motion   (absence = no reduced-motion support)
# React / Next
"use client"   (over-broad)
useEffect(.*fetch    (client-side/waterfall fetching)
force-dynamic|no-store   (SSR where static would do)
# Build
sourcemap: true|productionBrowserSourceMaps
minify: false
console\.log|debugger   (in shipped bundle)
# Tailwind
content: \[\]   or  `text-${...}`   (dynamic class construction)
```

**Sources:** [Core Web Vitals & INP replacing FID — Google Search Central](https://developers.google.com/search/docs/appearance/core-web-vitals) · [How to optimize INP — web.dev](https://web.dev/explore/how-to-optimize-inp) · [Fetch Priority — web.dev](https://web.dev/articles/fetch-priority) · [Reduce third-party impact / Partytown — DebugBear](https://www.debugbear.com/blog/reduce-the-impact-of-third-party-code) · [Web Almanac 2025 Performance — HTTP Archive](https://almanac.httparchive.org/en/2025/performance)
