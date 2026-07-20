# rymac-sales-page-builder

> Builds high-converting sales and landing pages with one repeatable RyMac funnel skeleton — for anyone building, rewriting, or critiquing a marketing or sales page.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Builds a sales page from one repeatable skeleton: hero → P.A.S. "engine" (a sales letter, a calculator, or a free demo) → mechanism → value stack → proof → pricing → FAQ → final CTA. The skeleton never changes; only the clothes change per offer. It sizes the page to your ask (book a call vs. gated deal vs. card-on-page), builds in the order that actually ships (headline first, structure before copy, never top-to-bottom), and orchestrates the right companion skill at each step so you're never guessing. Three live pages are mapped onto the exact same bones as proof.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "build a landing page" / "write a sales page"
- "build a funnel"
- "high-converting page" / "hero section"
- "VSL page"

(You can also force it with the slash command `/rymac-sales-page-builder`.)

## Install

Copy this entire `rymac-sales-page-builder` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-sales-page-builder/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-sales-page-builder\`
- **One project only:** `<your-project>/.claude/skills/rymac-sales-page-builder/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Build a sales page for my $49/mo app — the ask is buy on the page.

Claude will work the spine, nail the headline, build the hero and P.A.S. engine, then lay out the rest of the skeleton with placeholder copy before the final copy sweep.

## What's inside

- `SKILL.md` — the instructions Claude loads
- `references/section-playbook.md` — the job, copy anatomy, and a template for every section (hero through final CTA)
- `references/conversion-principles.md` — the page-level rules (value equation, one villain, the refrain, risk reversal, CTA patterns)
- `references/case-studies.md` — three live pages mapped onto this exact skeleton, same bones different clothes

## Pairs well with

This is the orchestrator. It hands off to `rymac-headline-copywriting` (the headline step), `rymac-paid-traffic-landing-page` (fold and hero rules), `rymac-direct-sales-copy` (the written-letter P.A.S. engine), and `rymac-vsl-copywriting` (a hero video). It can also call the optional external skills `niche-research` and `ui-ux-pro-max` if you have them — but the pack works without them, since the core principles are inlined in `conversion-principles.md`.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
