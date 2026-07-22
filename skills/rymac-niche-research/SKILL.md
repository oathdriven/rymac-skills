---
name: rymac-niche-research
description: Runs RyMac's offer-validation research method. Fans out parallel subagents to map a niche's pain points in their own words, the psychology of why the pain persists, a competitor matrix, and demand proof with a lead-pool count, then delivers a build/pivot/skip verdict with the underserved wedge, the USP, and offer angles written in the niche's own language. Use when the user asks to "research a niche", "validate an offer", "find the pain points", "run niche research", "should I build this", "who else sells this", or has an idea or observation about a market. Make sure to use this skill whenever the user is deciding what to build, sell, or make content about next.
argument-hint: [niche or idea, optional offer hypothesis]
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

If only an observation was given, write the hypotheses yourself and state
them up front so the research can prove or break them.

## Step 2: Fan out (4 parallel subagents, always all 4)

Launch all four Agent subagents in ONE message so they run concurrently.
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

## Step 3: Synthesize (the part the user reads)

Deliver in this order:

1. **Verdict: BUILD / PIVOT / SKIP.** One line, committed. Pivot means the
   pain is real but the offer hypothesis aims at the wrong wedge; say where
   to aim instead.
2. **The lead pool.** Estimated count of target businesses, with the sizing
   method stated. Threshold: tens of thousands is ideal (plenty for cold
   outreach at scale); flag it loudly if the pool is under ~5,000 because a
   thin pool caps the whole model regardless of pain.
3. **The underserved wedge.** Where competitors are not: the segment, the
   angle, or the delivery model left open.
4. **The USP.** One sentence in plain words: why this offer wins against the
   matrix. Tie it to a real gap, not a vibe.
5. **2-3 offer angles** written in the niche's verbatim pain language,
   each as: promise + mechanism + price anchor from the competitor matrix.
6. **The pain language bank.** The best verbatim quotes, grouped by theme,
   ready to feed rymac-headline-copywriting and rymac-sales-page-builder.
7. **What would kill this.** The strongest evidence AGAINST the verdict,
   stated honestly. One paragraph.

## Step 4: Save the handoff file

Write the full synthesis to `niche-research-<niche-slug>.md` in the current
project. This file is the machine handoff: rymac-headline-copywriting and
rymac-direct-sales-copy consume it instead of re-researching. Tell the user
the file path. If your environment supports publishing a shareable page
(artifacts), also publish a scannable version with the verdict banner up
top.

## Rules

1. Competitor analysis is mandatory, every run.
2. Verbatim quotes over paraphrases; copy is downstream of this research.
3. A verdict is required. "It depends" is not a deliverable.
4. Cheap emotional validation is not demand. Anchor the verdict in spend
   evidence (agent 4), not complaint volume (agent 1).
5. If the research breaks the user's hypothesis, say so plainly and pivot;
   that is the method working, not failing.
