# rymac-profit-calculator

> Builds the "run YOUR numbers" calculator for any sales page: the prospect enters their own numbers, honest cited constants do the math, and the page shows them what their leak costs — because nobody argues with their own math.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Builds an interactive on-page calculator around the one leak bleeding your prospect: response-speed decay, SaaS rent with compounding hikes, missed after-hours calls, whatever your niche's version is. The method: 2-4 inputs clamped to sane ranges with painful defaults, honest constants with named sources, a bad-news-then-good-news output (the loss IS the opportunity), and exactly one CTA after the result. Optional patterns included: shareable result permalinks for cold email, and gating a bonus asset below the never-gated number.

## When it fires

- "build a calculator"
- "profit calculator" / "loss calculator" / "ROI calculator"
- "run your numbers section"
- when a sales page needs its pain engine

(Or force it with `/rymac-profit-calculator`.)

## Install

Copy this entire `rymac-profit-calculator` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-profit-calculator/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-profit-calculator\`
- **One project only:** `<your-project>/.claude/skills/rymac-profit-calculator/`

Restart Claude Code. Done.

## Example

> "Build a calculator for my detailing-shop site. The leak: they answer lead calls same-day instead of in 5 minutes."

You get the leak formula with the cited speed-to-lead study, painful defaults, the bad-news/good-news reveal, and the single CTA.
