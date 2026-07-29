---
name: rymac-sales-page-builder
description: Build high-converting sales pages and landing pages with the RyMac funnel pattern - nail the headline first, then a pain-agitate-solution "engine" (a sales letter, a calculator, or a free interactive demo), then teach the mechanism, value stack, proof, pricing, FAQ, and a final CTA. Orchestrates the full machine checklist-style with a published build board: rymac-niche-research, rymac-headline-copywriting, rymac-direct-sales-copy, rymac-profit-calculator, rymac-exit-pop, rymac-call-funnel, rymac-relationship-sequence, rymac-paid-traffic-landing-page, ui-ux-pro-max, and rymac-vsl-copywriting in the right order. Use whenever the user wants to "build a landing page", "write a sales page", "make a sales letter", "build a funnel", a "high-converting page", a "hero section", or a "VSL page". Make sure to use this skill whenever the user is building, rewriting, or critiquing any marketing, sales, or landing page.
argument-hint: [what page / which brand / the offer]
---

# RyMac Sales Page Builder

Build a sales or landing page that converts, using one repeatable skeleton. The skeleton is always the same; the clothes change per offer. This skill is the map plus the order of operations, and it hands off to the right companion skill at each step so you are never guessing.

Load these on demand (one level deep):
- `${CLAUDE_SKILL_DIR}/references/section-playbook.md` - the job, copy anatomy, and a template for every section (hero through final CTA).
- `${CLAUDE_SKILL_DIR}/references/conversion-principles.md` - the page-level rules that make copy convert (value equation, one villain, the refrain, micro-yes, risk reversal, honesty, CTA patterns).
- `${CLAUDE_SKILL_DIR}/references/case-studies.md` - three live pages (Allodra, Sierra-6, closectl) mapped onto this exact skeleton. Read this to see "same bones, different clothes."

## The one insight

Every page is the same skeleton:

```
1. HERO          grab + promise. Either closes on its own, or earns the scroll to #2.
2. PAS ENGINE    the pain-agitate-solution section. Make the reader FEEL the pain is
                 real and theirs, then reveal the mechanism as the way out.
                 The FORM varies, the FUNCTION is constant:
                   - a written P.A.S. sales letter        (Sierra-6)
                   - an interactive calculator that shows them their own pain (Allodra)
                   - a free experience of the product that makes them feel the gap (closectl)
3. MECHANISM     show or teach HOW it works so the promise is believable.
                 Often you GIVE AWAY real value here. Belief is the goal.
4. VALUE STACK   name every piece, dollar-anchor it, tie each to a pain removed,
                 total it, make it dwarf the price. One "priceless" row = the emotional core.
5. PROOF         receipts, transcripts, screenshots, testimonials, the founder story.
6. PRICING       behind the value. Anchor, tiers, "one X pays for the year," risk reversal.
7. FAQ           kill the last objections. Warm. Each answer nudges back to the CTA.
                 ALSO your best SEO/AEO surface: keyword-as-question titles,
                 answer-first sentences, FAQPage schema, varied-anchor internal links.
8. FINAL CTA     "that's the whole page, what's the move?" two-path close + the refrain.
9. FOOTER        the foundation: socials (real human), legal (Terms/Privacy/Disclaimer),
                 contact, parent-company copyright. All outbound links open a NEW tab.
```

Three cross-cutting layers ride alongside the skeleton: an **exit pop** (its own mini-offer, something NOT sold on the page; build it with the `rymac-exit-pop` skill), a **chatbot / scheduling agent** that injects on scroll into section 2 (NOT the fold - keep the hero decision-free), stays out of the way, and doubles as live proof the product works (wire it with the `rymac-call-funnel` skill when the page's goal is booked calls), and the **relationship-building email sequence** every captured lead enters (exit pop and booking both feed it; build it with the `rymac-relationship-sequence` skill). Page-side anatomy in `section-playbook.md`.

**Legal is load-bearing, not optional.** The moment the page makes a cost claim ("run it free on billion-dollar infrastructure") or names a competitor ("cheaper than GoHighLevel"), it needs a **Disclaimer page** (plus Terms + Privacy) linked in the footer. The bold copy is only safe because the disclaimer is precise: free tiers are real but not a zero-cost guarantee, you're not affiliated with any company you name, no results are guaranteed. See `section-playbook.md` -> Legal pages.

Do not reinvent the structure per project. Reinvent only the PAS engine and the copy. Full anatomy and templates: `section-playbook.md`.

## The ask sets the page

**The single biggest design decision: what are you asking for?** A page selling a $49 card-on-page charge does a harder job than a page asking for a free call, because it has to handle objections and close with no human on the line. Match the amount of selling to the ask:

| The ask | Selling needed | Length | Example |
|---|---|---|---|
| **Book a free call** (high ticket, price set on the call) | Least. The VSL + PAS earn the call; the FAQ supports it. | Short, ~3 sections | Allodra ($900+, price made on the call) |
| **Gated deal** (price shown but you must call to qualify) | Medium. Price + scarcity + a "get to know each other" call gate. | Medium | Sierra-6 ($100/mo for the next 10 veterans) |
| **Card on the page** (buy now, no call) | Most. The full sales framework, objection handling built in. | Long, all 8 sections | closectl ($49/mo, buy on the page) |

Two hard rules that fall out of this:
- **Selling anything over ~$500: ask for a quick call first, not the card.** People buy big things from people. Write "book a quick call," never "book a zoom demo" (a demo sounds like work and like a pitch).
- **A booked call needs far less on-page selling than a card charge.** Do not bloat a book-a-call page with a full close; let the call do the closing. Less is more: Allodra converts on 3 sections because it only needs the click.

**Every section is earned by the one above it.** The page is the live sales framework rebuilt on paper: the hero earns the PAS, the PAS earns the mechanism, the value earns the price, and the FAQ is where you handle objections for a reader who cannot ask them out loud. If a section does not earn the next, cut it or fix it.

Research the buyer first, then design the page around the ask. Never design before you know the ask and the buyer.

## Build in this order (NOT top-to-bottom)

Copy this checklist and tick it off. Note: you build the highest-leverage pieces first, not the pieces in page order.

- [ ] 1. **The spine** (before a single word of copy). Write one page: **villain** (the ONE pain / enemy), **promise** (dream outcome), **mechanism** (how it works), **proof** (receipts), **offer**, **voice**. Everything on the page serves this. If the spine is wrong, the words do not matter. Skill: `rymac-niche-research` for the audience and their pain *in their own words* (if a `niche-research-<slug>.md` already exists, use it; mine proven hooks - cold emails that got replies, VSL hooks, real call language - before you invent anything).
- [ ] 2. **The headline** (single highest-leverage element). Nail the hero H1 before building anything else. **The formula: `[Dream outcome] in [timeframe] without [the pain]`** - this drives the H1, the subhead, and the bullets. **Never make the reader admit a failure** ("Practice the call without the judgment" beats "the call you keep avoiding" - the first sells the escape, the second makes them confess). The villain is external, never the reader. Skill: `rymac-headline-copywriting` (20+ variants, the five tests, pick the top 3, assemble the hero). Decide the hero's job here (see below).
- [ ] 3. **The hero**, built to its job. Skill: `rymac-paid-traffic-landing-page` for the fold rules.
- [ ] 4. **The PAS engine** - the section right after the hero that makes them NEED it. Pick its form (letter / calculator / free demo) to fit the offer. This is the section people skip; it is the one that converts.
- [ ] 5. **Everything below**, in the natural progression (mechanism -> value stack -> proof -> pricing -> FAQ -> final CTA).
- [ ] 6. **Structure first, copy sweep last.** Build the whole skeleton with placeholder copy, get it seen and approved, THEN do one top-to-bottom copy pass. See "How to work" below.
- [ ] 7. **The craft floor.** Run every line of the craft-floor checklist below and screenshot the result before you call the page done. A page with a perfect spine and system fonts still reads as cheap, and the reader prices the offer off the page.

## The hero's job (decide this in step 2)

| Traffic | Hero job | Hero CTA |
|---|---|---|
| Warm / most-aware (they know you, retargeting, referral) | **Convert on its own** | the buy or the lead form |
| Cold / problem-aware (paid ads, first touch) | **Earn the scroll** to the PAS engine | scrolls to #2, does not sell yet |

When in doubt on cold traffic, earn the scroll. A cold reader will not buy from a fold; they buy after the PAS engine has made the pain real.

## The craft floor (a page does not ship until every line passes)

Structure and copy are not the whole job. A page can have a great headline, a
great PAS letter and every correct element and still read as a free template.
That is a **craft** failure, not a copy failure, and it kills trust before a
word is read: a $10,000 offer on a $200 page is not believable.

This floor is derived from the real delta between allodra.ai (reads expensive)
and the first dispatchzap.com build (reads cheap) with near-identical structure.

- [ ] **1. Never ship system fonts.** This is the single loudest cheap tell.
      `Arial Narrow`, `Impact`, `Helvetica`, `Segoe Script`, `Georgia` as the
      display face = template. Load **2 or 3 real webfonts** with distinct
      roles: a display face for headlines, a body face, and a mono for
      labels/data. Allodra runs Geist + Instrument Serif + JetBrains Mono.
      Nothing else on this list matters if the type is wrong.
- [ ] **2. The headline gets a treatment, not just a size.** Split it: the
      setup in the base ink, the payload words in the brand gradient or accent.
      "Your CRM isn't **Software.** It's a **Landlord.**" carries a spectrum
      gradient on 2 words. One flat accent colour on the whole second line is
      the budget version of the same idea.
- [ ] **3. The background is never one flat fill.** 2 or 3 ambient radial
      glows, off-axis, low opacity, in brand hues. A single hex across 100vh
      reads as unfinished. This is 6 lines of CSS and it does more than any
      other single change.
- [ ] **4. The hero's proof must be visible in the first painted frame.**
      NEVER gate the hero visual behind an entrance animation, and never use
      `animation-fill-mode: backwards` on hero content. Animate INTO motion
      from a visible resting state, not FROM `opacity:0`. If a screenshot, a
      social preview, a Lighthouse run or a fast scroller can catch an empty
      box, the animation is a bug. **Test it: screenshot the page headless at
      0ms and look at what you get.**
- [ ] **5. Bold whole sentences or nothing.** Partial bold inside body copy is
      the most common self-inflicted readability wound: every bold run forces
      the eye to re-enter the sentence, so a paragraph with 3 bolded fragments
      reads slower than one with none. It works on a **single short line** (a
      hero bullet, a one-line stat) and it fights you everywhere else. In any
      multi-sentence block, bold the entire sentence that carries the point, or
      leave the block clean and let a pull-quote or a chip do the emphasis.
      Never bold a fragment mid-sentence in body copy.
- [ ] **6. Nothing sits below full opacity at rest.** Dimmed text reads as
      disabled or broken, not subtle. Use a dimmer *colour* token, never a
      lowered opacity, for de-emphasis.
- [ ] **7. Trust bars are logos, not grey text.** "AS SEEN ON ENTREPRENEURS ON
      FIRE" set in small grey caps is weaker than the logo itself. If real
      logos exist (press, integrations, stacks, clients), render them. A row
      of real marks is the cheapest credibility on the page.
- [ ] **8. Buttons have depth.** Gradient or layered fill, a soft glow in the
      accent, a hover lift, and a visible focus ring. A flat filled rectangle
      is a wireframe, not a CTA.
- [ ] **9. Kill dead space.** If a hero column is empty, or a gap between
      sections is larger than any gap inside them, the layout is wrong.
      Vertical rhythm comes off one spacing scale, used everywhere.
- [ ] **10. One ownable signature detail.** Every page needs a single device
      that could only belong to this brand: Allodra's dictionary eyebrow
      (`al·lo·di·al /əˈlōdēəl/ (adj.)` under a gradient rule), DispatchZap's
      hazard-stripe rule. Without it the page is competent and forgettable.
- [ ] **11. Look at it before you call it done.** Render the page headless and
      actually view the screenshot at full width AND at 390px. Do not report a
      page as finished on the basis that the code is correct. Half of these
      failures are only visible, never detectable in source.

**When copy is great and the page still feels cheap, it is always this list.**
Run it before the copy sweep, not after, because these are structural.

## Companion skills (hand off, do not re-derive)

| Step | Skill |
|---|---|
| Audience + pain research + offer validation | `rymac-niche-research` (produces the `niche-research-<slug>.md` handoff; downstream skills consume it instead of re-researching) |
| Headline + hero copy | `rymac-headline-copywriting` |
| The written P.A.S. letter engine (step 4, letter form) | `rymac-direct-sales-copy` |
| The calculator engine (step 4, calculator form) | `rymac-profit-calculator` |
| Exit pop (cross-cutting layer) | `rymac-exit-pop` |
| Chat scheduler + voice agent + booking plumbing | `rymac-call-funnel` |
| Lead nurture after capture | `rymac-relationship-sequence` |
| Fold rules, conversion structure, anti-leak | `rymac-paid-traffic-landing-page` |
| Visual design + build | `ui-ux-pro-max`, `frontend-design` |
| VSL script (for the hero video) | `rymac-vsl-copywriting` |
| VSL render | `remotion-best-practices` |

If a companion skill is not installed (e.g. a Skool member using this standalone), the principles you need are inlined in `conversion-principles.md` - use those.

## The build board (publish it, keep it current)

At the START of every build, publish an Artifact (load artifact-design
first) that is the living plan for the whole machine, and republish it to
the same URL as things complete. Ryan runs off this board. It contains:

1. **The full-machine checklist**, every element with its owner:

| Element | Skill | Owner |
|---|---|---|
| Niche research + offer validation | rymac-niche-research | Claude |
| Decide the ask + approve the spine | (decision) | Ryan |
| Headline + hero | rymac-headline-copywriting | Claude drafts, Ryan picks |
| PAS engine (letter or calculator) | rymac-direct-sales-copy / rymac-profit-calculator | Claude |
| Sections below (mechanism -> final CTA) | this skill | Claude |
| Exit pop + its unseen asset | rymac-exit-pop | Claude builds, Ryan approves the asset |
| Call funnel (chat + voice + booking + escalation) | rymac-call-funnel | Claude wires, Ryan sets on-call contact + hours |
| Relationship sequence E1-E10 | rymac-relationship-sequence | Claude drafts, Ryan voice-checks |
| Domain + DNS + deploy | (build) | Ryan buys, Claude deploys |
| Legal pages + footer | this skill | Claude |
| Copy sweep + em-dash grep | this skill | Both, independently, then merge |

2. **A "still left" section** at the top: the next 3 actions, who owns
   each. Update it every time something finishes; the board should always
   answer "what's still left?" at a glance.
3. **Status per element**: not started / in progress / done, with links to
   drafts or live URLs as they exist.

The board is the orchestrator's contract: any element skipped must be
skipped out loud on the board, never silently.

## How to work (the method that actually ships)

- **Structure first, copy ("knit picking") last.** Lock the skeleton with rough copy so decisions are about layout, not wording. Polish every line only once the bones are approved.
- **Build -> show -> react -> iterate.** People decide by seeing, not reading a plan. Ship a screenshot after each section and let them react. "I have to see it" is the default, not the exception.
- **Yes/yes/swap.** To move fast through structure, propose, let them approve or swap in one word, keep going. Save debate for the copy sweep.
- **Parallel sweeps, then reconcile.** For the copy pass, have the human do their own top-to-bottom sweep AND you do yours independently, then merge to best-of-both. Independent beats sequential (no anchoring).
- **Save early and often.** Commit the build and write the state to a handoff/brain doc so a dead laptop or session cannot cost the work.
- **Verbatim founder lines are sacred.** If the founder has signature lines (a sales script, a proof line), use them exactly. Write around them, never paraphrase them.

## House rules (RyMac defaults - swap for the brand's own)

These are Ryan's; a Skool member should replace them with their brand's:
- **Write at a 5th-to-8th grade reading level.** Short sentences, plain words. Check with the free Hemingway app (hemingwayapp.com) and cut until it passes. Clever loses to clear.
- **Always show the promised thing.** Even a static image beats an empty slot: a screenshot of the dashboard, the result, the product. The reader should SEE what they are being promised, not just read about it. **Best form:** brand-native motion loops (short, silent, on-brand animations rendered over the real screenshots - e.g. a deal card dragging to Won, a bar chart counting up) instead of generic gifs; they read as "the actual product, alive." A montage of them makes a strong "you're looking at it" proof shot.
- **No em dashes** in customer-facing copy. Ship gate: grep the built page, zero hits. (This one bites repeatedly - sweep EVERY section, including ones you wrote earlier.)
- **Numbers are always numbers** (digits, never spelled out). Same tier as the em-dash rule; sweep for spelled-out figures too.
- **No orphaned words** (a lone word wrapping to its own line reads lazy). Enforce with `text-wrap: pretty` + `white-space: nowrap` on short labels.
- **Headline house style:** Title Case, with the gradient span carrying its trailing punctuation (the period rides the gradient too, so it never snaps back to white). The brand wordmark wears the full gradient everywhere, every piece of it (`.ai` included).
- **One brand palette + font pair**, committed. Dark-only or light-only, not both by accident.
- **Progressive enhancement.** The offer must be readable and takeable with JavaScript off; interactivity only enhances.
- **Honesty guardrail.** Only claims you will defend publicly. One soft/inflated claim next to your best proof poisons the credibility of both. Protect the falsifiable numbers.

## Critical rules

1. **Never build top-to-bottom.** Spine -> headline -> hero -> PAS engine -> the rest. Highest leverage first.
2. **The PAS engine is not optional.** A hero followed by features and a price does not convert cold traffic. Something between them must make the pain real (letter, calculator, or free demo).
3. **Every ask gets a risk reversal** beside it (free, no card, cancel anytime, guarantee, "one close pays for the year").
4. **One villain, one promise, one refrain**, carried from hero to final CTA. See `conversion-principles.md`.
5. **Structure before copy.** Do not polish words on a layout that is not approved.
6. **Ship the legal + footer with the page, not after.** A page that makes cost or competitor claims is not shippable until the Disclaimer exists and is linked. The footer's outbound links open new tabs (no leaks) and pin their visited color.

## Final note

The skeleton is fixed; your job is the PAS engine and the copy. When you are unsure what a section should say, open `section-playbook.md` for that section. When you are unsure whether a line converts, check it against `conversion-principles.md`. When you want proof the skeleton holds across wildly different offers, read `case-studies.md`.
