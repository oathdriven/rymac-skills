---
name: rymac-headline-copywriting
description: Write and rewrite landing-page headlines, hero sections, and their CTAs using a pain + dream-outcome formula, awareness-stage diagnosis, and a curated SaaS swipe file. Use when the user asks to "write a headline", "rewrite the hero", "fix the landing page headline", "give me headline options", "punch up the hero", or works on above-the-fold copy for allodra.ai, sierra6ai.com, or any writing-room landing page. Make sure to use this skill whenever a headline, hero section, subheadline, or CTA button copy is being written or critiqued.
argument-hint: [brand/page + task, e.g. "allodra.ai hero rewrite"]
---

# Headline Copywriting — Hero Sections That Convert

Write headlines that name a felt pain and promise the dream outcome, then carry that promise through the subheadline into the CTA. The headline is the highest-leverage text on the page; treat it as the product of a process, not a first draft.

Read these supporting files on demand:
- `${CLAUDE_SKILL_DIR}/references/headline-formulas.md` — the full formula library (Hormozi value equation, PAS, enemy positioning, Schwartz awareness stages, Copyhackers, Harry Dry, Julian Shapiro, StoryBrand) and the 20 headline rules
- `${CLAUDE_SKILL_DIR}/references/hero-and-cta.md` — hero-section anatomy (job of each element) and CTA/click-trigger patterns with conversion evidence
- `${CLAUDE_SKILL_DIR}/references/swipe-file.md` — 38 real SaaS headlines tagged by pattern, before→after rewrites, and stealable sentence structures

## Load first — brand context

| Brand | Load | Hard rules |
|---|---|---|
| Allodra | `writing-room/docs/voice-allodra.md` | Honesty guardrail (see below); use the approved vocabulary |
| Sierra-6 | `writing-room/docs/voice-sierra6.md` (if built) | Never sell leads; veteran-operator tone |
| Other | The brand's voice doc, or ask for positioning | — |

Paths are relative to the OathDriven workspace root — Glob for `**/voice-allodra.md` if the session starts in a subfolder. The voice doc supplies the enemy, the metaphor, the approved words, and the claims that are safe to make (guardrails can change — the voice doc is always the source of truth). Never write a headline before reading it.

**Standalone use (no OathDriven workspace / this skill was shared with you):** if no voice doc exists, check `${CLAUDE_SKILL_DIR}/my-brand-voice.md`. If that's missing too, interview the user briefly before writing anything: (1) what do you sell and to whom, (2) the enemy (the tool/practice/incumbent the reader blames — never the reader), (3) the dream outcome in the customer's words, (4) proven pains — real lines from replies, reviews, or calls, (5) approved and banned vocabulary, (6) claim guardrails (what's safe to promise publicly). Save the answers to `${CLAUDE_SKILL_DIR}/my-brand-voice.md` so the user answers once; load it in place of the voice doc from then on. The "Allodra defaults" section at the bottom shows what a filled-in profile looks like.

## The core formula

```
HEADLINE  = PAIN (villain named or implied) × DREAM OUTCOME (specific, visualizable)
SUBHEAD   = the mechanism — what it is and why the promise is believable
CTA       = hand them the outcome, first person, risk killed beside the button
```

Run every candidate through the Hormozi value lens: raise the **dream outcome** and its **perceived likelihood** (proof beside the claim); cut **time delay** ("in 7 days", "instantly") and **effort/sacrifice** ("without X"). A headline that only states pain agitates; a headline that only states outcome floats. The strongest pair both: *"Stop paying a penalty for growth"* = pain (growth tax) with the outcome (penalty-free scaling) implied in the same breath.

The villain is always a tool, category, incumbent, or practice — **never the reader's own failure.**

## Workflow

Copy this checklist and tick it off:

- [ ] 1. **Load the brand voice doc.** Note the enemy, approved vocabulary, and any claim guardrails.
- [ ] 2. **Diagnose the awareness stage** of the page's traffic (table in `references/headline-formulas.md`). Homepage traffic is usually solution-aware → lead with pain + differentiated outcome. Cold-ad traffic skews problem-aware → lead harder on pain.
- [ ] 3. **Mine the pain and dream outcome in customer language.** Sources in priority order: proven hooks that already got replies (cold-email sequences, VSL hooks), actual reply/call language, the voice doc. Steal the customer's sentence; don't invent one.
- [ ] 4. **Bleed the tap — write 20+ headlines minimum** across at least 4 pattern categories (enemy/"Stop X", dream-outcome, specificity-number, metaphor, clarity). The first dozen are always predictable; gold shows up late. Use the stealable structures in the swipe file.
- [ ] 5. **Score with the five tests** (below). Shortlist the top 3.
- [ ] 6. **Assemble the full hero for the winner:** eyebrow → H1 → subhead → CTA + click trigger → proof line (element jobs in `references/hero-and-cta.md`).
- [ ] 7. **Honesty check** against the brand guardrail. A headline you can't ship is a failed headline, no matter how good.
- [ ] 8. **Deliver** in the output format below and save to `writing-room/drafts/[brand]-[slug]-draft.md` (standalone: wherever the user keeps drafts, or beside the page being edited).

## The five tests (scoring gate)

Every shortlisted headline must pass all five:

1. **Grunt test** — a stranger glancing for 3 seconds knows what you sell, how it helps, and what to do next.
2. **Visualizable** — the reader can see it ("1,000 songs in your pocket"). Abstractions evaporate.
3. **Falsifiable** — a specific claim that could be proven wrong ("30 minutes or it's free") gets believed. Vague claims get ignored.
4. **Un-copyable** — if a competitor could run the same line word-for-word, it's a category label, not a headline.
5. **One big idea** — one reader, one pain, one promise. Two ideas = half the strength of each.

Mechanics: ~6–12 words, roughly 7th-grade reading level, no hype stacking, concrete numbers over adjectives (odd/precise numbers read as counted, not invented).

## The CTA segue

The button is the actionable next step to the headline's promise — a continuation of the story, never a generic verb.

- **Call to value:** `[verb] + [the thing they actually want]`. "See the 3-year math" beats "Learn more".
- **First person converts:** "Start **my** free trial" beat "your" by +90% CTR in the canonical test. Default to first person.
- **Kill risk at the click:** microcopy beside the button — "No credit card", "Takes 30 seconds", "One-time, own it forever" (+19% signups documented for a single click trigger).
- **Match CTA weight to awareness:** most-aware → hard CTA ("Buy it once"); earlier stages → soft first CTA ("See how it works") with the hard CTA repeated lower.

Full patterns and evidence: `${CLAUDE_SKILL_DIR}/references/hero-and-cta.md`.

## Output format

Deliver exactly this shape:

```markdown
## Shortlist (from N variants)
| # | Headline | Pattern | Why it wins |
|---|---|---|---|
| 1 | ... | enemy / pain-led | ... |
| 2 | ... | dream-outcome | ... |
| 3 | ... | specificity | ... |

## Recommended hero (option 1)
**Eyebrow:** ...
**H1:** ...
**Subhead:** ...
**CTA:** [button] + [click-trigger microcopy]
**Proof line:** ...

## Why this beats the current hero
(1–3 sentences against the incumbent headline)

## Full variant list
(all 20+, grouped by pattern — the user picks differently than you'd predict)
```

## Allodra defaults (worked example)

- **Current hero (the incumbent to beat):** "Stop renting your CRM. Own it outright." — leads with the *mechanism* (CRM ownership). Weakness: "CRM" makes the reader think software category, not their own pain.
- **Target energy:** "Stop paying a penalty for growth." — leads with the *felt pain* (you're taxed for succeeding) and implies the dream outcome (scale free and clear).
- **The enemy:** the digital landlord — rent, seat creep, the growth tax. Attack the incumbent practice (renting), never the reader.
- **Approved vocabulary:** landlord · rent · growth tax · seat creep · take title · own it · allodial · digital real estate · free and clear · one-time · stop renting.
- **⚠️ Honesty guardrail (hard rule):** safe to claim **"buy it once, own the license, no monthly rent, no growth tax."** Do NOT claim "deployed to your own cloud / nobody can ever lock you out" in public copy until reseller rights are live. The honesty is the edge — never trade it for a bigger number.
- **Proven pains that already got replies** (mine these first): the growth tax / taxed for succeeding · renting vs owning · the 3-year number ($18k GHL / $43k HubSpot) · "you're a digital tenant" · "why I fired GoHighLevel".

Read `$ARGUMENTS` for the brand, page, and task. If no brand is named, ask which brand — the voice doc changes everything.
