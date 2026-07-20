# rymac-direct-sales-copy

> Writes direct-response P.A.S. sales letters in the RyMac voice — a personal letter to one reader in the Dan Kennedy tradition — for anyone who needs long-form persuasive letter copy.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Writes a Problem-Agitate-Solution sales letter as one human writing to one human: self-identification pain bullets, "you're not alone" normalization, cinematic agitation played as scenes, an I-was-you origin story, a named-mechanism reveal, "imagine" future-pacing, and a soft P.S. close — formatted for skimmers with a deliberate bold/underline path. On first run it interviews you to capture your voice, story, and offer, saves it to a profile, and reuses it for every letter after. It runs seven quality gates (including a skim test) before showing you the letter.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "write a sales letter"
- "P.A.S. letter" / "pain-agitate-solution copy"
- "Dan Kennedy letter"
- "set up my sales letter voice profile"

(You can also force it with the slash command `/rymac-direct-sales-copy`.)

## Install

Copy this entire `rymac-direct-sales-copy` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-direct-sales-copy/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-direct-sales-copy\`
- **One project only:** `<your-project>/.claude/skills/rymac-direct-sales-copy/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Write a sales letter for my done-for-you bookkeeping service to overwhelmed solo contractors.

Claude will mine the reader's pain language, draft all 23 beats in your voice, mark the emphasis path, and run the quality gates before handing back the letter and its skim path.

## What's inside

- `SKILL.md` — the instructions Claude loads
- `references/letter-anatomy.md` — the 23-beat structure and a fully annotated real letter specimen
- `references/pas-framework.md` — why each beat works (Kennedy / Collier / Schwartz / Halbert lineage)
- `references/voice-dna.md` — the RyMac voice, the formatting fingerprint, and the first-run setup interview

## Pairs well with

Uses `rymac-headline-copywriting` for the promise line, and can hand off to `rymac-vsl-copywriting` to turn the finished letter into a video script. It is the written-P.A.S. engine for `rymac-sales-page-builder`.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
