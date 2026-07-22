# rymac-exit-pop

> Builds the exit-intent popup that catches leaving visitors with a free asset the page never promised — desktop mouse-leave plus the mobile fast-scroll-up trigger, with proven timing constants.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Builds the full exit pop: the mini-sales-page card (pattern-interrupt eyebrow, asset headline, curiosity bullets or thumbnail, one email input, one CTA, success state that keeps them on the page), the trigger logic with battle-tested constants (arm delay, desktop mouse-out test, the mobile scroll-up-near-top test most exit pops miss), and lead capture with exit-pop attribution so these leads are always distinguishable. Enforces the one law: never offer what the page already promises.

## When it fires

- "add an exit pop"
- "build an exit popup"
- "exit intent"
- "catch people leaving the page"

(Or force it with `/rymac-exit-pop`.)

## Install

Copy this entire `rymac-exit-pop` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-exit-pop/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-exit-pop\`
- **One project only:** `<your-project>/.claude/skills/rymac-exit-pop/`

Restart Claude Code. Done.

## Example

> "Add an exit pop to my landing page. The page sells my $500 audit; I have a free checklist PDF I never mention on the page."

Perfect setup: the checklist is unseen, so it qualifies as the pop offer. You get the card, both triggers, and the capture wiring.
