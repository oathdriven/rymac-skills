---
name: rymac-vsl-copywriting
description: Write video sales letter (VSL) scripts in the house slide-per-sentence format — one sentence per slide, on-screen text verbatim with the VO, under 6 seconds a slide, scripted holds on the lines that matter — plus "invisible VSL" organic variants for YouTube. Use when the user asks to "write a VSL", "VSL script", "video sales letter", "fold video", "homepage video script", "invisible VSL", "YouTube VSL", "slide video", or wants a script, sales letter, or transcript converted into slides. Make sure to use this skill whenever a VSL or slide-based sales video is being written, rewritten, compressed, or storyboarded for any OathDriven brand.
argument-hint: [brand + video, e.g. "allodra charter VSL, 4 min"]
---

# VSL Copywriting — Slide-Per-Sentence Sales Video Scripts

Write VSL scripts as slides, not prose: one thought per slide, the VO reads exactly what's on screen, the cut is the punctuation, and silence is the highlighter. The script is ~80% of the video's conversion — treat every slide as a unit of attention you either earn or lose.

Read these supporting files on demand:
- `${CLAUDE_SKILL_DIR}/references/vsl-beat-structures.md` — the narrative playbook: guru beat sequences (Benson 3X, Suby, Hormozi, Brunson's Epiphany Bridge), the retention-timed 8-beat template, 10 hook patterns, mechanism/enemy theory, application-funnel CTA beats, proof-without-testimonials stack, 12 failure modes
- `${CLAUDE_SKILL_DIR}/references/slide-pacing.md` — the mechanics with numbers: reading speed, words-per-slide, duration math, chunking rules, the pause/hold playbook, on-screen readability, retention pacing
- `${CLAUDE_SKILL_DIR}/references/house-models.md` — the Sierra-6 fold video decomposed (the live pacing model on sierra6ai.com), the Allodra "Tech Rent Boycott" beat map, and the all-brand guardrails master list

## Load first — brand context

| Brand | Load | Hard rules |
|---|---|---|
| Allodra | `writing-room/docs/voice-allodra.md` | Honesty guardrail on ownership claims; approved vocabulary only |
| Sierra-6 | `writing-room/docs/voice-sierra6.md` *(if built — else the de facto sources in house-models.md)* | Never sell leads; veteran-operator tone; the 3 Laws |
| RyMac | No voice doc yet — teaching voice, "Marine, two dogs, and a laptop" persona | Teach what/why, never sell hard |

Paths are relative to the OathDriven workspace root — Glob for `**/voice-*.md` if the session starts in a subfolder. Guardrails move as the business does (e.g. the own-cloud claim) — **the voice doc at write time is the source of truth.** Never write a VSL before reading it.

## The format (non-negotiable)

```
ONE SLIDE   = one complete thought, 5–15 words (hard cap ~20; split at the clause break past 15)
ON-SCREEN   = verbatim what the VO says (or an exact fragment) — never paraphrase; mismatch breaks the trance
DURATION    = words ÷ 2.5 + hold seconds · floor 1s · cap 6s (only scripted holds run longer, never past 8s)
THE CUT     = the punctuation. End mid-thought slides with "..." or ":" to pull the eye forward
EMPHASIS    = 1–2 highlighted words per slide, max. A word alone on a slide shouts loudest
SILENCE     = the highlighter. Script every hold explicitly — [HOLD 2s] / [BEAT] — editors won't invent pauses
```

Why text-only works: when the sentence is the only visual, reading + hearing the same words beats hearing alone (Moreno & Mayer 2002), and the format forces linear consumption — nobody skims to the price. Full numbers and evidence: `${CLAUDE_SKILL_DIR}/references/slide-pacing.md`.

Budget math before writing: 140–160 spoken wpm → a 4-min VSL is ~560–640 words and ~45–60 slides. Write to the budget, not past it.

## The narrative spine (house default, 2–6 min application VSL)

Timings scale proportionally to target runtime. Retention stakes per beat in `references/vsl-beat-structures.md`.

| Beat | ~% of runtime | Job | Rule |
|---|---|---|---|
| 1. Hook | 0–10% | Pattern interrupt + callout; open the master loop | Payoff promised by 0:15. Never open with a name or greeting |
| 2. Problem | 10–25% | Name the pain in the viewer's words | Problem-first beats claim-first on cold traffic |
| 3. Agitate | 25–40% | Stack the cost; twist the knife | ≤90 seconds, ever — past that it reads as manipulation |
| 4. Credibility | mid-problem | Scar tissue: "listen to me because I got burned too" | Drop it inside the problem, not up front |
| 5. Mechanism reveal | 40–55% | Name the hidden enemy (why everything else failed), then name YOUR system | Both get proper nouns. Enemy = tool/practice/incumbent, never the viewer |
| 6. Solution + offer | 55–75% | What they get, stacked; the vehicle for the mechanism | Full value stack BEFORE any price |
| 7. Proof | 65–80% | Receipts, math, demonstration, founder story | Specificity is the proof — "11 estimates last Tuesday" beats "tons of leads" |
| 8. Price anchor + price | 75–85% | Anchor high (agency $/mo, old price), then land the real number | HOLD on the number, alone on its slide |
| 9. CTA | 85–100% | Apply/qualify frame + risk reversal + real scarcity | See CTA rules below. Repeat: soft CTA seeded mid-video, hard CTA at close |

## Application-funnel CTA rules

These VSLs sell a *call*, not a checkout. The CTA beat must:
1. **Frame it as qualification** — "apply to see if you qualify"; the call is a diagnosis, not a pitch.
2. **Take it away** — "this isn't for everyone"; say who it's for AND who it's not for.
3. **Pre-frame the next step literally** — "click the button below this video, answer a few questions, pick a time." Next-step-specific CTAs beat generic ones.
4. **Use only real scarcity** — cohort caps, builds-per-month, founding-member counts. No countdown timers; fake urgency destroys the qualification frame.
5. **Kill risk in plain words** — "not a pushy call, no contracts, if it's not a fit I'll tell you."

## Line-level rules

- Flesch-Kincaid grade 5–7. Short sentences; vary rhythm — a 3-word punch after two longer lines.
- Start lines with And / But / So / Because / Now / Look / Here's the thing — speech glue, momentum.
- One master open loop from hook to close; resolve minor loops within ~3 slides or frustration wins.
- Concrete pictures over abstractions: not "get more leads" — "wake up to a booked calendar."
- Lists fire as slide runs: one item per slide, 2–3s each, momentum by rhythm.
- Read the whole script aloud before delivering. If a line makes you cringe spoken, rewrite it.

## Invisible VSL (YouTube organic variant)

A content video that carries the VSL's persuasion spine disguised as teaching — top-of-funnel for the sales page. Same slide format, different wrapper:

- **Hook is content-native, not ad-native:** promise a lesson or reveal ("what renting your CRM actually costs — the real math"), never an offer.
- **Teach what and why, never how** (Brunson) — the full "how" is the reason the sales page and call exist.
- **The lesson IS beats 2–5** of the spine (problem → agitate → mechanism/enemy) played straight as education. The viewer should feel smarter, not sold.
- **One soft CTA, at the end** — "if you want the math on your own numbers, the calculator's linked below" energy. Sending them to a tool/lead magnet (analyzer, roadmap) converts better than sending them to a pitch.
- **Congruence rule:** every invisible VSL is a slice of the one message (own your stack / digital landlord / growth tax). Title, thumbnail, and first slide must agree — a bait gap kills retention and trust.
- Runtime 3–8 min; hook rules and pacing identical to the sales VSL.

## Workflow

Copy this checklist and tick it off:

- [ ] 1. **Load the brand voice doc** (or de facto sources). Note enemy, vocabulary, claim guardrails.
- [ ] 2. **Fix the spec:** sales VSL or invisible VSL? Target runtime? Funnel CTA? → word + slide budget (140–160 wpm, ~12–15 slides/min).
- [ ] 3. **Mine proven language first:** existing VSL scripts, hooks that got replies, call/reply language, the copy bank. Steal the customer's sentence.
- [ ] 4. **Write 5+ hooks** across patterns (problem-first, callout question, contrarian, receipt, stakes) before picking one — see hook library in `references/vsl-beat-structures.md`.
- [ ] 5. **Draft the spine as beats first** (one line per beat), then expand each beat into slides.
- [ ] 6. **Chunk into slides** per the format block; script every [HOLD] and [BEAT]; end mid-thought slides with "..." .
- [ ] 7. **Run the gate** (below). Fix before delivering.
- [ ] 8. **Honesty check** against the voice-doc guardrail — only claim what's deliverable today.
- [ ] 9. **Deliver** in the output format and save to `writing-room/drafts/[brand]-vsl-[slug]-draft.md`.

## The gate (every script must pass)

1. **0:15 test** — by second 15 the viewer knows the pain, the promise, and why to keep watching. No intros.
2. **Named mechanism** — a hidden enemy that absolves the viewer, and a proper-noun system that attacks it.
3. **Congruent CTA** — qualification frame, real scarcity only, next step stated literally.
4. **Pacing math validates** — total words ÷ runtime = 140–160 wpm; no slide over 6s except scripted holds; slide count ≈ 12–15/min.
5. **Honesty + read-aloud** — every claim shippable today per the voice doc; the whole script survives being spoken.

## Output format

Deliver exactly this shape:

```markdown
# [Brand] VSL — [working title]
**Spec:** [sales VSL | invisible VSL] · target [X:XX] · [N] words ([N] wpm) · [N] slides · CTA: [the ask]
**Hook options considered:** (the 5+, winner marked)

| # | ON-SCREEN TEXT (verbatim) | VO | DUR | NOTES |
|---|---------------------------|----|-----|-------|
| 001 | ... | (same, or exact fragment) | 3.0s | highlight "growth tax" · [BEAT] after |

**Beat map:** slide ranges per beat (hook 001–004, problem 005–011, ...)
**Guardrail check:** (claims audited, pass/fail per claim)
```

DUR sums must equal the target runtime. NOTES carries highlights, holds, pattern interrupts, and production flags only — visual/color specs live in the design doc, not the script.

## House models

The pacing model is the live Sierra-6 fold video (sierra6ai.com): 19 slides, one thought each, red-highlight emphasis, ellipsis cliffhangers, the CTA split across two slides for a hard pause. The Allodra "Tech Rent Boycott" script is the current long-form build. Both are decomposed — beat by beat, with the 5:1 transcript-to-slide compression pattern — in `${CLAUDE_SKILL_DIR}/references/house-models.md`. Match their register before inventing a new one.

Read `$ARGUMENTS` for the brand, video, and target length. If no brand is named, ask which brand — the voice doc changes everything.
