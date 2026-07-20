# Page Structure — One Screen, One Decision

A dedicated landing page converts 2–5x higher than sending paid traffic to a homepage. The page's only job: continue the ad's promise and collect ONE decision.

## Contents
- [Structure rules](#structure-rules)
- [Single-screen anatomy](#single-screen-anatomy)
- [CTA](#cta)
- [Trust & risk reversal (ranked)](#trust--risk-reversal)
- [Mobile (~390px)](#mobile)
- [Data points](#data-points)

## Structure rules

1. **Attention ratio 1:1** — links on page : conversion goals. Unbounce data: 1 link = 13.8% conversion vs 10 links = 5.86%; removing 3 links ≈ +50%.
2. **No navigation bar.** Nav removal lifted conversion up to +28% (HubSpot), +100% (Yuppiechef), +336% with form above fold (Career Point). Only ~16% of live pages do this — it's a real edge.
3. **No footer links** except legally required Privacy + Terms in tiny ghost text (Meta lead pages REQUIRE a privacy policy link).
4. **One decision per page.** Single-CTA pages: 13.5% vs 10.5% for 3+ CTAs (Unbounce, 18,639 pages). Jam study: 24 choices → 3% buy; 6 → ~30%.
5. **One dedicated page per ad angle** — message match per angle, never one generic page.
6. **Headline ≤8 words, outcome-focused**, message-matched to the ad (see `headlines.md`).
7. **Write at 5th–7th grade reading level.** Converts 11.1% vs 7.1% (grade 8–9) vs 5.3% (professional) — Unbounce CBR 2024.
8. **Cut copy ruthlessly** — word count, reading time, and difficult words all correlate negatively with conversion.
9. **CTA above the fold, enforced at ~390px** — above-fold CTAs perform up to +304%.
10. **If the page scrolls at all, repeat the SAME CTA** (identical copy/goal) — never add a different one. Repeated single CTA: +20–84% in tests.
11. **Form: 3 fields max; fewer is better.** 3-field forms peak ~25% (HubSpot); 11→4 fields = +120%; 1-field squeeze pages hit 30–60% on targeted traffic. Delete any field follow-up doesn't strictly need (Expedia deleted one field: +$12M/yr). No dropdowns, textareas, or "company" unless required.
12. **One trust element in the first screen, adjacent to the CTA.** Specific beats generic ("4.9★ from 312 roofers" > "trusted by thousands"). Cap at 3–4 badges total — badge bloat cuts conversion 5–8%.
13. **Load under 3 seconds** — 53% of mobile users abandon >3s; ~4.4% conversion lost per extra second. No hero video, no carousels, no web-font stacks, no third-party scripts beyond the ad pixel/analytics.
14. **No sliders, no auto-play video, no social icons** — attention leaks or speed taxes, all of them.
15. **Hero visual (if any) reinforces the one message** — a mockup of the deliverable or the outcome. If it competes with the headline, cut it.

## Single-screen anatomy

Top-to-bottom (must fit ~390×844 mobile viewport; test desktop ~1440px too):

1. **Logo** — small, top-left, NOT linked (a linked logo is an exit). Optional phone number top-right for call-intent local traffic (same goal, not a second one).
2. **Eyebrow** (optional, 1 line, small caps) — who it's for or message-match echo: "For veteran-owned HVAC shops."
3. **H1** — largest text element. ≤8 words, outcome, ad-matched.
4. **Subheadline** — 1–2 lines: mechanism + specificity + objection-kill.
5. **3 benefit bullets** (optional — include for lead magnets/quotes; skip when headline+sub carry it). Checkmarks, ≤7 words each, specific numbers.
6. **Conversion unit** — 1–3-field form OR single button. Highest-contrast element on the page. Two-step opt-in (button → form in step 2) keeps the screen to one button and exploits micro-commitment.
7. **CTA button** — first-person outcome copy, ≥48px tall (56px+ better), full-width on mobile.
8. **Risk-reversal micro-line directly under the button** — "Free — no credit card" / "Takes 30 seconds".
9. **One trust strip** — pick ONE: stars + count, 3–4 known logos, or a one-line micro-testimonial with name.
10. **Legal footer** — © + Privacy + Terms, tiny and low-contrast. Nothing else.

Visual-weight order: CTA ≥ headline > form > subhead > bullets > trust > everything else. The CTA gets the most whitespace around it of anything on the page.

## CTA

**Copy formula: [Action verb] + "my" + [specific outcome].** First-person "my" beat "your" by 90% in Aagaard's Unbounce test (replications +10–40%). Never "Submit", "Sign Up", "Continue", "Learn More".

Examples: "Get My Free Quote" · "Get My Free Analysis" · "Send Me the Checklist" · "Start My Free Trial" · "Show My Results" (quiz) · "Book My Free Call" · "Claim My Free Audit" · "Get My Price in 60 Seconds" · "Reserve My Spot".

Placement: thumb zone (middle/bottom third) on mobile; a hue used nowhere else on the page (never grey); if scroll exists, sticky bottom bar on mobile with the identical CTA.

## Trust & risk reversal

Ranked by impact for a single-screen paid page — pick 1–2 max:

1. **"No credit card required" / "Free" under the CTA** — kills the #1 objection at the decision moment (+71% trial signups in one SaaS case).
2. **Money-back / performance guarantee** — +21–26% typical, +52% high-ticket; 60-day beats 30-day by 23% and strong guarantees CUT refund rates. "Book 10 jobs in 60 days or you don't pay."
3. **Stars + review count** — 5 reviews vs none = +270% purchase likelihood; sweet spot 4.75–4.99 (a perfect 5.0 converts like a 3.0 — distrusted).
4. **Micro-testimonial: real name + specific number** — ""Booked 14 estimates in week one." — Mike R., Reyes Plumbing."
5. **Effort/time reassurance** — "Takes 30 seconds." Cheap, always fits.
6. **3–4 client logos** — only if recognizable to THIS audience.
7. **Privacy micro-line** on email forms — "No spam. Unsubscribe anytime."
8. **Security seals** — only next to payment fields; noise on lead-gen pages. Cut.
9. **"As seen in" press logos** — weakest for direct response. Cut unless genuinely famous.

## Mobile

- Entire anatomy fits ~390×844: headline + sub + CTA + risk line visible without scroll; bullets/trust may sit at the fold line. If content pushes the CTA down, cut bullets before cutting the CTA.
- Type: H1 30–36px via `clamp()` with line-parity vs desktop (no orphan words); sub 16–18px; button 17–18px; micro-copy floor 13px; inputs ≥16px font (prevents iOS zoom).
- Tap targets ≥48px (56px+ for the CTA), button + inputs full-width, ≥8px spacing.
- Correct `type`/`inputmode` on fields (tel, email) for the right keyboard; labels above fields, not placeholder-only.
- Shorter button copy on mobile: "Get My Quote", not "Start Your 14-Day Free Trial Today".

## Data points

| Metric | Number |
|---|---|
| 1 link vs 10 links | 13.8% vs 5.86% conversion (Unbounce) |
| Nav removal | +28% (HubSpot) / +100% (Yuppiechef) / +336% w/ form above fold |
| 1 CTA vs 3+ | 13.5% vs 10.5% (Unbounce, 18,639 pages) |
| First-person button copy | +90% clicks (Aagaard) |
| Above-fold CTA | up to +304% |
| 3-field form | ~25% peak conversion (HubSpot) |
| Grade 5–7 copy vs professional | 11.1% vs 5.3% (Unbounce CBR 2024) |
| Median LP conversion | 6.6% all-industry; top pages 20%+ (Unbounce CBR 2024) |
| Mobile abandonment >3s load | 53% (Google) |
| Guarantee | +21–52% |
| 5 reviews vs 0 | +270% purchase likelihood (Spiegel/Northwestern) |
