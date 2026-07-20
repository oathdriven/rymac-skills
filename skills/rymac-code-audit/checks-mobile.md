# Responsive / Mobile-Compatibility Checklist

Catch the layout breakage on phones **before** it ships — the "had to go back and fix mobile after production" class of bug. For React/Vite/Tailwind/GSAP sites, Next.js, and static HTML. Each item: **why → how to spot (grep signals) → fix → impact**. Greps assume ripgrep (`rg`).

**Test widths:** 320px (small phone, the hard floor), 375/390px (typical iPhone), 414px, 768px (tablet). If anything horizontally scrolls or overlaps at 320–414px, it's a bug. Also remember Google indexes the **mobile** version (see checks-seo.md §11).

## Contents
1. Viewport & meta
2. Horizontal overflow (the #1 mobile bug)
3. Fixed pixel sizing that won't reflow
4. Touch targets & spacing
5. Hover-only / touch-hostile interactions
6. Inputs & mobile keyboards
7. `100vh` and mobile viewport units
8. Navigation (hamburger / off-canvas)
9. Images & media on mobile
10. Tables & wide content
11. Fixed / sticky / absolute overlap
12. Typography & readability
13. Breakpoints & mobile-first order
14. Content hidden or duplicated across breakpoints
15. Animation / GSAP on mobile
16. Safe areas / notches
17. How to actually test
18. Grep cheat-sheet

---

## 1. Viewport & meta `[HIGH]`
- **Why:** Without the viewport meta, mobile browsers render at ~980px and shrink it — everything is tiny, tap targets fail, and the site isn't "mobile-friendly" (a ranking hit).
- **Spot:** grep `index.html` / `app/layout.*` for `name="viewport"`. Flag if **missing**; flag `user-scalable=no` / `maximum-scale=1` (blocks pinch-zoom — accessibility failure). Next.js: `export const viewport` or a `<meta>` in the root layout.
- **Fix:** `<meta name="viewport" content="width=device-width, initial-scale=1">`. Never disable zoom. Add `viewport-fit=cover` only when handling safe areas (§16).

## 2. Horizontal overflow — the #1 mobile bug `[HIGH]`
- **Why:** One element wider than the screen creates a horizontal scrollbar and a "shifted" broken page. The most common post-production mobile complaint.
- **Spot:**
  - Fixed widths bigger than a phone: `rg -n "w-\[[4-9][0-9]{2,}px\]|w-\[[0-9]{4,}px\]"` (Tailwind `w-[400px]`+), `rg -n "width:\s*[4-9][0-9]{2,}px|min-width:\s*[3-9][0-9]{2,}px"`.
  - `min-w-` / `min-width` on wide elements that can't shrink.
  - `100vw` used for full-bleed (includes the scrollbar width → slight overflow): `rg -n "100vw|w-screen"`.
  - `whitespace-nowrap` / `nowrap` on long text; long unbroken strings (URLs, tokens).
  - Negative margins, `left:`/`right:` offsets pushing content past the edge.
  - Grids with fixed column counts that don't collapse (`grid-cols-4` with no responsive prefix).
  - Flex rows that don't wrap (`flex` without `flex-wrap` holding wide children).
- **Fix:** Relative units + `max-w-full`/`max-width:100%`, `w-full` over fixed px, `min-w-0` on flex children that must shrink, `flex-wrap`, responsive grid (`grid-cols-1 md:grid-cols-4`), `overflow-wrap:break-word` / `break-words` for long strings. Quick diagnostic: temporarily `* { outline: 1px solid red }` or run the DevTools "find overflowing element" check. As a guard, `body { overflow-x: hidden }` hides the symptom but **find the real cause first**.

## 3. Fixed pixel sizing that won't reflow `[MED]`
- **Why:** Hardcoded px widths/heights look right on the design canvas and break on every other screen.
- **Spot:** `rg -n "w-\[[0-9]+px\]|h-\[[0-9]+px\]"` (Tailwind arbitrary px); `rg -n "width:\s*\d+px|height:\s*\d+px"` in CSS on layout containers; fixed-height heroes/cards that clip content when text wraps to more lines on narrow screens.
- **Fix:** Relative units (`%`, `rem`, `vw` with a `max`), `clamp()` for fluid sizing, `min-height` instead of fixed `height` so content can grow, `aspect-ratio` for media boxes.

## 4. Touch targets & spacing `[MED]`
- **Why:** Fingers need room — targets under ~44×44px (Apple) / 48×48px (Google) are mis-tapped; buttons packed together cause wrong taps.
- **Spot:** tiny icon buttons (`rg -n "<button"` with only an icon and small padding, `p-1`/`p-0.5`, `w-4 h-4` hit areas); links in dense lists/footers with no vertical padding; close/menu icons sized `16–20px` with no padding.
- **Fix:** Minimum ~44px tappable area (pad the target even if the icon is small), adequate gap between adjacent controls (`gap-2`+), full-width primary buttons on mobile.

## 5. Hover-only / touch-hostile interactions `[HIGH]`
- **Why:** Phones have **no hover.** Menus, tooltips, and content that only appear on `:hover`/`onMouseEnter` are unreachable or stuck on touch devices.
- **Spot:** `rg -n "onMouseEnter|onMouseLeave|onMouseOver"` driving nav/menus/tooltips; CSS `:hover`-only dropdowns (`group-hover:` in Tailwind with no click/focus equivalent); dropdown menus with no `onClick`/tap toggle; `title=`-only tooltips (don't show on touch).
- **Fix:** Make it work on **tap/click** (and keyboard focus): toggle menus on click, show tooltips on tap/focus, or use `@media (hover: hover)` to gate hover-only enhancements. Test the nav at 375px with touch emulation.

## 6. Inputs & mobile keyboards `[MED]`
- **Why:** Two classic mobile annoyances: (a) iOS **auto-zooms** when focusing an input whose `font-size` is under 16px; (b) the wrong keyboard appears for the field.
- **Spot:** `rg -n "font-size:\s*1[0-5]px|text-\[1[0-5]px\]|text-xs|text-sm"` on `<input>`/`<textarea>`/`<select>`; `<input>` without a specific `type`/`inputmode` (`rg -n "<input"` then check for `type="email|tel|number|url"`, `inputmode`, `autocomplete`); missing `autocomplete` on name/email/address fields.
- **Fix:** Inputs ≥16px font on mobile (Tailwind `text-base` on inputs). Correct `type`/`inputmode` (`type="email"`, `type="tel"`, `inputmode="numeric"`) so the right keyboard shows. Add `autocomplete` tokens for faster fill.

## 7. `100vh` and mobile viewport units `[MED]`
- **Why:** On mobile, `100vh` includes the area behind the browser's URL bar, so full-height sections/heroes get **cut off** or jump when the bar shows/hides.
- **Spot:** `rg -n "100vh|h-screen|min-h-screen"` on heroes/overlays/modals.
- **Fix:** Use **dynamic viewport units** — `100dvh` (Tailwind `h-dvh`/`min-h-dvh`) for fill-the-screen, or `svh`/`lvh` where appropriate. Keep a `100vh` fallback for old browsers via `@supports`.

## 8. Navigation (hamburger / off-canvas) `[HIGH]`
- **Why:** A desktop nav bar that doesn't collapse overflows or wraps into a mess on phones; the most visible mobile break.
- **Spot:** a `<nav>` with many links and no responsive collapse (no `hidden md:flex` + a mobile menu button); no hamburger/`Menu` toggle component; off-canvas menu with no scroll-lock or no close control; mobile menu that doesn't cover full width/height.
- **Fix:** Collapse to a hamburger below the breakpoint (`hidden md:flex` desktop nav + a `md:hidden` menu button), a full-height off-canvas/drawer that locks body scroll while open and is dismissible (tap-outside + close button + Esc), and links that are real `<a href>` (crawl + a11y).

## 9. Images & media on mobile `[MED]`
- **Why:** Oversized images blow the layout, waste mobile data, and shift content; videos/iframes overflow.
- **Spot:** `<img>` without `max-w-full`/`w-full` in a constrained container; no `srcset`/`sizes` (serving a desktop-size file to phones — also perf, see checks-performance.md §3); `<iframe>`/embeds with fixed px width; background images with `background-size` not `cover`/`contain`; missing width/height → CLS on mobile.
- **Fix:** `max-width:100%`/`w-full h-auto` on images, responsive `srcset`+`sizes`, wrap embeds in a fluid `aspect-ratio` container, `object-fit: cover`.

## 10. Tables & wide content `[MED]`
- **Why:** Data tables and wide `pre`/code blocks don't fit a phone and force horizontal page scroll (§2).
- **Spot:** `rg -n "<table"` without a scroll wrapper; `<pre>`/code blocks; wide flex/grid card rows.
- **Fix:** Wrap the wide element in a scroll container (`overflow-x-auto` on the wrapper only, not the page), or switch to a stacked/card layout on mobile, or make columns collapse.

## 11. Fixed / sticky / absolute overlap `[MED]`
- **Why:** On short mobile viewports, `position:fixed`/`sticky` headers, cookie bars, chat bubbles, and CTAs overlap content or each other and cover tap targets.
- **Spot:** `rg -n "position:\s*fixed|fixed\s|sticky\s|position:\s*sticky"`; multiple fixed elements (header + cookie + chat) with no coordinated spacing; content with no top/bottom padding to clear a fixed header/footer; high `z-index` stacking (see checks-correctness.md §10.6).
- **Fix:** Reserve space for fixed bars (padding/margin on content), stack fixed elements so they don't collide, ensure floating widgets don't cover primary CTAs on small screens, test with the keyboard open.

## 12. Typography & readability `[MED]`
- **Why:** Desktop font sizes/line-lengths don't translate; huge display headings overflow, tiny body text is unreadable, long words break the layout.
- **Spot:** large fixed heading sizes with no responsive step-down (`text-6xl` with no `text-3xl md:text-6xl`); `rg -n "text-\[[0-9]{2,}px\]"`; long unbreakable strings (§2); very long line lengths with no `max-w-*` on prose.
- **Fix:** Responsive type scale (`text-3xl md:text-5xl`) or `clamp()`, `break-words`/`hyphens-auto` for long strings, `max-w-prose`/`max-w-[65ch]` on body copy, body ≥16px.

## 13. Breakpoints & mobile-first order `[MED]`
- **Why:** Tailwind (and good CSS) is **mobile-first** — unprefixed classes are the mobile base, `md:`/`lg:` layer on larger screens. Writing desktop-first (everything styled for desktop, then patched down with `max-*`) leaves gaps and awkward mid-sizes.
- **Spot:** components where the base (unprefixed) styles are the *desktop* layout and mobile is an afterthought; heavy use of `max-md:`/`max-lg:` overrides; custom `@media (max-width)`-only CSS; a `tailwind.config` with unusual breakpoints — confirm the design's real breakpoints are covered; layouts that only look tested at one width.
- **Fix:** Author base styles for mobile, add complexity upward with `sm:`/`md:`/`lg:`. Verify every breakpoint boundary (just below and above 640/768/1024).

## 14. Content hidden or duplicated across breakpoints `[MED]`
- **Why:** `hidden md:block` / `md:hidden` pairs are common, but hiding **primary content or links** on mobile hurts UX and SEO (mobile-first indexing), and duplicated desktop/mobile markup drifts out of sync.
- **Spot:** `rg -n "hidden md:|md:hidden|lg:hidden|hidden lg:"` around headings, nav links, CTAs, or body content (not just decorative); two near-identical blocks (one `md:hidden`, one `hidden md:block`).
- **Fix:** Keep content/link parity between mobile and desktop; prefer one responsive component over separate mobile/desktop copies; only hide genuinely decorative or redundant elements.

## 15. Animation / GSAP on mobile `[MED]`
- **Why:** Heavy scroll animations jank on low-end phones (INP/CLS); ScrollTrigger positions miscalculate when the mobile URL bar resizes; scroll-jacking feels broken on touch.
- **Spot:** `rg -n "ScrollTrigger"` with no `invalidateOnRefresh`/`refresh()` after resize; `gsap.matchMedia()` absent (no per-breakpoint or reduced-motion branch); scroll-hijacking/pinned sections not adapted for touch; `prefers-reduced-motion` unhandled (see checks-performance.md §6).
- **Fix:** `gsap.matchMedia()` to simplify/disable heavy animation on small screens and honor `(prefers-reduced-motion: reduce)`; `ScrollTrigger.refresh()` on resize / `invalidateOnRefresh: true`; avoid scroll-jacking on touch; keep animated elements from causing CLS.

## 16. Safe areas / notches `[LOW–MED]`
- **Why:** On notched/rounded phones, fixed headers/footers and full-bleed content get clipped by the notch or home indicator.
- **Spot:** fixed bottom bars/CTAs and full-screen overlays with no `env(safe-area-inset-*)`; `viewport-fit=cover` set without safe-area padding (or content edge-to-edge without it).
- **Fix:** `viewport-fit=cover` + `padding: env(safe-area-inset-top/bottom/left/right)` on fixed/edge elements (Tailwind arbitrary: `pb-[env(safe-area-inset-bottom)]`).

## 17. How to actually test
- **Chrome/Edge DevTools device toolbar** (Ctrl+Shift+M): step through 320 / 375 / 414 / 768; toggle touch; look for horizontal scroll and overlap. Use "Show rulers" + the overflow finder.
- **Responsive design mode** in Firefox; **Lighthouse mobile** (`npx lighthouse <url> --form-factor=mobile --screenEmulation.mobile`) for mobile-friendliness + perf.
- **A real phone** for the last mile (hover, keyboards, safe areas, momentum scroll) — emulators miss touch/keyboard nuances.
- Test **with the on-screen keyboard open** (covers inputs, resizes the viewport) and in **landscape**.

## 18. Grep cheat-sheet
```
# Viewport
name="viewport"            (absence = HIGH)  |  user-scalable=no|maximum-scale  (a11y fail)
# Horizontal overflow
w-\[[4-9][0-9]{2,}px\]|w-\[[0-9]{4,}px\]     # wide Tailwind fixed widths
width:\s*[4-9][0-9]{2,}px|min-width:\s*[3-9][0-9]{2,}px
100vw|w-screen                                # scrollbar overflow risk
whitespace-nowrap|nowrap                      # long text can't wrap
grid-cols-[3-9]                               # check for responsive prefix
flex(?!.*wrap)                                # rows that may not wrap
# Fixed sizing
w-\[[0-9]+px\]|h-\[[0-9]+px\]
height:\s*\d+px|width:\s*\d+px
# Touch / hover
onMouseEnter|onMouseOver                      # hover-only interactions
group-hover:                                  # verify a click/focus equivalent exists
# Inputs
<input                                        # check type/inputmode/autocomplete + >=16px font
text-xs|text-sm|font-size:\s*1[0-5]px         # on inputs = iOS zoom
# Viewport height
100vh|h-screen|min-h-screen                   # prefer dvh
# Nav
<nav                                          # verify responsive collapse + hamburger
# Fixed overlap
position:\s*fixed|fixed\s|sticky
# Responsive hiding
hidden md:|md:hidden|lg:hidden                # verify not hiding primary content
# Safe area
env\(safe-area-inset                          # presence on fixed/edge elements
# Animation
ScrollTrigger|gsap.matchMedia|prefers-reduced-motion
```

**Fastest high-value pass:** confirm the viewport meta exists, load the served site at **375px and 320px**, scroll for any horizontal shift, tap the nav and any hover menus, and focus an input to check for iOS zoom. Those five checks catch the large majority of "broken on mobile after launch" issues.
