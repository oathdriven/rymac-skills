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
2. **Pick honest constants and cite them.** The speed-to-lead reference
   uses response-speed decay factors (under 5 minutes = 0.04 loss factor,
   scaling up to 0.6 for same-day answering) anchored to the MIT /
   InsideSales 15,000-lead study, shown right above the calculator. The
   rent reference uses a 9%/yr SaaS price-hike rate and a 10-year horizon,
   all restated in an on-page disclaimer.
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
