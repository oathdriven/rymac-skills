# rymac-ctc-video-script

> Writes bite-sized teaching-video scripts for the CommitToClose sales course in RyMac's exact voice, using the slide-per-sentence animation format — for scripting short course videos.

A drop-in [Claude Code](https://docs.claude.com/en/docs/claude-code) skill from the **[RyMac Skills](../../README.md)** pack.

## What it does

Writes animation-ready teaching scripts (under 10 minutes) for the CommitToClose video course in Ryan "RyMac" McKinney's spoken voice. It uses the slide-per-sentence format — one to two sentences per slide, voiceover reads the on-screen text verbatim, numbers get their own slide with a hold, and pause markers flag the load-bearing beats. It enforces the pacing math (word count, slide count, runtime), keeps verbatim framework lines untouched, and outputs a render-ready script for the Remotion pipeline. This one is tuned to Ryan's course and voice specifically.

## When it fires

Ask naturally and Claude loads it automatically. It triggers on things like:

- "write a video script"
- "script video 2" / "write the objections video"
- "sales course script"
- "CTC video"

(You can also force it with the slash command `/rymac-ctc-video-script`.)

## Install

Copy this entire `rymac-ctc-video-script` folder into your Claude Code skills directory:

- **Global** (available in every project) — recommended:
  - macOS / Linux: `~/.claude/skills/rymac-ctc-video-script/`
  - Windows: `C:\Users\<you>\.claude\skills\rymac-ctc-video-script\`
- **One project only:** `<your-project>/.claude/skills/rymac-ctc-video-script/`

Then restart Claude Code (or start a new session). Confirm it shows up in your skills list. That's it — no config, no dependencies.

## Try it

> **You:** Script the objections video for the CommitToClose course.

Claude will propose the beat map, then write the slide-by-slide script with pauses, isolated numbers, a war story, and the runtime printed in the header.

## What's inside

- `SKILL.md` — the instructions Claude loads
- `voice.md` — Ryan's spoken register, signature phrases, story structure, and hard style rules
- `framework.md` — the 7-stage framework, objection handlers, the hidden-row close, and all verbatim lines
- `course-map.md` — the video roadmap, per-video beat maps, and product tie-in rules
- `leadgen.md` — lead-generation / cold-email material for the videos that touch it

## Pairs well with

Works standalone (purpose-built for the CommitToClose course). For general slide-based sales videos, use `rymac-vsl-copywriting`.

---

Built by **RyMac**. Free to use and share. More at [theonlyrymac.com](https://theonlyrymac.com).
