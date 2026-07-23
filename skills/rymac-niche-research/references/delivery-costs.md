# Delivery cost card — what it costs YOU to serve one client

The mirror of the affordability question. One section of the report asks
whether the niche can pay your price. This file is what lets the next
section answer whether you can deliver at that price and still make money.

**The standing rule: never build a thing that cannot project a 65% net
margin.** Not a target, a floor. If the projection cannot clear 65% at
expected usage, the offer is wrong, the price is wrong, or the stack is
wrong. Say which. Set your own number if 65% is not yours, but set one, and
hold it.

---

## Fill this in once (ask the user, then save it here)

Do not guess these. Ask, and write the answers into this file so they are
never asked for again. Anything the user cannot answer gets marked
**UNMEASURED**, not estimated.

| Component | Your cost | Unit | Measured? |
|---|---|---|---|
| AI voice agent | | per minute | |
| LLM / chat | | per conversation | |
| Email sending | | per 1,000 | |
| CRM / platform seat | | per client per month | |
| Payment processing | | % + fixed | |
| Support / your time | | hours per client per month | |

**A worked example, for shape only.** One measured voice-AI call, 10.15
minutes, came to $1.02 all-in: $0.10 speech-to-text, $0.24 LLM, $0.17
text-to-speech, and $0.51 in platform fees. That is about **$0.10 per
minute, of which half was the platform's cut rather than compute.** Your
numbers will differ; the useful habit is breaking the cost into parts,
because the biggest line is usually the one you can renegotiate or remove.

Always model a **worst-case drift** alongside the measured rate. Provider
prices move and usage runs hot; a projection that only works at the happy
rate is not a projection.

---

## What you should NOT absorb

Some costs belong to the client, and saying so protects both your margin and
your liability. The pattern worth copying:

**SMS / A2P.** Have the client register their own A2P brand and buy their
own phone number from the carrier or provider. They own the number, which is
better for them, and you do not take on carrier-compliance liability, which
is better for you. SMS then never appears in your margin math at all.

The same treatment fits anything billed directly to the client: their
domain, their ad spend, their merchant account. **Name each one as a
carve-out** in the report so nobody quietly re-adds it to COGS later.

---

## The rented-stack comparison

Always compute the same delivered stack two ways: on rails you own, and on
rails you rent. The common rented option for this kind of stack runs about
**$97/mo per account plus roughly $0.25/min** of voice usage.

| | Owned | Rented |
|---|---|---|
| Platform | ~$0 marginal | ~$97/mo |
| Voice | your measured rate | ~$0.25/min |

Run both at the niche's expected usage. The gap is usually large enough to
decide the business model on its own: a reseller charging $200/mo on rented
rails can be underwater before support costs, while the same $200 on owned
rails clears the floor comfortably.

**Put both numbers in the report and stop.** Do not write the conclusion
underneath them. The arithmetic makes the argument, and a reader who reaches
it themselves believes it, where a reader who gets told it discounts it.
Same law as the calculator: never tell them anything you can get them to say
themselves.

---

## How to build the projection

1. **Name the stack** you would ship for this niche (voice scheduler, email
   follow-up, site chat scheduler, CRM, review engine, whatever the offer
   contains).
2. **Pull expected usage from the research, not from a guess.** The unit-
   economics agent has jobs per month and close rate; the response-behavior
   agent has inbound call volume, missed-call share, and after-hours share.
   A niche doing 40 calls a month costs a fraction of one doing 400. Usage
   is the variable that actually moves margin, so state where it came from.
3. **Three scenarios, always:**
   - **Low-end:** heavy usage, worst-case rates, no credits or discounts.
   - **Mid:** expected usage, measured rates.
   - **High-end:** light usage, best-case rates.
4. **Solve for the floor.** The lowest monthly price that still clears your
   margin rule at expected usage. One number, stated plainly. Worth knowing
   even if you never intend to sell there.
5. **State any deliberate exception separately.** If you knowingly serve
   some segment thinner (a discount you have decided to give), give that
   second number and label it a choice, never present it as the model.
6. **Flag a fail loudly.** If expected usage cannot clear the floor at a
   price the niche can afford, the offer is broken. Say so and name the fix:
   raise the price, cut the stack, cap the usage, or skip the niche. The
   affordability section and this one disagreeing is a finding, not a
   rounding error.
