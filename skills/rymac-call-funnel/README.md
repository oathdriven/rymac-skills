# rymac-call-funnel

> Wires a site to convert visitors into scheduled calls: one AI persona across chat and voice, emergency keywords that ping a live human, and every channel booking against one calendar truth.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Designs and builds the call-conversion plumbing as four separable mechanisms instead of one naive emergency flag: escalation keywords that silence the AI and ping the on-call human, live phone transfer with ring timeout and text-back, structured callback capture that creates follow-up tasks, and booking tools against one shared calendar engine so chat, voice, and the booking page never disagree on availability. Includes explicit after-hours configuration, the spot where most service businesses leak money.

## When it fires

- "wire up the call funnel"
- "set up the voice agent"
- "convert traffic into scheduled calls"
- "handle after-hours calls"

(Or force it with `/rymac-call-funnel`.)

## Install

Copy this entire `rymac-call-funnel` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-call-funnel/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-call-funnel\`
- **One project only:** `<your-project>/.claude/skills/rymac-call-funnel/`

Restart Claude Code. Done.

## Example

> "Wire the call funnel for a mobile diesel repair site. Emergencies (breakdown, roadside) should ring the on-call tech; everything else books a morning slot."

You get the emergency vocabulary, the four mechanisms, the after-hours config, and the test checklist for all four paths.
