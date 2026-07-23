---
name: rymac-profit-calculator
description: Builds RyMac's "run YOUR numbers" profit/loss calculator for any niche: an interactive on-page calculator that shows a prospect what their current leak costs them, framed as their own math, ending in one CTA. Use when the user asks to "build a calculator", "profit calculator", "loss calculator", "run your numbers section", "ROI calculator", or when a sales page needs its pain engine. Make sure to use this skill whenever an ROI, loss, or savings calculator is being designed or built for a landing or sales page.
argument-hint: [niche + the leak the calculator monetizes]
---

# RyMac Profit Calculator

Build the calculator that makes the prospect argue with their own math
instead of your claims. The sales law behind it: never tell them anything
you can get them to say themselves. They will not believe what you say;
they will believe everything they say. Two live reference patterns are
described inline below (a speed-to-lead loss calculator and a
SaaS-rent/growth-tax calculator, both running on RyMac's own pages).

## Start here: is there a research file?

If a `niche-research-<slug>.md` exists for this niche, **read its HANDOFF
CONTRACT block first and build from it.** It already carries the calculator
type, the leak variable, the inputs with painful defaults, the constants
with sources, the formula, the bad-news and good-news lines in the niche's
own words, the ask, and the CTA. Do not re-interview the user for anything
that block already answers, and do not re-research the niche. If a contract
field says UNKNOWN, that field is the only thing worth asking about.

No research file? Build from scratch with the method below, and say up front
that running `rymac-niche-research` first would have supplied the constants.

## What this actually is

**The calculator is the P.A.S. sales letter's logical twin.** Same three
beats, different fuel:

| | `rymac-direct-sales-copy` (the letter) | this skill (the calculator) |
|---|---|---|
| **Problem** | questions that make them self-identify: "sound like you?" | input fields that make them ADMIT their own numbers |
| **Agitate** | emotional, cinematic, the villain, the Groundhog Day feeling | arithmetic. Their number, annualized, sitting there in red |
| **Solution** | the mechanism revealed as the way out | the same number shown recovered, one CTA under it |

Emotion gets people to buy; logic lets them justify what they already
decided. The letter does the first job, this does the second, and a strong
page often runs both. So the calculator's persuasion comes entirely from
arithmetic they cannot argue with, because they typed the inputs. The moment
it editorializes, it stops being logic and becomes just another claim, and
it loses the only advantage it had over the letter.

**The mechanism, once:** get them to admit their numbers, let the math
agitate the pain, make the solution the obvious conclusion of their own
arithmetic.

## Pick the type before you build

| Type | Monetizes | The question it answers |
|---|---|---|
| **LOSS-DRIVEN** | revenue they never captured | "what did last month cost you?" |
| **COST-DRIVEN** | money they already spend | "what is renting this costing you?" |
| **CAPACITY-DRIVEN** | headroom they cannot reach | "what would one more crew be worth?" |

The type sets the register. Loss-driven says *you are bleeding and did not
know it*. Cost-driven says *you are being farmed and did not know it*. Never
mix two leaks in one widget; it halves the punch of both.

## The design law

**The output is THEIR math, not our claim.** The calculator takes the
prospect's own numbers, applies honest constants with named sources, and
shows the cost of their current leak. Never inflate: one dishonest constant
next to their real numbers poisons the whole page.

## Construction method

1. **Name the leak variable.** The one mechanism bleeding them: response
   speed decay, rent plus compounding price hikes, missed after-hours
   calls, an unworked database, etc. If you ran rymac-niche-research, the
   handoff file (`niche-research-<slug>.md`) names it.
2. **Pick honest constants and cite them.** For any LOSS-DRIVEN calculator
   built on speed to lead or follow-up, the constants ship with this pack in
   `rymac-niche-research/references/the-3-laws.md`: the 0.60 winnable
   factor, the loss-rate table (under 5 min = 0.04, 30 min = 0.28, 1 hr =
   0.42, same/next day = 0.60), and the MIT / Harvard stats that justify
   them. Use those exact values so the calculator and the research report
   quote the same number. That file also marks which figures are
   attributable to the studies and which are one operator's calibration;
   keep that distinction in the on-page disclaimer. The rent reference uses
   a 9%/yr SaaS price-hike rate and a 10-year horizon, all restated in an
   on-page disclaimer.
3. **Two to four inputs maximum,** clamped to sane ranges, with defaults
   chosen so the DEFAULT result is already painful (reference defaults:
   $2,500 job value, 30 leads/mo, same-day answering).
4. **The formula shape:** monthly loss = (winnable volume) x (leak factor)
   x (unit value). Then annualize x12, and show a recovery projection that
   is conservative (the reference multiplies annual by 1.3 for the upside
   case, not a 10x fantasy).
5. **Output as bad news then good news.** "The Bad News:" lost units and
   dollars last month, then the 12-month cost "if it stays broken." Then
   "The Good News:" the same number recovered. Same number both ways: the
   loss IS the opportunity.
6. **One CTA after the result.** The next step in the funnel, nothing else
   ("Book Your Free Fix-It Call →" / "Apply To Qualify →"). Fire the
   pixel event on click.

## Optional patterns (use when they fit)

- **Shareable permalink:** recompute from query string on a results page
  (`/r?c=...&p=...`) so cold email can prefill `?company=` and the result
  URL can be forwarded.
- **Gated supportive asset below the ungated number:** the big number is
  NEVER gated; a bonus asset below it may be email-gated. Gate submission
  dual-writes (raw lead log + CRM form submit with attribution), both
  best-effort, and the unlock never blocks on capture failure.
- **The pre-frame:** a short opportunity-cost teach right above the
  calculator (a money-choice question plus the cited study) so the
  prospect believes the constants before entering their numbers.

## Checklist

- [ ] Leak variable named from research; constants chosen and cited
- [ ] Inputs clamped, defaults painful, mobile-friendly
- [ ] Bad news / good news output, conservative recovery projection
- [ ] One CTA, pixel event, funnel-consistent
- [ ] Disclaimer restating every assumption
- [ ] Honesty check: every constant survivable in public

## Hand off the next move

Close by printing the next commands, so the build keeps moving without a
re-explanation:

```
  "use rymac-sales-page-builder, the calculator is the PAS engine"
  "use rymac-direct-sales-copy for the emotional twin of this calculator"
  "use rymac-headline-copywriting for the hero above it"
```

If the calculator was built from a `niche-research-<slug>.md`, name that
file in the handoff so the next skill reads the same contract.
