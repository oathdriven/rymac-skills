---
name: rymac-ctc-video-script
description: Writes bite-sized (under 10 minute) video course scripts for Ryan's CommitToClose sales course in his exact voice, using the slide-per-sentence animation format of the Allodra VSL (1-2 sentences per slide, VO reads on-screen text verbatim, pause markers for emphasis). Use when Ryan asks to "write a video script", "script video 2", "write the objections video", "course video", "sales course script", "CTC video", or wants any CommitToClose / RyMac teaching video scripted. Make sure to use this skill whenever a video script for the sales course is being written or revised. For Allodra blog posts use allodra-seo-writer instead.
argument-hint: [video number or topic, e.g. "video 1" or "objections"]
---

# CTC Video Script Writer

Write animation-ready teaching scripts for Ryan "RyMac" McKinney's CommitToClose
video sales course. Ryan records the voiceover himself, rolling slide to slide,
adding his own pauses to drive points home. The audience is builders and nerds
who ship whiz-bangs but can't sell them.

## Load these BEFORE writing (in order)

1. `${CLAUDE_SKILL_DIR}/voice.md` — Ryan's voice: spoken register, signature
   phrases, story structure, hard style rules. The script must sound like HIM.
2. `${CLAUDE_SKILL_DIR}/framework.md` — the 7-stage framework, the 3 objection
   handlers, the hidden-row close, the $/call math. All verbatim lines live
   here; use them word for word, never paraphrased.
3. `${CLAUDE_SKILL_DIR}/course-map.md` — the video roadmap, per-video beat maps,
   and the product tie-in rules (closectl, the free Skool, the Lurker kit).
4. `${CLAUDE_SKILL_DIR}/leadgen.md` — only when the video touches lead
   generation / cold email (video 3 and any lead-gen follow-ups).

If Ryan supplies lines or a story in the request, those are canon: use them
verbatim and build around them.

## The format (modeled on the Allodra Charter Fold VSL)

The produced Allodra VSL is the shape to copy: slide-per-sentence "fold" format,
centered bold type, VO reads the on-screen text verbatim, font size scales
inversely with word count. Adapt it for teaching:

- **One slide = 1-2 sentences, 4-18 words.** Hook and punch slides run short
  (4-9 words). Explanation slides can take the full two sentences.
- **Numbers get their own slide, alone, max type, with a hold.**
  "71%." "$17,892." "64 days." Silence does the selling.
- **[PAUSE] marks a scripted hold** where Ryan drives the point home. Use them
  after punch slides and revealed numbers, 3-6 per video, never more. Ryan adds
  his own pauses live, so mark only the load-bearing ones.
- **[VISUAL: ...] cues are optional, one line max**, only when the animation is
  load-bearing (a stage lighting up on the commit graph, the hidden row
  unhiding, a diff flipping red to green). The editor invents nothing else.
- **Ellipsis pulls** may span two slides ("So when they say 'let me think about
  it'..." → "...they just told you the price is the problem."). VO does not
  pause across the ellipsis.
- **Refusal/rule stacks** = one item per line on a single slide ("No scripts.
  No charisma. No 1,000 rebuttals.").
- **Reenacted dialogue is the pivot of every story.** Quote both sides, then
  land the "Boom." Every story ends with the rule stated plainly on its own
  slide.

## Pacing math (enforce, do not eyeball)

Ryan reads at ~150 words per minute, plus roughly 1.5 seconds per [PAUSE].

- **Hard ceiling: 10 minutes → never exceed 1,400 spoken words.**
- **Target: 8-9 minutes → 1,100-1,300 words**, leaving room for his live pauses.
- Overview/bridge videos can run shorter (4-6 min, 600-900 words). Short and
  dense beats long and padded, every time.
- Expect roughly 12-16 slides per minute.

Compute and print the word count, slide count, and estimated runtime in the
script header. If over budget, cut content, never compress sentences into
run-ons.

## Beat map (default shape for a teaching video)

1. **Hook** (≤20 seconds) — a receipt, a wound, or a wrong belief. Never
   "hey guys, welcome back."
2. **The stakes** — why this costs them money, in numbers.
3. **The teach** — the meat. Story-driven: setup with a date/age anchor →
   reenacted dialogue → the mechanism lands → "Boom." → the rule.
4. **The recap** — the rule(s) restated as a stack, one per line.
5. **The bridge** — tease the next video + at most ONE soft product touch
   (see course-map.md for which product goes with which video).

## Hard voice rules (full detail in voice.md — these are the non-negotiables)

- **No em dashes anywhere.** Slides are on-screen customer copy. Use periods,
  commas, colons, parentheses.
- Verbatim lines from framework.md are untouchable tokens: write around them,
  never through them.
- One version of every stat: **71% close** (never 50%), 64 days → one call,
  $750K on 6 webinars, $650 first Cutco week.
- Money is spoken in words at a close ("It's Seventy-Five-Hundred to get
  started"), digits everywhere else.
- Audience is "builders" and "nerds", never "entrepreneurs". Their product is
  a "whiz-bang".
- No hype stacking, no fake scarcity, no income promises, no "in today's
  world" openers. Give away the how; sell the compression.

## Rendering (the Remotion pipeline)

Scripts render via `OathDriven/production/ctc-videos/` (see its README).
Rules that live in the renderer but shape the writing:

- **Color grammar (kit tokens, applied per phrase, never single words):**
  blue #58A6FF = quoted speech (auto) · green #41FF7A = positive / merge /
  "Stage N:" lines (auto) · red #FF5C57 = the lie, negative, CONFLICT ·
  amber #FFB454 = commitment ONLY (brand law: the node is always amber).
  Manual emphasis lives in `scripts/emphasis/<video-id>.json` in the render
  project: sprinkle on emphasis beats (~1 in 3 slides), never every slide.
- **No orphaned words, ever** (renderer balances lines, but keep slide
  sentences shaped so they split into even lines).
- The final slide of every video is an end card: commit-graph rail animates
  in, the brand wordmark, tagline slides in; the video ends as the close
  node's merge pulse fades (no og-image morph, Ryan's call).
- "Go be dangerous." always gets the shake treatment.
- **The living rail** renders automatically: every "Stage N: name." slide
  grows the bottom commit-graph rail and sets the pulsing current node, so
  write stage announcements exactly in that form.
- **Roadmap slides**: put "roadmap" in the [VISUAL] cue to render the 9-step
  terminal roadmap beside the text ("cascade" = animate in, "step N" =
  pulsing you-are-here highlight). Use for any presentation-stage teaching.
- **Calculator slides**: [VISUAL: calc <stage>] renders the hidden-row
  profit calculator (stages: cascade → total → testclose → question →
  reveal → roi → close). Use whenever the hidden-row story is told.
- After writing a script, run the parser and hand-author the emphasis JSON.

## Output

Write the script to
`OathDriven/writing-room/drafts/ctc-course/ctc-video-[NN]-[slug]-draft.md`
(create the folder if missing). Statuses follow workspace convention:
draft → review → final.

Script file shape:

```markdown
# CTC Video [NN] — [Title]
&gt; ~[N] words · [N] slides · est. [M:SS] at 150 wpm · [N] pauses

[001] [on-screen text — VO reads this verbatim]
[002] [next slide]
      [PAUSE]
[003] [VISUAL: the commit graph lights stage 3 amber]
      [on-screen text]
...
```

## Checklist (copy and tick per script)

- [ ] Loaded voice.md + framework.md + course-map.md (+ leadgen.md if lead-gen)
- [ ] Hook lands inside 20 seconds, no throat-clearing
- [ ] Every framework line used is verbatim from framework.md
- [ ] At least one war story with reenacted dialogue and a stated rule
- [ ] Numbers isolated on their own slides with holds
- [ ] Word count ≤ 1,400, runtime computed and printed in header
- [ ] Zero em dashes (search the file for "—" before delivering)
- [ ] 3-6 [PAUSE] marks, each after a load-bearing beat
- [ ] One soft product bridge max, matched to the video per course-map.md
- [ ] Read the script aloud mentally: does it sound like Ryan talking, not copy?

`$ARGUMENTS` names the video (number or topic). If it names a video not yet in
course-map.md, propose the beat map first, get a yes, then write.
