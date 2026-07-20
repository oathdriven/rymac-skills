# rymac-aeo-blog-writer

> Writes SEO + answer-engine-optimized blog posts built to rank on Google AND get cited by AI answer engines — for anyone who wants their content quoted, not just found.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Writes posts that do three jobs at once: rank in classic search, get cited by AI answer engines (Google AI Overviews, ChatGPT, Perplexity, Gemini), and move the reader toward one action. It runs live SERP recon on the top results to find the format that wins and the gap you can exploit, writes answer-first so the AI can lift your sentence cleanly, wires in internal and external authority links, and recommends FAQ/HowTo schema. The edge over a normal SEO post is structure — being the source the AI quotes.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "write an AEO post"
- "answer-engine optimization"
- "get cited by AI Overviews"
- "rank AND get quoted"

(You can also force it with the slash command `/rymac-aeo-blog-writer`.)

## Install

Copy this entire `rymac-aeo-blog-writer` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-aeo-blog-writer/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-aeo-blog-writer\`
- **One project only:** `<your-project>/.claude/skills/rymac-aeo-blog-writer/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Write an AEO post targeting "how much does a CRM cost" so it gets quoted by AI Overviews.

Claude will run SERP recon, propose an answer-first outline, then write the post with question-H2s, tables, internal + external links, and ready-to-paste schema.

## What's inside

- `SKILL.md` — the instructions Claude loads

## Pairs well with

This is the advanced, answer-engine-optimized writer with live SERP recon and authority linking. For a quick keyword blog post without the recon and citation engineering, use the simpler `rymac-seo-writer` instead.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
