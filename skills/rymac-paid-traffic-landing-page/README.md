# rymac-paid-traffic-landing-page

> Researches a niche's pains and builds a single-screen, one-decision landing page for paid ad traffic — for anyone sending Meta, Google, or YouTube clicks to a page that has to convert.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Builds a landing page whose only job is turning one ad click into one action. It mines the niche for real pain and desire language, diagnoses awareness and market sophistication, writes the copy headline-first (message-matched to your ad), and fills a single-screen HTML template with one CTA and one true trust element — nothing else. It runs a conversion gate on every line and hands back the page plus a copy doc with A/B alternates so your ads can reuse the same language.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "make a landing page for ads"
- "build a page for this campaign"
- "squeeze page" / "opt-in page"
- "lead capture page"

(You can also force it with the slash command `/rymac-paid-traffic-landing-page`.)

## Install

Copy this entire `rymac-paid-traffic-landing-page` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-paid-traffic-landing-page/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-paid-traffic-landing-page\`
- **One project only:** `<your-project>/.claude/skills/rymac-paid-traffic-landing-page/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Build a lead-capture page for HVAC owners running Facebook ads — the goal is to book a call.

Claude will mine the niche, write the headline first, fill the single-screen template, run the conversion gate, and hand back the HTML plus a copy doc with A/B alternates.

## What's inside

- `SKILL.md` — the instructions Claude loads
- `references/niche-research.md` — 12 intake questions, the 20-minute pain-mining sprint, sophistication stages, pain→copy mapping
- `references/headlines.md` — awareness levels, 13 rules, 16 formulas, subheadline formulas, message match
- `references/page-structure.md` — structure rules with conversion data, single-screen anatomy, CTA/trust rankings, mobile rules
- `assets/page-template.html` — the single-screen HTML shell with tokens to fill

## Pairs well with

`rymac-sales-page-builder` calls this skill for its fold and hero rules. For multi-section marketing websites, reach for `build-premium-website` or `website-builder` instead of this one.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
