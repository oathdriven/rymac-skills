# rymac-niche-research

> Validates a niche or offer idea before you build: parallel research agents map the pain, the psychology, the competitors, and the demand, then hand you a BUILD / PIVOT / SKIP verdict with offer angles in the niche's own words.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Fans out 4 research subagents at once: verbatim pain quotes from where the niche actually complains, the psychology of why the pain persists, a mandatory competitor matrix, and demand proof including a count of how many of these businesses exist. Then it commits: BUILD, PIVOT, or SKIP, with the underserved wedge, a one-sentence USP, 2-3 offer angles priced off the competitor matrix, a pain-language bank ready for headline and sales-page work, and the honest "what would kill this" paragraph. It saves everything to a `niche-research-<slug>.md` handoff file that the copywriting skills in this pack consume instead of re-researching.

## When it fires

- "research a niche"
- "validate this offer"
- "should I build this?"
- "who else sells this?"
- "run niche research on [X]"

(Or force it with `/rymac-niche-research`.)

## Install

Copy this entire `rymac-niche-research` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-niche-research/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-niche-research\`
- **One project only:** `<your-project>/.claude/skills/rymac-niche-research/`

Restart Claude Code. Done.

## Example

> "Run niche research on mobile diesel repair. My hunch: they miss overnight emergency calls and lose the job to whoever answers."

You get the 4-agent fan-out, the verdict, the lead-pool count, the wedge, offer angles in mechanics' own words, and the handoff file for the page build.
