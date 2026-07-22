---
name: rymac-exit-pop
description: Builds RyMac's exit-intent popup pattern on any landing or sales page: desktop mouse-leave plus the mobile fast-scroll-up trigger, offering a supportive asset that is deliberately NEVER promised on the page itself. Use when the user asks to "add an exit pop", "build an exit popup", "exit intent", "catch people leaving the page", or when finishing any sales/landing page build. Make sure to use this skill whenever an exit-intent popup or leave-catcher is being designed, built, or critiqued.
argument-hint: [page or site to add the exit pop to, and what asset it offers]
---

# RyMac Exit Pop

Build the exit pop the way RyMac builds them, proven on two live sales
pages (a single-file static site and a Next.js/React app).

## The one law (never break it)

**Never exit pop an offer the page already promises.** The pop offers
something supportive and UNSEEN: the page sells the paid thing, the pop
gives a free thing that helps them even if they never buy. Live example:
a page selling a $100/mo system and a booked call runs a pop offering a
free educational brief whose own bullet says "2 of the 3 fixes don't
involve me." Another page pushes an application call; its pop offers a
free roadmap that appears nowhere else on the page. If the pop repeats a
page offer, it is not an exit pop, it is a nag.

## The offer formula

A mini sales page in one card:
1. Pattern-interrupt eyebrow (the proven frame is the 🛑 emoji:
   "🛑 Leaving Empty-Handed? 🛑" / "🛑 WAIT 🛑")
2. Headline naming the free asset ("Don't leave without your roadmap")
3. EITHER 3-4 curiosity bullets with bolded numbers (best when the asset
   is educational) OR an image thumbnail + one-line body (best when the
   asset is a visual artifact)
4. Single email input, one CTA button naming the delivery ("Send Me The
   Free Brief →")
5. Fine print ("No spam. Unsubscribe anytime.")
6. Success state that keeps them on the page ("On its way. Check your
   inbox." + a back-to-page button), never a redirect away
7. The pop copy must match the asset exactly. One asset, one description,
   everywhere: if the asset is "3 phases, 9 steps," never describe it as
   "3 phases" in one place and "9 steps" in another.

## The trigger (proven constants, copy them)

- Arm delay after page load: 1500-3000 ms (never fire on a fast bounce)
- Desktop: fire when the cursor exits the top of the viewport
  (`mouseout`/`mouseleave` with `relatedTarget === null && clientY <= 0`)
- Mobile: fire on scroll UP near the top: `y < lastY && y < 300 && y > 0`
  (direction + position test; passive scroll listener)
- Frequency: once per page view minimum (a `shown` flag); once per visitor
  preferred (localStorage key pattern `brand:exitpop:shown`)
- Close on: Escape key, click outside the card, explicit close button
- Lock body scroll while open, restore on close

## Lead capture

- POST the email to the site's form endpoint / CRM with attribution:
  `utmSource: "exit-pop"` plus the landing page URL, so pop leads are
  always distinguishable
- Fire the pixel Lead event with a content_name naming the pop asset
- The capture must be best-effort: if the POST fails, still show success
  and deliver by fallback; never strand the visitor in an error state

## Checklist

- [ ] Confirm the offered asset is NOT promised anywhere on the page
- [ ] Build card + triggers with the constants above
- [ ] Wire capture with exit-pop attribution + pixel event
- [ ] Test: desktop mouse-out, mobile scroll-up at top, Escape, re-arm
      behavior, success state
- [ ] Copy check: asset name and framing identical to the asset itself
