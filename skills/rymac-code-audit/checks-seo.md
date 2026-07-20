# Technical SEO & Crawlability Checklist

For React/Vite/Tailwind/GSAP SPAs, Next.js (SSR/SSG), and static HTML. Each item: **why (for crawlers) → how to spot (grep signals) → fix → impact**. Greps assume ripgrep (`rg`).

> **The mental model:** Googlebot crawls in two waves. Wave 1 reads the **raw HTML your server returns** — this gets you into the crawl queue and is what fast/AI/social pipelines rely on. Wave 2 renders JS in headless Chromium *later, when resources allow* (content took ~2× longer to index at depth 1, up to ~9× deeper). **Dec 2025 clarification:** pages returning a **non-200 status may skip JS rendering entirely.** So anything that only exists after JS runs is second-class. The whole checklist is essentially: *is the important stuff in the raw HTML, and is nothing blocking the crawler from reaching it?*

## Contents
1. Crawlability blockers
2. Client-side rendering (CSR) problems
3. XML sitemaps
4. URL structure & canonicalization
5. Per-page head essentials
6. Social / Open Graph
7. Structured data (JSON-LD)
8. Status codes, redirects & SPA 404s
9. HTTPS & security signals
10. Internal linking & navigation
11. Mobile-friendliness (see also checks-mobile.md)
12. Core Web Vitals as a signal
13. hreflang / i18n
14. Accessibility overlaps
15. Framework-specific gotchas
16. Emerging: AEO / llms.txt
17. Grep cheat-sheet + runtime confirmations

---

## 1. Crawlability Blockers (check first)

### 1.1 robots.txt over-blocking `[HIGH]`
- **Why:** `Disallow: /` blocks the whole site. Blocking JS/CSS prevents Wave-2 rendering (Google must fetch `/assets/*.js` to render an SPA).
- **Spot:** read `public/robots.txt` (Vite/static), `app/robots.ts`/`robots.js` (Next). Grep `Disallow: /$`, `Disallow: /assets`, `Disallow: /_next`, `Disallow: *.js`. Watch for a default deploy robots shipping `Disallow: /`. Confirm the file returns 200 (not the SPA HTML fallback).
- **Fix:** Permissive prod robots (`User-agent: *` / `Allow: /`) + a `Sitemap:` line. Never disallow `/_next/static/`, `/assets/`, JS/CSS. Next: `app/robots.ts` returning prod rules.

### 1.2 `noindex` left in from staging/boilerplate `[HIGH]`
- **Why:** `<meta name="robots" content="noindex">` removes the page from the index even when crawlable — the #1 "why isn't my site indexed" cause.
- **Spot:** grep whole repo incl. built `dist/` for `noindex`, `content="noindex`, `index: false`. Check `index.html`, layouts, `react-helmet`/`next/head`, Next `metadata` (`robots: { index:false }`), env-gated `if (!isProd) noindex`.
- **Fix:** Remove from prod. If env-gated, verify the prod env var is actually set at build. Next preview: gate via `VERCEL_ENV !== 'production'`.

### 1.3 X-Robots-Tag HTTP header `[HIGH]` (easy to miss)
- **Why:** A `X-Robots-Tag: noindex` **response header** deindexes like the meta tag but is invisible in HTML.
- **Spot:** grep `netlify.toml`, `_headers`, `vercel.json`, `next.config.js` (`headers()`), `nginx.conf`, `.htaccess`, `middleware.ts` for `X-Robots-Tag`. Confirm with `curl -I`.
- **Fix:** Remove `noindex`/`none` from prod headers. (This IS the right place to noindex non-HTML like PDFs, if intended.)

### 1.4 robots meta injected by JS `[HIGH]` (SPA-specific)
- **Why:** A JS-added directive only exists after render; if the page is also disallowed in robots.txt, Google never sees the meta at all.
- **Spot:** compare `view-source:` vs rendered DOM; grep `Helmet`, `useHead`, dynamically-set `name="robots"`.
- **Fix:** Put the canonical index directive in **static** `index.html`/SSR output. Never disallow a URL whose meta you want honored.

---

## 2. Client-Side Rendering Problems (the core SPA risk)

### 2.1 Empty initial HTML / content only in JS `[HIGH]`
- **Why:** A stock Vite/CRA SPA ships `<div id="root"></div>` and nothing else — Wave 1 sees a blank page; content depends on the slower, rationed Wave 2. Marketing sites can be near-invisible, and totally invisible to AI answer engines and social scrapers (which mostly **don't** run JS).
- **Spot:** open `dist/index.html`. If `<body>` is basically `<div id="root"></div>` + a module script, all content is client-rendered. `curl <url> | rg "<h1"` — if your headline isn't there, crawlers don't see it in Wave 1.
- **Fix (ranked):** (a) **SSG/prerender** — best for marketing sites (`vite-react-ssg`, `vike`, post-build `react-snap`/Puppeteer). (b) **SSR** (Next.js/Remix) for dynamic content. (c) Dynamic rendering is now an explicit **legacy workaround** Google discourages — don't recommend for new builds.

### 2.2 Hash-based routing (`#/`) `[HIGH]`
- **Why:** Everything after `#` is ignored — every route collapses to one indexable URL. The old `#!` scheme is deprecated.
- **Spot:** grep `HashRouter`, `createHashHistory`, `createHashRouter`, `#/` in hrefs.
- **Fix:** `BrowserRouter`/History API (clean paths) + a server rewrite serving `index.html` for deep links, combined with prerender (2.1) so those paths have real content.

### 2.3 Hydration-gated / animated-in content `[MED]`
- **Why:** Content revealed only after hydration or via JS animation (GSAP `opacity:0` intros) may be missing from the indexable snapshot if JS is delayed/fails.
- **Spot:** hydration warnings, `suppressHydrationWarning`, content behind `useEffect`/`isMounted`, `gsap.from({opacity:0})` on primary copy without a visible fallback.
- **Fix:** Critical content in server HTML and visible by default (animate *from* a visible state, or CSS that doesn't hide content when JS is absent). Fix hydration mismatches.

### 2.4 Interaction-gated primary content `[MED]`
- **Why:** Content behind "Load more"/tabs/IntersectionObserver may not render — Googlebot doesn't scroll/click.
- **Spot:** grep `IntersectionObserver`, `React.lazy` on above-fold sections, `onClick`-gated content fetches.
- **Fix:** Server-render / include primary content in initial HTML; lazy-load only genuinely below-fold, non-critical media.

---

## 3. XML Sitemaps `[MED–HIGH]`
- **Why:** Aids discovery (deep/orphaned pages, JS sites). Stale/invalid sitemaps waste crawl budget.
- **Spot:** presence (`public/sitemap.xml`, `app/sitemap.ts`, `next-sitemap.config.js`); referenced in robots (`Sitemap: https://…`, absolute); valid XML, absolute HTTPS URLs, ≤50k URLs/50MB (else a sitemap index); fresh (all 200, no 404/redirect/noindex/localhost URLs — grep the sitemap for `localhost`/`http://`/dev domains); Next `app/sitemap.ts` or `next-sitemap` runs at build (`postbuild`).
- **Fix:** Generate at build from the route manifest; only canonical, indexable, 200 URLs; reference (absolute) in robots.txt; submit in Search Console.

## 4. URL Structure & Canonicalization

### 4.1 Canonical tags `[HIGH]`
- **Why:** Missing/wrong `<link rel="canonical">` dilutes duplicates or points ranking to the wrong/dev URL. In SPAs a single static canonical means **every route claims to be the homepage**.
- **Spot:** grep `rel="canonical"`. In SPAs check it's per-route and in initial HTML, not hardcoded `/`; check for `localhost`/staging domains. Next: `alternates: { canonical }`.
- **Fix:** Self-referencing, absolute, per-page canonical matching the indexable URL; prerender so it's in raw HTML.

### 4.2 Trailing-slash & www/protocol consistency `[MED]`
- **Why:** `/about` vs `/about/`, `www` vs apex, `http` vs `https` served as separate 200s = duplicates + split signals; chains waste crawl budget.
- **Spot:** check host/CDN config (`vercel.json` `cleanUrls`/`trailingSlash`, `next.config` `trailingSlash`, `netlify.toml`, `.htaccess`); `curl -IL` both variants — one should single-301 to the other; confirm `http→https` and `www→apex`.
- **Fix:** One canonical form, single 301s, sitemap + internal links consistent.

### 4.3 Duplicate / param URLs `[MED]`
- **Spot:** links with tracking params, faceted nav.
- **Fix:** Canonicalize to the clean URL; avoid indexable param permutations.

## 5. Per-Page Head Essentials
- **Unique `<title>` `[HIGH]`:** SPA risk = same title every route (static in `index.html`). Confirm per-route (Helmet/metadata/`generateMetadata`) **and in raw HTML**. Next: `title.template` in root layout + per-page override.
- **Meta description `[MED]`:** drives CTR; missing → auto-generated. Grep `name="description"`; unique per page.
- **`<html lang>` `[MED]`:** grep `<html` — flag missing `lang`. Next: root layout `<html lang="en">`.
- **`<meta charset="utf-8">` `[MED]`:** first in `<head>`.
- **`<meta name="viewport">` `[HIGH]`:** mobile-first — must be `width=device-width, initial-scale=1` (see checks-mobile.md).

## 6. Social / Open Graph `[MED]`
- **Why:** OG/Twitter tags control link previews (social, Slack, iMessage) and feed some AI surfaces. Scrapers **don't run JS** — JS-injected OG tags are invisible. Common SPA failure.
- **Spot:** grep `og:title`, `og:description`, `og:image`, `og:url`, `twitter:card`. Verify in **raw HTML** (view-source/curl), not Helmet-only. `og:image` = absolute HTTPS to an existing ~1200×630 image.
- **Fix:** Emit server-side/prerendered per page. Next: `openGraph`/`twitter` in metadata (+ `opengraph-image` file). For Vite SPAs this is a strong reason to prerender.

## 7. Structured Data / JSON-LD `[MED — HIGH for rich results]`
- **Why:** Helps Google understand entities, unlocks rich results, central to AEO/AI answers. Google prefers JSON-LD over Microdata/RDFa.
- **Spot:** grep `application/ld+json`, `schema.org`. Relevant types: `Organization`/`WebSite` (home), `Article`/`BlogPosting`, `Product`+`Offer`, `BreadcrumbList`, `FAQPage`, `LocalBusiness`. Confirm it's in raw HTML, valid JSON, and **matches visible content** (Google penalizes mismatch). SPA risk: JS-injected only.
- **Fix:** Add appropriate schema, render server-side, validate with the Rich Results Test. Don't mark up content not visible on the page.

## 8. Status Codes, Redirects & SPA 404s

### 8.1 Redirect hygiene `[MED]`
- **Spot:** `301` vs `302`/`307` in config; trace chains `curl -IL`.
- **Fix:** Single-hop 301s for permanent moves.

### 8.2 SPA soft 404s `[HIGH]`
- **Why:** SPAs serve `index.html` (HTTP **200**) for *every* path incl. nonexistent ones, then show "Not Found" client-side → Google sees 200 + thin content = soft 404; wastes crawl budget on infinite non-pages.
- **Spot:** `curl -I <url>/this-page-does-not-exist` → a `200` is the bug.
- **Fix:** Return a real **404** for unknown routes (host 404 config, or prerender known routes and 404 the rest). Next: `not-found.tsx`. Add `noindex` to error states as backup.

## 9. HTTPS & Security Signals
- **HTTPS everywhere `[MED]`:** ranking signal; ensure http→https 301.
- **Mixed content `[MED]`:** HTTPS page loading `http://` assets breaks the padlock / blocks resources. Grep source + built output for `http://` in `src`/`href` (excluding schema/xmlns URIs).
- **HSTS `[LOW]`:** `Strict-Transport-Security` header — minor.

## 10. Internal Linking & Navigation `[HIGH]` (SPA crawl-path risk)
- **Why:** Google follows **`<a href>`** in HTML. Navigation via `onClick`+`navigate()`/`router.push` **without an href** is invisible → orphaned pages. The single most common way a fine SPA hides its own pages.
- **Spot:** grep `onClick={() => navigate(`, `onClick={() => router.push(` on non-anchors; `<div>`/`<button>` used as nav. Confirm real anchors (`<Link to>` / `next/link` render `<a>`). Check nav/footer render hrefs in **raw HTML**. Watch JS-only mega-menus.
- **Fix:** Real `<a href>` for all navigation; primary nav + footer in server/prerendered HTML; no orphans; important pages reachable within ~3 clicks.

## 11. Mobile-Friendliness `[HIGH]` (mobile-first indexing)
- **Why:** Google indexes the **mobile** version. Content/links/structured data hidden on mobile may not be indexed; missing viewport → ranking hit.
- **Spot:** confirm the viewport meta; check Tailwind `hidden md:block` isn't hiding primary copy/links on mobile. See **checks-mobile.md** for the full responsive pass.
- **Fix:** Responsive layout; content/link parity mobile↔desktop; correct viewport.

## 12. Core Web Vitals as a signal `[MED]`
- CWV (LCP, INP replaced FID 2024, CLS) are confirmed (minor) ranking signals; slow/heavy JS also reduces effective crawl budget and delays Wave-2. Depth is in **checks-performance.md** — flag large bundles, unoptimized hero images (LCP), animation CLS, blocking scripts. Fewer/faster resources = more pages crawled.

## 13. hreflang / i18n `[MED — only if multi-language]`
- **Spot:** grep `hreflang`. Each version references all others **and itself** (bidirectional), valid `lang-REGION` codes, `x-default`, absolute URLs. Next: `alternates.languages`.
- **Fix:** Complete reciprocal hreflang per page, in raw HTML/SSR.

## 14. Accessibility Overlaps `[MED]`
- **Alt text:** image SEO + a11y. Grep `<img` missing `alt`; flag CSS/GSAP background images carrying primary content (no alt/semantics).
- **Descriptive filenames `[LOW]`:** `hero-red-shoe.webp` > `IMG_2831.jpg`.
- **Semantic HTML / landmarks:** `<header><nav><main><article><footer>` aid understanding; flag div-soup / missing `<main>`.
- **Headings:** exactly **one `<h1>`** per page, logical descent — grep and count `<h1` (GSAP heroes often duplicate/omit).

## 15. Framework-Specific Gotchas

**Next.js (usually strong, but check):**
- **Metadata API `[HIGH]`:** static `metadata` for stable pages, `generateMetadata` for dynamic — both **Server Components only**. Grep `"use client"` components trying to set metadata (won't work). `title.template` in root layout.
- **Preview/staging noindex leaking to prod `[HIGH]`:** `robots.ts`/metadata gated on `VERCEL_ENV`/`NODE_ENV` — verify prod isn't caught. Grep `index: false`, `noindex`, `VERCEL_ENV`.
- **Sitemap `[MED]`:** `app/sitemap.ts`/`next-sitemap` present, runs at build, covers dynamic routes.
- **Dynamic routes `[MED]`:** `generateStaticParams`; bad slugs `notFound()` (real 404, not soft-404).
- **`next/image`/`next/link`** used.

**Vite / CSR SPA (highest-risk — check):**
- **Per-route head not reaching crawlers `[HIGH]`:** `react-helmet` sets title/meta/canonical/OG **client-side only** → invisible to Wave 1, social, AI. Grep `Helmet`, `HelmetProvider`. Looks fixed in devtools, isn't for crawlers.
- **No prerender step `[HIGH]`:** check build for `vite-react-ssg`, `vike`, `react-snap` (postbuild), Puppeteer prerender. Absent + Helmet-driven meta = effectively invisible. **The flagship finding for a Vite marketing SPA.**
- **`dist/index.html` empty shell `[HIGH]`** (2.1).
- **BrowserRouter + server rewrite + real 404** (2.2, 8.2).

## 16. Emerging: AEO / llms.txt `[LOW–MED]`
- AI answer engines favor **raw-HTML content + JSON-LD + clean structure** — the same fixes as §2 + §7, so this mostly rides along. `llms.txt` (markdown index at site root) is an emerging, unofficial convention (Google hasn't endorsed it). Check `public/llms.txt`; confirm robots doesn't block AI crawlers (`GPTBot`, `PerplexityBot`, `CCBot`, `Google-Extended`) *if* AI visibility is desired (a business decision). Don't oversell it — primary lever is still real content in HTML + JSON-LD + fast semantic pages.

## 17. Grep Cheat-Sheet + Runtime Confirmations

| Signal | Pattern | § |
|---|---|---|
| Full-site block | `Disallow: /$` in robots | 1.1 |
| Blocked JS/CSS | `Disallow: .*\.(js\|css)`, `/assets`, `/_next` | 1.1 |
| noindex anywhere | `noindex`, `index:\s*false` | 1.2, 15 |
| Header noindex | `X-Robots-Tag` in config | 1.3 |
| Empty SPA shell | `<div id="root"></div>` sole body in `dist/index.html` | 2.1 |
| Hash routing | `HashRouter`, `createHashRouter`, `#/` | 2.2 |
| Client-only head | `Helmet`, `HelmetProvider` (no prerender) | 15 |
| JS-only nav | `onClick={() => navigate(`, `router.push(` on non-anchors | 10 |
| Canonical to home/localhost | `rel="canonical"` = `/` or `localhost` | 4.1 |
| Missing lang / viewport | `<html` without `lang=`; no `name="viewport"` | 5 |
| OG in HTML? | `og:image` in view-source vs Helmet-only | 6 |
| Structured data | `application/ld+json` present + valid | 7 |
| No sitemap | no `sitemap.xml`/`sitemap.ts`; no `Sitemap:` in robots | 3 |
| Prerender present? | `vite-react-ssg`/`vike`/`react-snap` in build | 15 |

**Runtime (don't rely on source alone):**
```
curl -sL https://site/ | rg -i "<h1|og:image|canonical|robots"   # content/meta in raw HTML?
curl -I https://site/nonexistent                                  # soft 404 (200 = bug)?
curl -I https://site/                                             # X-Robots-Tag header?
# compare view-source: vs rendered DOM                            # JS-injected content?
```

**Typical Vite marketing SPA triage:** the recurring high-severity cluster is §2.1 empty HTML + §15 Helmet-only meta + no prerender → title/description/OG/canonical/content all invisible to Wave 1 and non-JS crawlers. **Fixing rendering (prerender/SSG) resolves the majority of findings at once.**

**Sources:** [Google JS SEO basics](https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics) · [Robots meta spec](https://developers.google.com/search/docs/crawling-indexing/robots-meta-tag) · [Next.js generateMetadata](https://nextjs.org/docs/app/api-reference/functions/generate-metadata) · [Dec 2025 error-page rendering update](https://ppc.land/google-clarifies-javascript-rendering-for-error-pages-in-december-documentation-update/)
