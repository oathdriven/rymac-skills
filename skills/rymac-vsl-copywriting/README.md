# rymac-vsl-copywriting

> Writes video sales letter scripts in the house slide-per-sentence format — one thought per slide, on-screen text read verbatim — for anyone scripting a sales video or homepage fold video.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Writes VSL scripts as slides instead of prose: one sentence per slide, the voiceover reads exactly what's on screen, the cut is the punctuation, and every pause is scripted. It works the full narrative spine (hook → problem → agitate → mechanism reveal → offer → proof → price → CTA), enforces pacing math so the runtime lands where you want it, and can also produce "invisible VSL" organic variants disguised as teaching for YouTube. You get a slide-by-slide table with verbatim on-screen text, durations, holds, and a beat map.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "write a VSL"
- "video sales letter"
- "homepage video script"
- "invisible VSL" / "YouTube VSL"

(You can also force it with the slash command `/rymac-vsl-copywriting`.)

## Install

Copy this entire `rymac-vsl-copywriting` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-vsl-copywriting/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-vsl-copywriting\`
- **One project only:** `<your-project>/.claude/skills/rymac-vsl-copywriting/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Write a 4-minute VSL for my lead-gen offer that sells a booked call.

Claude will draft the hook options, build the beat spine, and hand back a slide-by-slide script with verbatim on-screen text, durations, and scripted holds.

## What's inside

- `SKILL.md` — the instructions Claude loads
- `references/vsl-beat-structures.md` — the narrative playbook: guru beat sequences, the 8-beat template, 10 hook patterns, mechanism/enemy theory, 12 failure modes
- `references/slide-pacing.md` — the mechanics with numbers: reading speed, words-per-slide, duration math, the pause/hold playbook
- `references/house-models.md` — the Sierra-6 fold video decomposed, the Allodra beat map, and the all-brand guardrails

## Pairs well with

`rymac-sales-page-builder` hands off to this skill when a page needs a hero video, and `rymac-direct-sales-copy` uses it to turn a finished P.A.S. letter into a slide script.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
