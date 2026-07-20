# rymac-code-audit

> Runs a thorough, multi-lens audit of a web build — bugs, site speed, technical SEO, and mobile responsiveness — and returns a severity-ranked report with file:line locations and fixes.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Audits a web build across four independent lenses — correctness (bugs now and future-error risks), performance (Core Web Vitals, bundle, images), technical SEO (crawlability, indexing, metadata), and responsive/mobile — then returns one severity-ranked report. It runs the deterministic tools first (ESLint, tsc, Lighthouse, bundle analyzers), verifies every high-severity finding against the real code to drop false positives, and gives you a scorecard plus concrete file:line fixes. It is read-only — it reports, it never edits your code. Works on React/Vite, Next.js, and static HTML sites.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "audit this build" / "run a code audit"
- "find bugs before launch"
- "why is my site slow" / "why isn't my site getting indexed"
- "why does my site break on mobile"

(You can also force it with the slash command `/rymac-code-audit`.)

## Install

Copy this entire `rymac-code-audit` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-code-audit/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-code-audit\`
- **One project only:** `<your-project>/.claude/skills/rymac-code-audit/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Audit this build before I launch — check for bugs, speed, SEO, and mobile.

Claude will detect the stack, sweep all four lenses, verify the findings against the real code, and hand back a severity-ranked report with a scorecard and fixes.

## What's inside

- `SKILL.md` — the instructions Claude loads
- `checks-correctness.md` — bug and future-error checklist (JS/TS, React, effect cleanup, error handling, security basics)
- `checks-performance.md` — site speed and Core Web Vitals checklist (LCP/INP/CLS, bundle, images, fonts, caching)
- `checks-seo.md` — crawlability and technical-SEO checklist (rendering, robots/noindex, sitemaps, canonical, metadata)
- `checks-mobile.md` — responsive/mobile checklist (viewport, overflow, tap targets, hover-only UI, 100vh, breakpoints)

## Pairs well with

Works standalone. Natural fit as a pre-launch gate on pages built with `rymac-sales-page-builder` or `rymac-paid-traffic-landing-page`.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
