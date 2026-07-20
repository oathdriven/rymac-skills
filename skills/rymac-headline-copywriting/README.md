# rymac-headline-copywriting

> Writes and rewrites landing-page headlines, hero sections, and CTAs that name a real pain and promise the dream outcome — for anyone selling something above the fold.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Turns your above-the-fold copy into a process instead of a guess. It diagnoses the awareness stage of your traffic, mines pain and dream-outcome language in your customer's own words, bleeds out 20+ headline candidates across several patterns, then scores them against five hard tests and assembles the full hero — eyebrow, H1, subhead, CTA, and click trigger. You get a scored shortlist plus the full variant list, because people pick differently than you'd predict.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "write a headline"
- "rewrite the hero"
- "give me headline options"
- "punch up the hero"

(You can also force it with the slash command `/rymac-headline-copywriting`.)

## Install

Copy this entire `rymac-headline-copywriting` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-headline-copywriting/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-headline-copywriting\`
- **One project only:** `<your-project>/.claude/skills/rymac-headline-copywriting/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Rewrite the hero for my HVAC booking page — the current one is just "The best HVAC software."

Claude will mine the pain, generate 20+ candidates, score the top three, and hand back a full assembled hero with CTA and proof line.

## What's inside

- `SKILL.md` — the instructions Claude loads
- `references/headline-formulas.md` — the full formula library (Hormozi, PAS, Schwartz awareness stages, Harry Dry, StoryBrand) and the 20 headline rules
- `references/hero-and-cta.md` — hero-section anatomy and CTA/click-trigger patterns with conversion evidence
- `references/swipe-file.md` — 38 real SaaS headlines tagged by pattern, plus before→after rewrites

## Pairs well with

`rymac-sales-page-builder` orchestrates this skill as its headline step, and `rymac-direct-sales-copy` calls its promise-line formula for the letter's headline. It also feeds the hero for `rymac-paid-traffic-landing-page`.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
