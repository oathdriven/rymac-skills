---
name: rymac-direct-sales-copy
description: Writes direct-response P.A.S. (Problem-Agitate-Solution) sales letters in the RyMac voice, in the Dan Kennedy direct-letter tradition, modeled on the proven Sierra-6 letter. A personal letter to one reader with self-identification pain bullets, "you're not alone" normalization, cinematic agitation, an I-was-you origin story, a named-mechanism reveal, imagine future-pacing, and a P.S. close, formatted for skimmers (bold/underline paths). Use when the user asks to "write a sales letter", "write the letter", "P.A.S. letter", "direct sales letter", "Dan Kennedy letter", "pain-agitate-solution copy", says "set up my sales letter voice profile", or needs the letter section of a sales page. Make sure to use this skill whenever long-form persuasive letter copy is being written, rewritten, or critiqued.
argument-hint: [offer/brand + audience, e.g. "closectl letter to solo devs"]
---

# RyMac Direct Sales Copy — The P.A.S. Letter

Write a direct-response sales letter as one human writing to one human: name the reader's pain better than they can, agree it sucks, show them they're not alone, tell the story of why you can fix it, reveal the system, make them imagine the outcome, and close soft. This framework has produced millions in sales. The bones never change; only the clothes change per offer.

Read these supporting files on demand (one level deep):
- `${CLAUDE_SKILL_DIR}/references/letter-anatomy.md` — the 23-beat structure + the annotated Sierra-6 specimen (the canonical letter). **Read this before drafting any letter.**
- `${CLAUDE_SKILL_DIR}/references/voice-dna.md` — the RyMac voice: formatting fingerprint (what gets bold vs underline vs italic), diction, persuasion habits, the never list, and the intake for writing as someone other than Ryan.
- `${CLAUDE_SKILL_DIR}/references/pas-framework.md` — WHY each beat works (Kennedy/Collier/Schwartz/Halbert lineage): agitation limits, the three-beat bridge, the double readership path, awareness stages, the close. Read when a draft is structurally right but not landing, or when adapting to a new market.

## The arc in one breath

```
P  headline → "Dear Fellow ___," → "sounds like you?" pain bullets → "you're not alone"
   → "You want…" empathy run → agitation scenes (a full bad day, lived not summarized)
A  → "Wake up. Rinse. Repeat." → THE PIVOT: pain agreement, no pitch ("It's aggravating
   as fire. I get it.")
S  → "I'm not [the enemy's category]" → who I am + origin story (named client, real
   dollars, their spoken quote) → credibility, humbly framed → "my focus is [you]"
   → named mechanism + outcome bullets (each kills a pain named above) → bonus
   → promise: dream outcome + timeframe → "Imagine…" ×3 (negate the pains one-for-one)
   → price anchored to an everyday purchase → soft CTA ("see if it makes sense")
   → signoff → risk killers → P.S. (one sideways metaphor + the link)
```

Full beat map with lengths and jobs: `references/letter-anatomy.md`.

## First-run setup (the voice profile)

The letter is signed by a real person, and their tokens live in `${CLAUDE_SKILL_DIR}/my-voice-profile.md`. Resolve the signer before anything else:

1. **If `my-voice-profile.md` exists** → the signer is set. Load it and skip to the workflow.
2. **If it doesn't exist and the session is in Ryan's OathDriven workspace** → the signer is Ryan; his tokens are in `references/voice-dna.md` §1–4 and the brand voice docs. No profile file needed.
3. **Otherwise (a new user, or the user says "set up my voice profile" / "set this up")** → run the 7-question intake from `references/voice-dna.md` §5 as a short interview (one question at a time, with Ryan's answer shown as the example for each). Then WRITE the answers to `${CLAUDE_SKILL_DIR}/my-voice-profile.md` under the same 7 headings, tell the user where it lives and that they can edit it anytime, and use it for every letter from then on. Never re-interview a user who already has a profile; if an answer is missing, ask only for that one.

## Workflow

Copy this checklist and tick it off:

- [ ] 1. **Read `references/letter-anatomy.md` and `references/voice-dna.md`.** Never draft from memory of the framework.
- [ ] 2. **Establish the signer** per First-run setup above (load `my-voice-profile.md`, or Ryan's tokens in the OathDriven workspace, or run the intake and save it). Never invent origin stories, client names, or dollar figures — ask.
- [ ] 3. **Mine the pain in the reader's own words.** Sources in priority order: real replies/call language, proven hooks that already converted, reviews and forums, then the niche-research skill if nothing exists. The pain bullets and agitation scenes must use vocabulary the reader actually says (their words go in scare quotes).
- [ ] 4. **Collect the raw materials** before writing a word: the enemy (a specific middleman, never the reader), 4–6 pain questions, one full bad-day sequence for the agitation scenes, the origin story (name, trade, risk, timeframe, dollar result, spoken quote), the credibility marker, the mechanism NAME, the dream outcome + honest timeframe, the price anchor, the risk killers.
- [ ] 5. **Nail the promise line.** Use the `rymac-headline-copywriting` skill's formula: `[Dream outcome] in [timeframe] without [the pain]`. This drives the letter's headline (beat 1) and the speed promise (beat 18). If that skill isn't installed, the formula plus the Hormozi value lens in `references/pas-framework.md` §7 is enough.
- [ ] 6. **Draft all 23 beats in order.** One-sentence paragraphs dominate; 3-sentence hard cap. Bullets appear exactly twice (pains in, outcomes out).
- [ ] 7. **Mark the emphasis pass.** Bold = claims/pains/promises. Underline = dream outcomes/identity lines (~6 per letter). Italics = quoted speech and identity wounds. Budget: ~2–5% of words, at most one emphasized phrase per paragraph.
- [ ] 8. **Run the quality gates** (below). Fix and re-run until all pass.
- [ ] 9. **Deliver** in the output format below. In the OathDriven workspace, save to `writing-room/drafts/[brand]-letter-draft.md`; otherwise save beside the project or where the user asks.

## Quality gates (all must pass before delivery)

1. **The skim test.** Read ONLY the headline, bold, underline, pull-quotes, and P.S., top to bottom. They must tell the complete story alone: problem → promise → proof → offer → close. If not, re-mark — don't rewrite.
2. **The pivot check.** The writer's name must not appear before the pain-agreement line, and no pitch before "I get it."
3. **The loop check.** Every system bullet and every "Imagine" line maps to a specific pain named in the bullets or agitation scenes. No new dreams at the close.
4. **The scene check.** Agitation is scenes, not summaries ("rings out to their voicemail," not "leads don't answer"). Each scene could be filmed.
5. **The proof check.** No anonymous proof. The story client has a name, a trade, a dollar figure, and a timeframe. All numbers specific and defensible.
6. **The voice check.** Read aloud: contractions, tag questions, 5th–8th grade level (Hemingway-app clean), no hype words, no corporate speak, no fake scarcity, no em dashes, no orphaned words. Full never-list: voice-dna §4.
7. **The honesty check.** Every claim survivable in public. Timeframe matches real delivery speed. The villain is real. One inflated claim next to your best proof poisons both.

## Critical rules

1. **Pain is paid in full before the pitch.** Roughly the first 40% of the letter is empathy and agitation. Amateurs jump to the solution; this letter never does.
2. **Agitate the problem, never the person.** The reader feels seen, not judged. Hopeless people don't buy.
3. **The enemy is an external middleman** profiting off the reader's work. Never the reader's own failure.
4. **The bridge is three beats and none are optional:** you're not alone → it's not your fault (disqualify the enemy) → I was there, so I built this.
5. **Verbatim signature lines are untouchable.** If the signer has locked lines (Ryan's are in `closectl/_config/voice-lines.md`), use them exactly or not at all.
6. **Soft close for call-based offers.** "See if it makes sense" — takeaway energy, never a hard close. Card-on-page offers may close harder, but the letter still ends on an invitation, not pressure.

## Output format

Deliver the letter as markdown with the formatting marked inline, plus a short header block:

```markdown
# [Brand] — Direct Sales Letter ([audience])
**Promise line:** [dream outcome] in [timeframe] without [pain]
**Enemy:** … · **Mechanism:** … · **CTA:** … · **Anchor:** …

---
[the letter, beats 1–23, with **bold**, <u>underline</u>, *italic*, and > pull-quotes marked]
---

## Skim path (the bold/underline story, extracted for review)
[the emphasized lines only, in order — proves gate 1 passed]
```

When the letter is destined for HTML, map: bold → `<strong>`, underline → `<u>`, italic → `<em>`, pull-quote → a styled quote paragraph; spoken triumph quote may take brand color + ALL CAPS.

## Companion skills (hand off, don't re-derive)

| Need | Skill |
|---|---|
| The page around the letter (hero, value stack, pricing, FAQ) | `rymac-sales-page-builder` (this letter is its written-P.A.S. engine) |
| The promise/headline formula and variants | `rymac-headline-copywriting` |
| Audience + pain research when no real language exists | `niche-research`, `researcher` |
| Turning the letter into a video script | `rymac-vsl-copywriting` |

Read `$ARGUMENTS` for the offer, brand, and audience. If the audience or offer is unclear, ask before writing — the letter is written to ONE reader, and everything depends on who that is.
