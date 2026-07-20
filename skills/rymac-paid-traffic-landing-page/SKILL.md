---
name: rymac-paid-traffic-landing-page
description: Researches a niche's pains and builds a single-screen, one-decision landing page for paid ad traffic (Meta/Google/YouTube) — headline-first, message-matched to the ad, with one CTA and a risk-reversal/trust element, nothing else. Use when the user asks to "make a landing page for ads", "build a page for this campaign", "squeeze page", "lead capture page", "opt-in page", or wants to convert paid traffic for a niche. Make sure to use this skill for any ad-destination page; for multi-section marketing websites use website-builder or build-premium-website instead.
argument-hint: [niche/offer, traffic source, and CTA goal — e.g. "HVAC owners, Facebook ads, book a call"]
---

# Paid-Traffic Landing Page

Build a landing page whose only job is converting one ad click into one action. Headline quality is ~80% of the outcome; simplicity is the other 20%. Everything else is deleted, not designed.

Reference files (read at the step that needs them):
- `${CLAUDE_SKILL_DIR}/references/niche-research.md` — 12 intake questions, the 20-minute pain-mining sprint, sophistication stages, pain→copy mapping
- `${CLAUDE_SKILL_DIR}/references/headlines.md` — awareness levels, 13 rules, 16 formulas, subheadline formulas, message match
- `${CLAUDE_SKILL_DIR}/references/page-structure.md` — structure rules with conversion data, single-screen anatomy, CTA/trust rankings, mobile rules
- `${CLAUDE_SKILL_DIR}/assets/page-template.html` — the single-screen HTML shell with `{{TOKENS}}` to fill (read it, fill it, save as the deliverable; don't rebuild the layout from scratch)

## Workflow

Copy this checklist and tick it off:

- [ ] 1. Intake — parse `$ARGUMENTS`; collect what's missing
- [ ] 2. Mine the niche (research sprint, parallel subagents)
- [ ] 3. Diagnose awareness + sophistication
- [ ] 4. Write the copy elements, headline first
- [ ] 5. Build the page from the template
- [ ] 6. Run the conversion gate — fix anything that fails
- [ ] 7. Deliver page + copy doc with A/B alternates

### 1. Intake

Needed before writing: **niche/avatar, offer, traffic source + the ad's promise (for message match), CTA goal (lead form / booking / click-through), brand name + accent color.** Take what `$ARGUMENTS` and context give; ask the user only for genuinely unknowable items (the ad copy, the brand color). If no ad exists yet, note that the H1 should become the ad headline later — write them as one unit.

### 2. Mine the niche

Read `${CLAUDE_SKILL_DIR}/references/niche-research.md` and run its sprint. Fan out 2–3 parallel research subagents (Reddit/forums · reviews of competitors or current solutions · Meta Ad Library/competitor headlines) and have each return verbatim quotes tagged pain / desire / objection / failed-alternative / trigger. Rank by frequency × emotional charge. Output: 1 dominant pain, 1 dream outcome, top 3 objections, top 2 failed alternatives — in the prospect's exact words.

### 3. Diagnose

- **Awareness** of the traffic (cold social ≈ problem/solution-aware; search ≈ solution-aware; retargeting ≈ product/most-aware) — sets which headline formulas apply.
- **Sophistication** of the market (stage 1–5 from competitor ads) — write one stage ahead of the loudest incumbent; never repeat a worn-out claim.

### 4. Write the elements (headline first)

Read `${CLAUDE_SKILL_DIR}/references/headlines.md`. In order:

1. **Headline** — write 20 candidates from the 3 best-fitting formulas; if ad copy exists, the verbatim ad promise is always candidate #1. Cut to the strongest 3 by the rules (≤8 words, specific, visualizable, outcome-led, prospect's own words). Pick one; keep the other two as A/B variants.
2. **Subheadline** — mechanism + proof + kills the #1 objection. 10–30 words.
3. **3 bullets max** — ≤7 words each, specific numbers, mined language. Skip entirely if headline+sub carry the page.
4. **CTA** — `[verb] + my + [outcome]` ("Get My Free Quote"). Never "Submit"/"Learn More".
5. **Risk reversal** — one line under the button, aimed at the #1 mined objection ("Free — no credit card" / guarantee / "Takes 30 seconds").
6. **Trust line** — ONE element: stars+count, micro-testimonial with name + number, or 3–4 known logos. Only what's real — never fabricate reviews, counts, or testimonials; if nothing real exists, use effort reassurance instead.

### 5. Build the page

Fill `${CLAUDE_SKILL_DIR}/assets/page-template.html` (copy it into the project/output directory first). Lead form → Variant B with the fewest fields follow-up can survive on (3 max); booking/click-through → Variant A. Set the accent color; keep it the only saturated hue on the page. No additions: no nav, no sections below the fold, no images unless one visual directly shows the deliverable/outcome, no external scripts except the ad pixel if provided.

### 6. Conversion gate

Verify every line; fix and re-check anything that fails:

- [ ] H1 restates the ad's promise (message match) — or is flagged to become the ad headline
- [ ] H1 ≤8 words, outcome-led, passes the 5-second test (what / for whom / what to do)
- [ ] Copy reads at 5th–7th grade level
- [ ] Exactly ONE decision: one CTA goal, zero other links (Privacy/Terms ghost-text footer only)
- [ ] Headline + subhead + CTA + risk line all visible in a ~390×844 viewport without scrolling; CTA ≥48px tall, full-width on mobile, never grey
- [ ] Form (if any) ≤3 fields, correct input types
- [ ] One trust element, specific and true, adjacent to the CTA
- [ ] No render-blocking or third-party requests; page is a single self-contained file

### 7. Deliver

Hand back: the HTML file path, the chosen headline with the two A/B alternates, and a short copy doc (all elements + the mined quotes that justify them) so ads can be written with the same language. Recommend one page per ad angle — offer to spin variants by swapping H1/eyebrow.

## Rules

1. The headline is the product. Never spend more effort on layout than on headline candidates.
2. One page, one pain, one decision. Cut a second idea rather than fit it.
3. Prospect's verbatim words beat anything invented — if a phrase wasn't mined or given, question it.
4. Never fabricate proof (reviews, star counts, names, "as seen in").
5. Delete before adding: when the fold is tight on mobile, bullets go before the CTA does.
