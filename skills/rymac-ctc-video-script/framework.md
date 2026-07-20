# The CommitToClose Framework — Canonical Source (all lines verbatim)

Lines in quotes are Ryan's verbatim. They are untouchable tokens: use them
word for word, never paraphrased. Fill `{NAME}` with the prospect's name and
`{DATE1YR}` with today's date plus one year when a script needs them live.

## Contents
- The doctrine
- The state machine (why it beats scripts)
- The 7 stages (0-6), verbatim lines and transitions
- The 3 objection handlers
- The hidden-row profit calculator (the 64-day close replay)
- The $/call math (revenue per conversation)
- Receipts (the proof stack)
- closectl: the framework as software
- Vocabulary

## The doctrine

- "Never tell them anything you can get them to say themselves. They won't
  believe what you say. They will believe everything they say."
- "Sales is a state machine, not a script."
- "Every stage is insurance for a later stage." Skip one and you pay for every
  objection at full price, later, when the truth is expensive.
- "All objections are lies. It's always about the price. Get to the truth."
- "You need three handlers, not a thousand rebuttals."
- "Close rate is a vanity metric." The metric is revenue per conversation.
- "You don't need a script. You need to know where you are in your framework."
- "Sales should be a pleasurable experience for the buyer."
- Always end in a question. Never end in a sentence.
- The most important word in the English language is someone's name.

## The state machine (the git metaphor, load-bearing)

It is a 7-state machine indexed from zero (the hero says "6-stage" because
arrays start at zero and so does selling). Each stage = a commit on the main
lane. Objections = diffs (their lie in red, your handler in green). The close
= a merge. Skipping stage 3 = a merge conflict:

```
CONFLICT (content): objection.md
Automatic close failed; fix conflicts at full price.
hint: stage 3 was never committed. every objection you meet
hint: from here on, you meet without a spade in your pocket.
```

Scripts are "if they say this, you say that" crap: they collapse the moment
the prospect goes off-page. A state machine only needs you to know what state
you are in and what transition earns the next one.

## The 7 stages

```
stage-0  lurk        a00000   # recon before contact
stage-1  rapport     a00001   # find common ground, then land the frame
stage-2  diagnosis   d1a605   # the frame licensed these questions. use them.
stage-3  COMMITMENT  c03317   # this stage is the brand (amber)
stage-4  present     a00004   # never demo the tech
stage-5  test-close  a00005   # surface the truth before the price
stage-6  close       71c05e   # then shut up
branch:  hotfix/objections    # only if needed
```

### Stage 0 — lurk
Fifteen minutes of public recon before every call, distilled to one page.
Weave one or two facts in naturally; never recite them. "Nobody trusts a
stranger who read their file out loud. But everybody remembers the one caller
who did their homework." Say their name in the first 30 seconds. Productized
as The Lurker (the free kit at committoclose.com). Doctrine: "Weave, never
recite." Transition: rapport built on something real.

### Stage 1 — rapport → help statement → the Business Doctor frame
1-2 minutes of common ground. No weather talk. Opener: "Sooo, Claude, where
are ya' at in the world?" and whatever they answer, common-ground it ("San
Diego? Nice, I was in the Marines there").

The help statement comes FIRST and ends in a question:
"I help [who] [get the outcome] using my [whiz-bang] so they can [what they'd
rather be doing]. Is this something you need help with?"

Then the frame lands: "Thanks for taking the call with me today. I want you
to think of me as your business doctor. I am going to ask you some questions
so I can diagnose what's going on and prescribe what you need. Just like a
doctor, if I can't help you, I will refer you to a specialist. Does that make
sense?" IT HAS TO END IN A YES. The frame licenses the intimate business
questions of stage 2, "just like a doctor would."

### Stage 2 — diagnosis
"A doctor does not prescribe before examining you." Up to 10 questions, 15
minutes or under ("we're not interviewing"). The doctor mapping:
- "What brought you in today?"
- "What did you hope to get out of this call today?"
- "Does it hurt if I touch here?" (are you happy with your X results?)
- "How long have you had this problem?"
- "What have you tried to get this fixed?"
- Decision-maker check: "Do you have a business partner or anyone else that
  should weigh in on this call?" (Don't present without every decision-maker.)
- The magic wand future pace: "I just waved a magic wand. It is now
  {DATE1YR}. Where is your business, that would make you happy?"
Early questions dig for pain; late questions put them in the future. Once you
know a happy future, get commit.

### Stage 3 — COMMITMENT (the brand stage)
"So {NAME}, great news, I can help you get to that goal. Before I show you
how, I wanted to know: if everything makes sense to you, would you be opposed
to moving forward at the end of this call?"

"The only time 'no' means 'yes'." A yes-ask fires their survival instinct; a
no is safe to say. So they say it, "and now there is a spade in your pocket
for later." This is the stage everyone skips, and it is the name of the
brand: Commit to close.

If a timing truth surfaces here ("honestly I couldn't do anything until next
month"), there is NO commitment. Default move is the honesty release: "Thank
you for being honest here. Most people would just lie to me and we'd be
wasting both of our time... why don't you reach back out when you're settled
in and ready. Does that sound fair?" Time saved beats hope.

### Stage 4 — presentation
"Never demo the tech." "Never get into the weeds of the whiz-bang's features.
Weeds don't close deals." Three minutes max inside the product to prove it
exists, then out. Present a roadmap in steps and phases (e.g. 9 steps, 3
phases), then have them self-locate:

"This is the steps needed to fix your problems. Everyone falls at a different
place. Which step are you currently on?"

"Great news, most people are much further behind. You're on step 4. I handle
steps 5 through 9 while you focus on [the thing they'd rather be doing]."

Being at step 4 is GREAT NEWS (ally energy, progress not deficiency). The
steps they have not reached ARE the offer. "Nobody argues with their own pin."

### Stage 5 — test-close
Before any money ask: "How does everything look?" / "Do you see this NOT
working for your business?" Real objections surface here because they cost
nothing yet. "The lies start after you go for the close." Answer each
question, then "does that make sense?"

If they jump to price (good sign), do NOT answer. Isolate first: "We're about
to get to that. Other than price, are there any other questions or concerns,
or is price the only thing you need to know?" Flush the stack, then close.

### Stage 6 — close
"It costs $X,XXX.XX to get started. What do you want to do next?"

Then silence. "I mean it, DO NOT SAY ANOTHER WORD." Mute yourself if you have
to. If the machine ran clean they say something like "Damn, that's a good
question... let's get started." Money is spoken in words here: "It's
Seventy-Five-Hundred to get started."

### Post-call (the honesty close-out)
"Spend a few minutes being honest with yourself, then it's on the board."
"What could you have done better? Even if you closed, there is something."
Fumbled objections go in the log and get drilled.

## The 3 objection handlers

"All objections are lies. It's always about the price. Get to the truth."
"You do not need to learn a thousand rebuttals. 'If they say this you say
that' crap. You need three handlers." They MIX. "You can't spade everything.
You can't isolate everything. You can't 1-10 everything. But you can use
those 3 for any and all types of objections." Every handler ends in a
question, then you close again.

### 1. The Spade — call out the lie (always leads with "I'm confused")
"Confusion is authentic. 'Hold up' is confrontational." Played on the broken
commitment ("I need to talk to my wife first"):

"I'm confused. At the start of the call you said you would not be opposed if
everything makes sense, and you said it made sense. Normally when people say
that, they're really telling me no and don't want to hurt my feelings. Is
that what just happened here?"

Follow-ups: the deposit test ("Cool, go ahead and hold this price with a
deposit, speak with her and we can settle the rest after. If she tells you
no, I'll just refund your money."). The surgical version: "Why do you think
SHE would say no?" Whatever they answer is the TRUE objection. Handle it and
close. "I'm a big boy, you can just tell me no."

Origin story (teaching gold): named live on a call. "Let's call a spade a
spade, you just lied to me because you didn't want to hurt my feelings. You
know when I call you in 2 weeks you won't answer. Right?" "I was like oh
shit, I'm tucking that spade away."

The two-weeks spade: "Every time someone says follow up with me in 2 weeks,
and I do, what would your guess be with how many people respond? Zero. No one
ever responds. Telling me to follow up in 2 weeks was just you telling me no,
but you didn't want to hurt my feelings. Is that the case?"

### 2. Isolation — flush the stack
Kills the objection loop (objection, answer, new objection, control lost):
"Great question. Our best customers asked the same thing before they got
started. Before I answer it: are there any OTHER questions?" Flush the whole
stack, then close off the original.

The price version: "So you do believe this will help you and it's just about
pricing?" (yes) "PERFECT! That's the easiest part. If it's just about the
money, what can you swing today?" Close on a payment plan.

### 3. The Scale (the 1-10) — they dictate their own closing conditions
On "I need to think about it": "Makes sense, our best customers needed to
think about it too. While I'm here, you can ask me questions... well, let me
ask you this real quick: on a scale of 1 to 10, where 1 is 'I wish I never
showed up' and 10 is 'I'm ready to start right now'... where are you?"
They say 7. "Sweet. What would it take to get you to a 10?" They dictate
their own closing conditions; you become the order-taker for their list.

Control rules: never invite open questions ("got any questions?" is asking to
get hammered). Relate them to a best customer, then take the mic back.
Closer: "Never argue, disagree outright, or let them control the conversation
with questions... Nobody buys from someone they're arguing with."

## The hidden-row profit calculator (the 64-day close, replayed)

The real spreadsheet from a real deal (database reactivation, $7,500 to start
plus $2,500/month, July 2022). Mechanic: agree, agree, agree, reveal.

1. Build the sheet from THEIR answers: 6,000 leads, $5,000 avg profit per
   sale, 30% close rate (their numbers, labeled "their answer").
2. YOUR funnel rows are deliberately lowballed ("my answer, they know it's
   lowballed"): 30% validations, 20% interested, 50% scheduled.
3. Total Net Revenue computes: $270,000. Test close: "I mean, so... do you
   not see this working for your business?"
4. "They ALWAYS went straight to: 'Well, no, I mean I see it working but
   what's the cost?'"
5. Unhide the hidden row: month one, -$7,500. Adjusted net plus ROI (some
   crazy number like 3,000%).
6. "It's Seventy-Five-Hundred to get started. What would you like to do
   next?" And shut up.

"They agreed with these numbers. The hidden row did the work. Merged."
"Nobody argues with their own math." Guarantee doctrine baked in: "I couldn't
guarantee their closes. That's their problem. But I can guarantee
response-to-schedule rates." Guarantee only what you control.

## The $/call math (revenue per conversation)

"Close rate is a vanity metric." The proof comparison:
- 10 calls, $50,000 offer, 10% close = $50,000. $/call = $5,000.
- 10 calls, $5,000 offer, 25% "elite" close = $12,500. $/call = $1,250.
- Same calendar. 4x the money. The "weak" closer wins.

Planning rule: run it at 25% until you prove otherwise (people claim higher;
"everyone counts the maybes"). The two levers, always side by side:
- Lever A: raise the close rate (25% → 35% cuts calls by ~29%)
- Lever B: raise the offer (2x deal value cuts calls by 50%)
- "One of those is a lot easier than the other."

The price anchor (advanced lever): quote double. If they push back, offer the
real price if they commit today, on this call. The doubled quote frames the
real price as the deal.

## Receipts (the proof stack, exact captions)

- close_rate 71% — "71% close rate on a $30,000 offer. That number stops
  salespeople mid-scroll." Stack: one roadmap. Nine steps, three phases.
- sales_cycle 64 days → 1 call (30 min) — "That one stops founders." Stack:
  one excel sheet.
- "No demo. No deck. No dashboard tour. The edge was never the tools."
- webinars: 6 x ~90 min → $750,000 collected. "Less than 12 hours of work.
  That one is a gut check."
- The pay stub: closing for someone else, 13 closes in 14 days, $51,900
  collected, 10% cut = $5,190.
- $315K in 4 days 9 minutes average sales duration ($2.36M/month velocity).
- Lead stat order by audience: 71% (salespeople) → 64 days to 1 call
  (founders) → "an Excel sheet and a roadmap" (builders).

## closectl: the framework as software

closectl (app.committoclose.com, $39 founding / $49) is the framework as a
terminal-styled sales console. The story beats for scripts:

- `$ init`: a 5-step intake wizard (what you sell, the numbers, the pipeline,
  the pain) compiles a personalized GAMEPLAN.md: their math, their Business
  Doctor frame, the seven stages applied to their offer, their two objections
  dealt to the three handlers, their week.
- The compile streams their $/call headline: "your number: $X walks out of
  every call you take. protect it."
- `$ call`: the live CALL BOARD, kept open during the call. The 7-stage rail
  on the left, the current stage's card in the center seeded with the
  verbatim lines (editable), notes on the right that auto-tag by stage. The
  prospect's name rendered HUGE so you never fumble it.
- The stage-3 conflict gate: try to jump past COMMITMENT and it blocks you:
  "CONFLICT: you are about to push past COMMITMENT without the commitment. a
  deal that skips stage 3 dies at the pitch. get the 'would you be opposed'
  first." Skip anyway and the graph shows a permanent red X. "The graph will
  tell on you."
- Post-call: the honesty close-out. Fumbled objections feed the fumble log;
  the fumble log feeds the Sparring Partner (a voice AI that plays THEIR
  prospect, lies like a real one, and only agrees to close if you actually
  ran the framework). "Fumble the spade eight times at 6am, nobody watching."
- The scoreboard tracks the 3 C's: conversations, closes, cash collected.
  Plus the no-doctrine: "you're told no more than you're told yes, and you
  make more. a regular job makes less."

Tie-in tone: the course teaches the full framework for free; closectl is
where it touches real deals. Give away the how, sell the compression.

## Vocabulary

- **whiz-bang** — the impressive product/system the builder made and cannot
  sell. Deliberately universal: any member's product slots into the same
  framework language.
- **the spade** — the pocket commitment from stage 3, replayed at any lie.
- **merged** — deal closed. **CONFLICT** — you skipped a stage.
- **The Lurker** — stage 0 as a free runnable prompt file (committoclose.com).
- **THE LAW** (tier doctrine): "Once a lead is generated, it is a sales
  problem. Marketing gets the lead. Sales gets the money."
