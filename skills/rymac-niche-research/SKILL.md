---
name: rymac-niche-research
description: Runs RyMac's offer-validation research method. Fans out parallel subagents to map a niche's pain points in their own words, the psychology of why the pain persists, a competitor matrix, demand proof with a lead-pool count, the niche's unit economics (revenue bands, net margin range, where the margin comes from, the P&L split, average ticket), and a response-behavior audit scoring the niche against your mechanism, then delivers a build/pivot/skip verdict with the underserved wedge, the USP, an affordability call on what the niche can actually pay, a delivery-economics check that YOUR own margin clears a 65% floor (with the lowest price you could charge and the owned-vs-rented cost of your stack), the profit left on the table, and ROI hooks written in their own numbers. Use when the user asks to "research a niche", "validate an offer", "find the pain points", "run niche research", "should I build this", "who else sells this", "what are the margins in X", "can they afford my offer", "what should I price this at", or has an idea or observation about a market. Make sure to use this skill whenever the user is deciding what to build, sell, price, or make content about next.
argument-hint: [niche or idea, optional offer hypothesis, optional price point]
---

# RyMac Niche Research

Validate before building. The input is a niche, an idea, or a raw
observation ("developers build cool things but never sell them"). The
output is a verdict and an offer angle, never just a summary.

## Step 1: Frame it

Extract from the prompt before any research:
- **The niche** (who, specifically)
- **The pain hypothesis** (what the user suspects hurts)
- **The offer hypothesis** if one was given (what they are thinking of selling)
- **The price hypothesis** and whether it is one-time or monthly

If only an observation was given, write the hypotheses yourself and state
them up front so the research can prove or break them.

**If no price was given, ASK for one before running.** The affordability
math in Step 3 needs a number to test against, and a research report that
skips it answers the wrong question. One question, then proceed.

### Your mechanism (ask once, reuse forever)

Agent 6 below scores the niche against a **mechanism**: the standard you
believe operators should hit, whose failure to hit it becomes your offer.
Before fanning out, establish it:

1. **Does the user have their own mechanism or framework?** If yes, ask for
   the standards and the stats behind it, and save it to
   `references/my-mechanism.md` in this skill folder so it is never asked
   for again.
2. **If not, use the bundled default:** `references/the-3-laws.md`, the 3
   Laws of Landed Jobs (speed to lead, follow-up persistence, right
   message). It ships with sourced stats and works for any business that
   takes inbound leads. Say that this is the default and can be swapped.
3. **If the niche does not take inbound leads at all** (a pure product
   business, say), skip agent 6 and note why in the report rather than
   forcing a mechanism that does not apply.

## Step 2: Fan out (6 parallel subagents, always all 6)

Launch all six Agent subagents in ONE message so they run concurrently.
Each must use web search and return findings, not opinions.

1. **Pain map.** Where the niche complains in its own words: Reddit, niche
   forums, Facebook groups, review sites, YouTube comments. Return VERBATIM
   quotes with sources. The exact phrasing matters: it becomes headline and
   sales-page copy later.
2. **Why the pain persists.** The psychology: are they scared, taught wrong,
   burned by a past purchase, or just underserved? What have they already
   tried and why did it fail? (Example of this layer done right: developers
   avoid sales because they think selling means being pushy, so the winning
   product was practice plus a framework proving it is not pushy. Find THIS
   layer for your niche.)
3. **Competitor matrix.** Who sells to this niche now: offer, price,
   positioning, delivery model, and the gaps. This validates that money
   already moves in the niche AND locates the USP. Never skip or slim this
   agent; competitor analysis is wanted every run without being asked for.
4. **Demand proof + lead pool size.** Two jobs, always both. First, evidence
   people pay: pricing pages, ad spend, search volume signals, marketplace
   listings, "how much does X cost" content. Distinguish loud complaining
   from actual spending. Second, COUNT THE NICHE: how many of these
   businesses exist in the target market. Sources: Census/NAICS
   establishment counts, industry reports, trade association member counts,
   state licensing rolls, Google Maps density sampling. Return a number
   with the method behind it.
5. **Unit economics and margin anatomy.** The money question: can this niche
   afford what the user wants to sell, and what do the numbers sound like
   when they say them out loud on a call. Return all six blocks below, per
   revenue tier where the sources allow it (under $500K, $500K to $1M, $1M
   to $3M, $3M to $10M), because margin structure changes with size.

   a. **Revenue bands.** Typical annual gross revenue for a shop in this
      niche, and where the bulk of operators actually sit.
   b. **Margin range, not a single number.** Top-quartile net margin, median
      net margin, bottom-quartile net margin, and the resulting average.
      Report GROSS margin and NET margin separately and never blur them;
      they do different jobs later. Say plainly what separates the top
      performers from the bottom ones.
   c. **Where the margin comes from.** Break the revenue into its streams
      and give the margin on each: labor (billable hours billed out versus
      loaded hourly cost, the "effective labor rate" spread), parts and
      materials (markup or matrix multiplier), equipment or physical goods
      resale, add-on fees (environmental or disposal fees, shop supplies,
      trip or diagnostic or truck-roll fees, fuel surcharge, after-hours or
      emergency premium), and recurring revenue (maintenance plans, service
      contracts, monitoring). Note which streams carry the niche and which
      are rounding errors.
   d. **The ideal P&L split.** The industry benchmark percentages for COGS,
      overhead / opex, and net profit, plus where a struggling shop in this
      niche typically leaks (usually overhead creep or underpriced labor).
   e. **Ticket economics.** Average job or ticket value; the emergency,
      after-hours, or callout premium if one exists; typical close rate on
      an inbound lead; jobs per month at each revenue tier; and customer
      lifetime value if the niche has repeat or contract work. These are
      the numbers that become the hook.
   f. **What they already spend on software and marketing.** Typical monthly
      spend and the tools they already pay for, with prices. This is the
      real price ceiling, more honest than any margin percentage.

   Sources to actually go after, in rough order of trustworthiness:
   franchise disclosure document (FDD) Item 19 filings, which contain real
   unit-level P&Ls and are the best public source for a service trade;
   trade association financial benchmark surveys; industry research reports;
   CPA and bookkeeping firms that specialize in the trade; vertical software
   vendor benchmark reports (the big field-service platforms publish these);
   trade-specific benchmark books; and operator forum threads where owners
   post real numbers. Label every figure with its source and a confidence
   level. If a number has to be modeled rather than found, mark it MODELED
   and show the arithmetic.
6. **Response-behavior audit (the mechanism baseline).** How this niche
   actually handles an inbound lead today. This agent exists to produce the
   industry average that the mechanism gets measured against, so every
   figure must be an average or a percentage with a source, not an anecdote.

   Using the 3 Laws default, that means:

   a. **Speed.** Average speed to lead in this niche. Percentage of inbound
      calls that go unanswered. Percentage of web forms or missed calls that
      never get a callback at all. Typical callback lag (minutes, hours, or
      next business day). How after-hours and weekend calls are handled, and
      what share of total inbound lands after hours. Look for lead-response-
      time studies, missed-call studies from the vertical software vendors,
      secret-shopper reports on the trade, and "we called 50 contractors and
      only X called back" journalism, which exists for most service trades.
   b. **Persistence.** Average number of follow-up attempts before the niche
      gives up on a lead. Share of operators who stop after 1 or 2 touches.
      Whether they run a CRM at all or work off a notepad, a phone log, and
      memory. Which touch number the jobs actually land on.
   c. **Right message.** Which channels they use, and whether they use more
      than one (call only, or call plus text plus email). Whether the
      message changes between touches or the same voicemail gets left five
      times. Whether anything is segmented by where the buyer is in their
      awareness journey. Expect the answer to be "almost nobody does this";
      the job is to prove it with a number, because that gap is the wedge.
   d. **The cost of each gap.** Any sourced figure tying these behaviors to
      revenue: conversion lift from responding inside 5 minutes, the decay
      curve past 5 and past 10 minutes, the share of jobs won by whoever
      called back first, revenue lost to unanswered calls per year.

   **Read `references/the-3-laws.md` (or the user's own
   `references/my-mechanism.md`) before writing the gap analysis.** It
   carries the standards, the sourced stats, the decay curve, the scoring
   tiers, and the loss model. Use those numbers verbatim. Do not substitute
   a similar-sounding stat found during research, and do not let this agent
   go looking for a replacement decay curve; the standard is fixed, and the
   agent's only job is finding what THIS niche does against it.

## Step 3: Synthesize (the part the user reads)

Deliver in this order:

1. **Verdict: BUILD / PIVOT / SKIP.** One line, committed. Pivot means the
   pain is real but the offer hypothesis aims at the wrong wedge OR the
   wrong price; say where to aim instead. A niche with real pain, a real
   pool, and no room in the margins to pay is a PIVOT on price, not a BUILD.
2. **The lead pool.** Estimated count of target businesses, with the sizing
   method stated. Threshold: tens of thousands is ideal (plenty for cold
   outreach at scale); flag it loudly if the pool is under ~5,000 because a
   thin pool caps the whole model regardless of pain.
3. **The money math.** A short table readable in ten seconds:

   | | Bottom quartile | Median | Top quartile |
   |---|---|---|---|
   | Annual revenue | | | |
   | Gross margin % | | | |
   | Net margin % | | | |
   | Annual net profit $ | | | |
   | Monthly net profit $ | | | |
   | Average ticket | | | |
   | Gross margin per ticket $ | | | |

   Under it, the margin anatomy in one paragraph: which stream carries the
   profit (labor spread, parts markup, fees, recurring), the benchmark
   COGS / overhead / net split, and the one lever that separates a top
   performer from a bottom one.

4. **The affordability call.** State it as one word: AFFORDABLE, STRETCH, or
   UNAFFORDABLE, then show the arithmetic.

   Run it against the median operator, not the top performer:
   - Monthly net profit = annual revenue x net margin / 12.
   - Offer as a percentage of monthly net profit (convert one-time pricing
     to a monthly equivalent over the expected commitment before comparing).

   The bands, calibrated to how a small business owner actually feels a bill:
   - **Under ~5% of monthly net profit: AFFORDABLE.** Sells on pain alone.
     You can lead with the outcome and barely defend the price.
   - **~5% to ~15%: STRETCH.** Real money to them. The offer needs an
     explicit ROI proof in their numbers up front, not at the end.
   - **~15% to ~25%: HARD.** Only viable if payback lands inside the first
     billing cycle and can be shown in captured jobs. Consider leading with
     a smaller entry offer that fixes one sharp pain and ascending later.
   - **Over ~25%: UNAFFORDABLE.** Say so plainly. A thin-margin niche with
     loud pain is still a bad niche; the check comes out of net profit, not
     out of revenue.

   Then answer the actual decision in one line: **lead cheap or lead
   premium.** If the niche runs thin (single-digit net), lead with the
   smaller affordable solution that fixes the sharpest single pain. If the
   niche runs fat (mid-teens net or better) at a healthy revenue band, the
   ROI justifies the bigger, more expensive solution, so pitch that first.
   Name the price point the research supports, not the one hypothesized.

5. **The margin floor (your delivery economics).** Section 4 asked whether
   they can pay. This asks whether YOU can profit. Both must pass or the
   offer is not real, and most people only ever run the first one.

   **The rule worth stealing: never build a thing that cannot project a 65%
   net margin.** Read `references/delivery-costs.md`, which holds the cost
   card, the carve-outs, and the scenario method. If the user has not filled
   the cost card in yet, ask for the missing costs once and save them there.
   Deliver:

   a. **The stack you would ship them,** itemized from the offer hypothesis
      (voice scheduler, email follow-up, site chat scheduler, CRM seat).
   b. **Expected usage for THIS niche,** pulled from agent 5 (jobs per
      month, close rate) and agent 6 (inbound volume, missed-call share,
      after-hours share). Never guess it; usage is the variable that
      actually moves margin, so state where the number came from.
   c. **Three margin scenarios:** low-end (heavy usage, worst-case rates,
      no credits), mid (expected usage, measured rates), high-end (light
      usage, best rates).
   d. **THE FLOOR.** The lowest monthly price that still clears the margin
      rule at expected usage. One number, stated plainly. Worth knowing even
      if you never intend to sell there.
   e. **Any deliberate exception,** separately: a segment you have chosen to
      serve thinner. Label it a choice, never the business model.
   f. **The carve-outs.** Costs that belong to the client and never enter
      your margin math. The pattern: have them register their own A2P brand
      and buy their own phone number, so they own the number and you do not
      own the carrier-compliance liability. Same for their domain, their ad
      spend, their merchant account.
   g. **Owned versus rented, side by side.** The same delivered stack on
      rented rails (the common option runs ~$97/mo plus ~$0.25/min) next to
      your own measured cost. **State both numbers and stop.** Do not write
      the conclusion underneath. The arithmetic makes the argument, and a
      reader who arrives there themselves believes it. Same law as the
      calculator: never tell them anything you can get them to say
      themselves.

   If expected usage cannot clear the floor at a price section 4 says the
   niche can afford, the offer is broken. Say so loudly and name the fix:
   raise the price, cut the stack, cap the usage, or skip the niche. Section
   4 and section 5 disagreeing is a finding, not a rounding error.

   Mark any unmeasured component UNMEASURED and widen the low-end scenario
   rather than inventing a cost. A margin projection built on a guessed COGS
   is worse than no projection.

6. **Break-even in their units.** Never state ROI as a percentage. State it
   as the number of jobs.
   - Break-even jobs = offer price / gross margin per ticket.
   - Use GROSS (contribution) margin here, not net, and say why in the
     research file: a job the shop was already going to miss adds no new
     overhead, so the recovered dollars drop at gross margin. Net margin is
     for the affordability question in section 4; gross margin is for the
     ROI question here. Mixing them up either oversells or undersells.
   - Also give it as a fraction of a month: how many days of normal volume
     pay for the offer.

7. **The mechanism gap analysis.** The section that turns research into an
   offer. The equation being solved:

   > pain + industry average + which standard it breaks + their numbers
   > = potential profit gained

   Build this table, one column per law (or per standard in a custom
   mechanism):

   | | Speed | Persistence | Right message |
   |---|---|---|---|
   | The standard | under 5 minutes | touches 5 to 12 | changes per touch, multi-channel |
   | Niche average today | | | |
   | Size of the gap | | | |
   | Their own words for it | | | |
   | Jobs recoverable / month | | | |
   | Profit gained / month | | | |

   How to fill it:
   - **The standard** row is fixed. Take it from the mechanism reference,
     never from the research.
   - **Niche average today** comes from agent 6, sourced. If a standard has
     no findable average, say UNSOURCED rather than inventing one, and mark
     that row's dollars as MODELED.
   - **Size of the gap** is expressed in the standard's own unit and placed
     on the curve: minutes against the decay curve for speed, touch count
     against the money zone for persistence, channels and message variants
     against the awareness ladder for message.
   - **Their own words for it** is a verbatim quote from agent 1 mapped onto
     the standard it breaks. This mapping is the point of the whole section.
     The niche never says "we have a speed-to-lead problem." They say
     *"leads suck, they never answer when I call the next day."* That is a
     speed break, and next day is past 40 hours, the far end of the curve,
     not a small miss. The mechanism reference has a translation table of
     common complaints; extend it for this niche.
   - **Profit gained** uses the loss model in the mechanism reference, fed
     by agent 5's ticket and gross margin. Show the arithmetic inline so the
     user can defend it live on a call.

   Close the section by naming which standard this niche breaks WORST. That
   becomes the wedge, the lead pain in the copy, and the first thing the
   product should fix. Note also whether the competitors from agent 3 fix
   that standard or ignore it; one broken industry-wide AND unaddressed by
   every competitor is the strongest possible position.

8. **The underserved wedge.** Where competitors are not: the segment, the
   angle, or the delivery model left open. It should be consistent with the
   worst-broken standard from section 6; if it is not, explain why.
9. **The USP.** One sentence in plain words: why this offer wins against the
   matrix. Tie it to a real gap, not a vibe.
10. **2-3 offer angles** written in the niche's verbatim pain language,
   each as: promise + mechanism + price anchor from the competitor matrix,
   with the affordability call from section 4 respected. Name the specific
   standard each angle fixes.
11. **3 ROI hooks** built with the formula below, using the real numbers
    from agent 5 and the gaps from section 6. These are the lines said on a
    sales call and the ones that feed rymac-headline-copywriting.
12. **The pain language bank.** The best verbatim quotes, grouped by theme,
    ready to feed rymac-headline-copywriting and rymac-sales-page-builder.
    Include a **numbers vocabulary** sub-bank: the exact words this niche
    uses for its own economics (ticket, callout, truck roll, effective labor
    rate, billable hour, job cost, parts matrix, booked jobs, close rate,
    shop supplies, comeback). Using their word for a number is half of
    sounding like an insider; using the wrong one ends the call.
13. **What would kill this.** The strongest evidence AGAINST the verdict,
    stated honestly. One paragraph. Include the margin risk if the
    affordability call was STRETCH or worse, and say plainly if the
    mechanism gaps had to be modeled rather than sourced.

## The ROI hook formula

Seven beats, in this order. Every number comes from agent 5 or from
something the prospect already said. This is the shape:

1. **Ticket anchor.** "An emergency mobile callout averages $800 to $1,200
   up front"
2. **Margin overlay.** "and runs at 60% gross margin"
3. **Trigger volume.** "catching 3 after-hours or missed calls a month"
4. **Profit result.** "puts $2,000+ in pure profit back in your pocket."
5. **Their own admission.** "You already said you're missing 3 calls a day
   and 3 more after hours."
6. **Break-even in jobs.** "Just 3 of those pay for what my system costs."
7. **Time to ROI.** "So you're in ROI week 1 of every billing cycle."

At least one of the three hooks must be a **gap hook**, which swaps beat 3
for the industry average from agent 6 and lets the gap do the work:

1. Ticket anchor. "A callout in your world runs $800 to $1,200"
2. Margin overlay. "at about 60% gross."
3. **The industry average, stated as their reality.** "The average shop in
   this trade takes 4 hours to call a lead back, and most never call twice."
4. The standard and the decay. "Past 5 minutes the odds fall off a cliff,
   and by the next day that lead has already hired whoever picked up."
5. Their own admission. (the slot)
6. Profit result and break-even in jobs.
7. Time to ROI.

Rules for the hook:
- Ranges, not single numbers, on anything the prospect can dispute. A range
  they recognize builds trust; a precise number they disagree with kills it.
- Beat 5 is the strongest beat. Leave it as a slot to fill with what the
  prospect actually said on the call; use the niche's typical figure only
  when writing cold copy.
- Profit dollars, never percentages. "$2,000 back in your pocket" beats
  "a 3x return" with an owner who thinks in jobs and payroll.
- Never claim a margin number that agent 5 could not source. These get said
  out loud to people who know their own P&L better than you do.
- Name the standard, never the framework as jargon. Say "under 5 minutes,"
  not "Law 1 compliance." The framework is your scaffolding, not the
  prospect's vocabulary.

## Step 4: Save the handoff file (and publish it if you can)

1. **The handoff file.** Write the full synthesis to
   `niche-research-<niche-slug>.md` in the current project. This file is the
   machine handoff: the downstream skills consume it instead of
   re-researching or re-interviewing the user. Tell the user the file path.

   It MUST end with the handoff contract below, verbatim structure, so the
   next skill can read one block instead of parsing the essay. Fill every
   field; write UNKNOWN where the research came up empty rather than
   deleting a line, because a missing field is the one thing that forces the
   user to re-explain on the next run.

   ```markdown
   ## HANDOFF CONTRACT
   <!-- Downstream skills: read THIS block. Do not re-research. -->

   ### The spine  → rymac-sales-page-builder step 1
   - villain:            (the ONE enemy, external, never the reader)
   - promise:            (dream outcome in their words)
   - mechanism:          (the standards, and which one leads)
   - proof:              (the receipts available today)
   - offer:              (what is sold, at what price)
   - voice:              (how this niche talks, 1 line)

   ### Headline inputs  → rymac-headline-copywriting step 2
   - dream outcome:
   - timeframe:
   - the pain to remove ("without ___"):
   - their 3 best verbatim phrases:

   ### Calculator spec  → rymac-profit-calculator
   - calculator type:    LOSS-DRIVEN | COST-DRIVEN | CAPACITY-DRIVEN
   - leak variable:      (the one mechanism bleeding them)
   - inputs (2-4):       (name, sane range, PAINFUL default)
   - constants+sources:  (each constant with its citation)
   - formula:
   - bad-news line:      (in their language)
   - good-news line:     (same number, recovered)
   - the ask:            (price + book-a-call vs card-on-page)
   - one CTA:

   ### PAS engine inputs  → rymac-direct-sales-copy
   - self-identification bullets: (3-5, verbatim pain, "sounds like you?")
   - the agitation:      (what it costs them to keep doing nothing)
   - the villain cameo:  (who profits from their pain)
   - the turn:           (the standard that fixes it)

   ### Numbers pack  → any skill that quotes a figure
   - avg ticket / gross margin / net margin / monthly net profit:
   - break-even in jobs:
   - profit gained per month by standard:
   - every figure's source or MODELED tag:

   ### Delivery economics  → pricing, and any page that names a price
   - the stack shipped:
   - expected usage for this niche:
   - my margin low / mid / high:
   - THE FLOOR (lowest price clearing the margin rule):
   - any deliberate exception:
   - carve-outs (SMS/A2P, other pass-throughs):
   - owned vs rented cost, both numbers:
   ```

2. **The shareable page.** If your environment can publish a page
   (artifacts, a static HTML file, a PDF), always produce one without being
   asked. Nobody digests a research report as a wall of terminal text, so a
   run that ends in chat output alone has under-delivered even if the
   research was perfect. Panels in this order:

   1. **Verdict banner.** BUILD / PIVOT / SKIP. Unmissable.
   2. **Affordability banner.** AFFORDABLE / STRETCH / UNAFFORDABLE, with
      the lead-cheap-or-lead-premium call and the supported price point.
   3. **The money math table** and the margin anatomy.
   4. **The margin floor panel.** Your side of the deal: the three margin
      scenarios, THE FLOOR as one big number, any deliberate exception, the
      carve-outs, and the owned-versus-rented table. Present the two cost
      columns plainly with no conclusion written under them.
   5. **The mechanism scoreboard.** The gap table as cards, one per
      standard, each showing: the standard, the niche average, the size of
      the gap, one verbatim quote proving it, and the profit-gained figure.
      Visually flag the worst-broken one as the wedge.
   6. **Break-even in jobs**, as a single large number.
   7. The wedge and the USP.
   8. The offer angles.
   9. **The 3 ROI hooks in copy-ready blocks**, each formatted to lift
      straight into a call or an email, with the fill-in-the-blank slot for
      the prospect's own admission visibly marked.
   10. The pain language bank grouped by theme with sources, plus the
      numbers vocabulary.
   11. The lead pool.
   12. What would kill this.

   Design rules: scannable over complete, numbers big, prose small. Every
   figure carries its source or a MODELED tag inline.

## Step 5: Hand off the next move

The research is worthless if continuing it costs the user a re-explanation.
End both the shareable page (as its final panel, "The next move") and the
chat reply with literal, copy-pasteable commands, gated on the verdict.

If the verdict is BUILD or PIVOT, print exactly this shape:

```
Attack it:
  "use rymac-profit-calculator with niche-research-<slug>.md"
  "use rymac-sales-page-builder for <niche>, research is in niche-research-<slug>.md"
  "use rymac-headline-copywriting from niche-research-<slug>.md"
```

If the verdict is SKIP, print the one thing that would change the answer
instead, and do not print the attack commands.

Say plainly in one line that every downstream skill reads the HANDOFF
CONTRACT block at the bottom of that file, so none of them will ask the user
to re-explain the niche, the pain, the margins, or the price.

## Rules

1. Competitor analysis is mandatory, every run.
2. Verbatim quotes over paraphrases; copy is downstream of this research.
3. A verdict is required. "It depends" is not a deliverable.
4. Cheap emotional validation is not demand. Anchor the verdict in spend
   evidence (agent 4), not complaint volume (agent 1).
5. If the research breaks the user's hypothesis, say so plainly and pivot;
   that is the method working, not failing.
6. Margins are mandatory, every run, same as competitor analysis. A niche
   report with no net margin range is incomplete; send it back.
7. Never state a margin, ticket, or revenue figure without a source or a
   MODELED label with visible arithmetic. These numbers get said to owners
   who know their own P&L cold, and one invented figure ends the call.
8. Ranges over point estimates, always. Top quartile, median, bottom
   quartile, then the average. A single number hides the whole decision.
9. Gross margin for the ROI math, net margin for the affordability math.
   Never substitute one for the other.
10. Affordability is judged against the median operator in the niche, never
    the top performer. You sell to the middle of the market.
11. Every major pain theme gets mapped to the standard it breaks. An
    unmapped complaint is unfinished work: the niche describes symptoms, and
    the translation into a broken standard is what turns a complaint into an
    offer.
12. If a niche breaks none of the standards, that is a finding, not a gap to
    manufacture. Say so and let it push the verdict toward PIVOT or SKIP,
    because the mechanism being sold has nothing to fix there.
13. Publish the shareable page every run if the environment allows it. The
    chat reply is a summary and a link, never the report itself.
14. **A 65% net margin is a floor, not a target.** Never green-light a build
    that cannot project it at expected usage. If it cannot, say so in the
    verdict rather than burying it in section 5. Most people research whether
    the customer can pay and never check whether they can deliver.
15. Never invent a delivery cost. Measured or UNMEASURED, and an UNMEASURED
    component widens the low-end scenario. A margin projection resting on a
    guessed COGS is worse than admitting there is no projection yet.
16. Show owned-versus-rented cost side by side and write no conclusion under
    it. People believe what they work out for themselves; naming the
    conclusion turns a proof into a pitch and loses the reader.
17. Quote the mechanism's stats from its reference file exactly. A prospect
    can look up the same studies, so a misquoted figure or a decay curve
    invented mid-research burns the credibility the whole mechanism rests on.
