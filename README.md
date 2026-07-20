# RyMac Skills

**A pack of drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skills for marketers, closers, agency owners, and creators.**

These are the actual skills I (RyMac) built to run my businesses — writing sales
pages, VSLs, headlines, direct-response letters, SEO/AEO blog posts, video
scripts, and auditing the sites I ship. I use them every day. Now they're yours.

Grab **one** skill (just the sales-letter writer, say) or grab the **whole pack**.
Each one is plug-and-play: copy the folder into Claude Code, restart, and ask.
No config, no API keys, no dependencies.

---

## What's a "skill"?

A Claude Code skill is a folder with a `SKILL.md` file that teaches Claude a
specific job — the exact process, rules, and taste I use. Once it's installed,
Claude loads it automatically when your request matches, so you get *my* method
instead of generic output. [More on skills →](https://docs.claude.com/en/docs/claude-code/skills)

You need [Claude Code](https://docs.claude.com/en/docs/claude-code) installed.
That's the only requirement.

---

## The skills

Every skill lives in its own folder under [`skills/`](./skills), and each has its
own README with triggers and an example.

### ✍️ Copywriting & sales pages
| Skill | What it does |
|---|---|
| [rymac-sales-page-builder](./skills/rymac-sales-page-builder) | Builds a full high-converting sales page / funnel — headline first, then a pain-agitate-solution engine, mechanism, value stack, proof, pricing, FAQ, CTA. **Orchestrates the copy skills below.** |
| [rymac-headline-copywriting](./skills/rymac-headline-copywriting) | Headlines, hero sections, and CTAs using a pain + dream-outcome formula, awareness-stage diagnosis, and a SaaS swipe file. |
| [rymac-direct-sales-copy](./skills/rymac-direct-sales-copy) | Direct-response P.A.S. (Problem–Agitate–Solution) sales letters in the Dan Kennedy tradition — a personal letter to one reader. |
| [rymac-paid-traffic-landing-page](./skills/rymac-paid-traffic-landing-page) | Single-screen, one-decision landing pages for paid ad traffic (Meta/Google/YouTube) — message-matched to the ad, one CTA, nothing that leaks. |

### 🎬 Video scripts
| Skill | What it does |
|---|---|
| [rymac-vsl-copywriting](./skills/rymac-vsl-copywriting) | Video sales letter (VSL) scripts in a slide-per-sentence format, plus "invisible VSL" organic variants for YouTube. |
| [rymac-ctc-video-script](./skills/rymac-ctc-video-script) | Bite-sized teaching / course video scripts in the same slide-per-sentence animation format (VO reads the on-screen text verbatim). |

### 📈 SEO & content
| Skill | What it does |
|---|---|
| [rymac-seo-writer](./skills/rymac-seo-writer) | Quick keyword-optimized blog posts for any business or niche — research a keyword, write the article, format it to publish. |
| [rymac-aeo-blog-writer](./skills/rymac-aeo-blog-writer) | The pro version: SEO **+ AEO** posts built to rank *and* get cited by AI answer engines (Google AI Overviews, ChatGPT, Perplexity). Runs live SERP recon, writes answer-first. |

### 🔧 Build quality
| Skill | What it does |
|---|---|
| [rymac-code-audit](./skills/rymac-code-audit) | Multi-lens audit of a web build — bugs, performance / Core Web Vitals, technical SEO / crawlability, and mobile responsiveness — as a severity-ranked report with `file:line` locations and concrete fixes. |

---

## Install

### Option A — grab one skill

1. Download or copy the single skill folder you want (e.g. `skills/rymac-direct-sales-copy`).
2. Drop it into your Claude Code skills directory:
   - **Global** (every project) — recommended: `~/.claude/skills/`
     _(Windows: `C:\Users\<you>\.claude\skills\`)_
   - **One project only:** `<your-project>/.claude/skills/`
3. Restart Claude Code. Ask for what the skill does — it loads automatically.

### Option B — grab the whole pack

Clone the repo and copy every skill into your global skills directory:

```bash
git clone https://github.com/oathdriven/rymac-skills.git
cp -r rymac-skills/skills/* ~/.claude/skills/
```

**Windows (PowerShell):**
```powershell
git clone https://github.com/oathdriven/rymac-skills.git
Copy-Item rymac-skills\skills\* "$env:USERPROFILE\.claude\skills\" -Recurse
```

Restart Claude Code and check your skills list — all nine should be there.

> **Global vs. project scope:** global (`~/.claude/skills/`) makes a skill
> available in every project on your machine. Project scope
> (`<project>/.claude/skills/`) limits it to that one repo. For skills like these
> — general craft you'll want everywhere — global is the right call.

See [INSTALL.md](./INSTALL.md) for the full walkthrough and troubleshooting.

---

## How to use them

Once installed, you don't "call" a skill — you just ask. Say _"write me a sales
letter for my roofing business"_ and `rymac-direct-sales-copy` fires on its own.
Each skill's README lists the phrases that trigger it. You can also force one
with its slash command, e.g. `/rymac-headline-copywriting`.

---

## License

[MIT](./LICENSE) — free to use, modify, and share, personally or commercially.
An attribution back to [theonlyrymac.com](https://theonlyrymac.com) is
appreciated but not required.

## Connect

Built by **RyMac**. If these help you close deals or ship faster, I'd love to
hear about it. Everything I do lives at **[theonlyrymac.com](https://theonlyrymac.com)** — start there.

- ▶️ **YouTube** — [@RyMacHQ](https://www.youtube.com/channel/UCCvs0428gbdbXHjKSV6-v5Q)
- 🎓 **Skool (CommitToClose)** — [skool.com/commit-to-close](https://skool.com/commit-to-close)
- 💼 **LinkedIn** — [in/theonlyrymac](https://www.linkedin.com/in/theonlyrymac/)
- 𝕏 **X / Twitter** — [@theonlyrymac](https://x.com/theonlyrymac)
- 🔗 **Everything else** — [theonlyrymac.com](https://theonlyrymac.com)
