# rymac-seo-writer

> Writes keyword-optimized blog posts for any business or niche — researches the keyword, writes the full article, and formats it ready to publish.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Writes real blog posts that rank, not keyword-stuffed filler. It researches what people in your niche actually search for, presents keyword options with intent and competition, drafts an outline for your approval, then writes an 800–1,500 word article with proper structure, a meta title and description, internal-link suggestions, and image alt-text notes. It writes like a knowledgeable friend at a grade 3–5 reading level and skips the AI-slop openers.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "write a blog post"
- "I need content for my client's site"
- "help me rank for [keyword]"
- "SEO article"

(You can also force it with the slash command `/rymac-seo-writer`.)

## Install

Copy this entire `rymac-seo-writer` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-seo-writer/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-seo-writer\`
- **One project only:** `<your-project>/.claude/skills/rymac-seo-writer/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Write a blog post for an Austin car detailing shop targeting homeowners.

Claude will research keywords, present options, build an outline for approval, then write the full publish-ready article with meta tags.

## What's inside

- `SKILL.md` — the instructions Claude loads

## Pairs well with

This is the simple keyword-blog writer. For posts built to also get **cited by AI answer engines** (Google AI Overviews, ChatGPT, Perplexity) with live SERP recon and authority linking, use the advanced `rymac-aeo-blog-writer` instead.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
