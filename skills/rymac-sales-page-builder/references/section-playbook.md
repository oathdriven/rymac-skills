# Section playbook

The job, the copy anatomy, and a fill-in template for every section. Build in leverage order (spine -> headline -> hero -> PAS engine -> rest), but the sections appear on the page in the order below.

## Contents
- [0. Spine (not a section - do first)](#0-spine)
- [Optional: qualifier bar](#qualifier-bar)
- [1. Hero](#1-hero)
- [2. PAS engine](#2-pas-engine)
- [3. Mechanism](#3-mechanism)
- [4. Value stack](#4-value-stack)
- [5. Proof](#5-proof)
- [6. Pricing](#6-pricing)
- [7. FAQ](#7-faq)
- [8. Final CTA](#8-final-cta)
- [9. Footer](#9-footer)
- [Legal pages (Terms / Privacy / Disclaimer)](#legal-pages)
- [Optional: recapture layer](#recapture-layer)

## 0. Spine
Not on the page - the doc everything serves. One page, six lines:
- **Villain:** the ONE pain / enemy (a practice, a tool, a feeling - never the reader's own failure). "the growth tax" / "the ABC-agency kid" / "the freeze."
- **Promise:** the dream outcome, specific and visualizable.
- **Mechanism:** how it delivers the promise, in one sentence.
- **Proof:** the receipts you can defend (numbers, screenshots, the founder win).
- **Offer:** what they buy, the price, the risk reversal.
- **Voice:** the founder's signature lines (verbatim, sacred) and tone.
If you cannot fill all six, do research (`niche-research`/`researcher`) before writing copy.

## Qualifier bar
Optional thin bar above or in the hero that names exactly who this is for. Disqualifying the wrong reader makes the right one lean in. Sierra-6: "This Page Is Only For Veteran-Owned Home-Service Business Owners." Use when the offer is niche.

## 1. Hero
**Job:** grab + promise in 3 seconds. Either close (warm traffic) or earn the scroll to the PAS engine (cold traffic).
**The headline formula:** `[Dream outcome] in [timeframe] without [the pain]`. It drives the H1, the subhead, and the bullets. Never make the reader admit a failure - frame the escape, not the confession ("close with confidence without a real deal on the line," not "the call you keep avoiding"). The villain is external.
**Anatomy (top to bottom):**
- **Eyebrow** - who it is for / the felt moment, stated without shaming them.
- **H1** - dream outcome without the pain, or a reframe that names the villain ("Your CRM isn't Software. It's a Landlord."). Use `rymac-headline-copywriting` to generate and score.
- **Subhead** - the mechanism + risk removal ("without X. without Y. without Z.").
- **The one visual** - a VSL (use `rymac-vsl-copywriting`), or the interactive thing itself. One, not a gallery.
- **One CTA** - value-based, first person. Warm: the buy/lead. Cold: scrolls to the PAS engine.
- **Risk-reversal ticks** - 3 short items ("Free, no card - 10 minutes - cancel anytime").
- **Trust bar** - 3 credibility items, your most falsifiable first ("71% close rate - on $30,000 deals - Featured on EOFire").
**Template:**
```
[eyebrow: who / the felt moment]
[H1: pain x dream, or villain reframe]
[subhead: the mechanism, without pain-1 / pain-2 / pain-3]
[VSL or the interactive thing]
[CTA: value-based, first person]  [3 risk-reversal ticks]
[trust bar: 3 items, falsifiable first]
```

## 2. PAS engine
**Job:** the most important section. Make the reader FEEL the pain is real and theirs, then reveal the mechanism as the escape. Skipping this is why hero-then-features pages fail on cold traffic.
**Pick the form by buyer:**
- **Sales letter** - emotional/story buyer. Structure: pain checklist -> dream contrast -> agitate + name the villain -> founder origin story with a quantified win -> turn to the solution -> future-pace -> P.S. close. (Sierra-6.) Use the `rymac-direct-sales-copy` skill to write it (the full 23-beat P.A.S. framework). **Presentation as a pattern interrupt:** render the letter as a physical PIECE OF PAPER popping off the page - a warm-white sheet with a drop shadow, BLACK ink, a "From the desk of: [Name]" + "Date:" letterhead, red X's on the pain bullets and green checks on the outcome bullets, a serif-italic signature, and classic blue hyperlinks. On a slick dark page this reads as a real, no-shit letter someone wrote you, and the pattern break itself pulls the eye in. Copy stays verbatim; only the presentation changes.
- **Calculator** - numbers/ROI buyer. They input their own figures; it outputs their own pain as one big number; that number transitions to the solution. (Allodra.) Make presets real (running costs, not sticker prices) so the number is defensible.
- **Free demo / experience** - experiential product. Let them use the real thing free, in-page, no signup, so they feel the gap themselves - while you capture the lead. (closectl.)
**Rule:** whichever form, it ends by pivoting from pain to the mechanism, and it captures a lead (a submitted number, an email for the report, a phone number for the call).

## 3. Mechanism
**Job:** show or teach HOW it works so the promise is believable. Belief is the product here. Often you give away real value (the framework, the math, the "3 Laws") - generosity builds trust and micro-commitments.
**Forms:** a data-backed principle set (Sierra-6 "3 Laws"), the ownership math/report (Allodra), the actual method given free (closectl board + framework). Teach enough that they think "this could work for me," not so much that there is no reason to buy.

## 4. Value stack
**Job:** name every piece, dollar-anchor it, tie each to a pain removed, total it, make the total dwarf the price.
**Anatomy:** rows of `[piece] + [$ value] + [the pain it removes]`, a final **priceless** row for the emotional core (the confidence / the ownership / the freedom), a **sum line** ("$5,282 of value... one close pays for the year").
**Rule:** set $ numbers you would defend if asked "how did you get that?" A clean anchor beats a suspicious one. Then anchor-then-reveal into pricing.

## 5. Proof
**Job:** believability - the second half of the value equation. "Receipts, not adjectives."
**Forms (use what you have):** real screenshots (payments, dashboards, results), a transcript, the founder story with a falsifiable win, a stat bar, third-party authority (EOFire), testimonials. Make sure proof images actually ship.

## 6. Pricing
**Job:** present the price behind the value, with risk killed.
**Anatomy:** the anchor (value from the stack, or a struck higher price), the tier(s) with a one-line "who each is for," a "one X pays for the year" line, and risk reversal (cancel anytime, founding price locked, a guarantee box). Withhold price and route to an application/call instead if the sale is high-touch (Allodra).

## 7. FAQ
**Job:** this is the **objection-handling stage of the live sales framework, for a reader who cannot object out loud.** Not filler, not there to look complete. Each question is a real objection you would get on a call; each answer is how you would handle it. Warm, in the founder's voice. Header: "What's on your mind?" (house signature).
**Include the real objections you hear** (price, "is this legit," "will it work for me," tech-savvy, cancellation, guarantee). Every answer that can, nudges back to the CTA. Dead-end the FAQ into the primary CTA.
**Fire the chatbot / scheduling agent here.** A chat or voice-scheduling agent that appears around the FAQ (and otherwise stays out of the way) catches the reader whose exact objection is not listed, and - if the product is an AI agent - doubles as live proof it works (Allodra's voice scheduler books the call AND demonstrates the thing). Keep it unobtrusive until the reader is deep enough to have real questions. **Refinement (Allodra):** don't load the widget on the fold (keeps the hero decision-free); inject it on scroll into section 2 and let its teaser bubble pop ~1.5s later ("hand-wave, Hi, I'm Ally, can I help?"). The fold stays clean; the helper shows up right as they start reading.

**The FAQ is also your best SEO/AEO real estate. Make it earn search traffic, not just handle objections.** When the brand has a keyword plan, do a second pass over the FAQ with it open:
- **Retitle questions to VERBATIM search queries** where it reads naturally ("Is this a GoHighLevel alternative?", "Is this a one-time payment CRM with no monthly fees?", "How much does an AI voice agent actually cost to run?"). The question *is* the keyword, phrased as a question. Keep the conversion questions (Charter/Fit/Trust) human - not everything is a search play.
- **Answer-first sentences.** Open each answer with a self-contained, liftable statement ("Yes: the GoHighLevel alternative you actually own." / "Pennies."). AI Overviews and LLMs lift the first sentence; make it stand alone.
- **Ship FAQPage JSON-LD** built from the SAME question/answer source so schema can never drift from the rendered copy. This is what gets you cited in AI answers.
- **Internal-link into blog/other pages** from inside answers, with a "read more here" CTA that opens a NEW tab (never lose the sales page). **Vary the anchor text - never bare exact-match keywords** ("owning your GoHighLevel alternative here", not "GoHighLevel alternative"). A perfect exact-match anchor profile is a spam footprint. One link per answer max; only link LIVE pages (never drafts); skip answers that have no natural home.
- Take **gap keywords the blog doesn't already own** so the FAQ reinforces the site instead of cannibalizing a ranking post (one keyword, one canonical URL).

## 8. Final CTA
**Job:** the last close. Signature line: "The page can't scroll any further, so what's the move?"
**Anatomy:** a two-path close (keep suffering vs take the step), the one CTA, a last risk-reversal tick row, and **the refrain** (the 5-word promise that also seeds the top of the page - "until the calls stop being scary").

## 9. Footer
**Job:** the page's foundation and legal/trust anchor. It is not an afterthought - it carries the parent-company attribution, the legal pages every claim on the page depends on, the contact paths, and the social proof of a real human behind the brand. Design it deliberately.
**Anatomy (4 columns + a centered base):**
- **Connect With Us** - a row of social icon links (the founder's real channels: YouTube, X, LinkedIn, Skool, whatever they actually run). Real presence = a real person behind the offer.
- **Product** - the same-page anchors + the primary CTA + a "Read the Blog" link (footer-only, so the blog is crawlable/linkable without stealing fold attention).
- **Legal** - Terms, Privacy, and **Disclaimer** (see below - required the moment you make cost or competitor claims).
- **Contact** - support email, phone (tap-to-call `tel:`), primary domain.
- **Centered base:** the brand lockup (the full gradient wordmark) centered above the copyright, and the copyright naming the **parent company** ("© 2026 OathDriven LLC"), linked to the parent site.
**Hard rules (learned on Allodra):**
- **No leaks.** EVERY footer link that navigates away opens in a **new tab** (`target="_blank" rel="noopener"`). The sales page is expensive to earn; a curious clicker must never lose it. Same-page scroll anchors (e.g. "Run the numbers" -> #calculator) stay same-tab - they keep the reader ON the page, so they can't leak.
- **Pin the visited color.** Footer links must set an explicit `visited:` color equal to their normal color. Otherwise a link the reader has clicked (a legal page, say) renders in the browser's default purple and looks like a broken/odd style next to its siblings.
- **Brand lockup consistency.** The wordmark wears the FULL brand gradient everywhere it appears (nav, footer, clips) - do not gray out a piece of it in one place and gradient it in another.

## Legal pages
**When you make cost claims ("run it on free infrastructure") or name competitors ("cheaper than GoHighLevel"), you MUST ship a Disclaimer page and link it in the footer.** This is the honesty guardrail made load-bearing: the sales copy gets to be bold because the disclaimer is precise. Build three pages (`/terms`, `/privacy`, `/disclaimer`), register each as a public/crawlable route (middleware allow-list + sitemap), and give them a "Last updated" date that is real (a fixed revision date, not a live "always today" - a legal doc that claims it changed today, every day, reads as untrustworthy).
**The Disclaimer must cover, at minimum:**
- **The "free" cost claim, squared up.** The free tiers are real and it's your honest experience, but it is NOT a guarantee of zero cost - it depends on the reader's usage and setup, and any charge comes from the third-party provider directly, at their rates, not from you. The honest promise is "significantly lower than renting, often effectively free," never "free, guaranteed."
- **No affiliation / trademarks.** You are not affiliated with, endorsed by, or partnered with any company you name (the infrastructure providers AND the competitors). All marks belong to their owners; you reference them only for comparison (nominative fair use).
- **No guarantee of results.** Calculator outputs, savings figures, and your own numbers are illustrations, not promises.
- **Not professional advice**, and any metaphor you lean on (Allodra's "title"/"allodial") is plain-English framing, not a legal claim.
- A good-faith accuracy clause + a support contact.

## Recapture layer
**The exit pop is its own mini sales page - always have one.** It offers something the reader canNOT get on the page itself, so it never feels like a redundant repeat of the page's message. Treat it as a second, tiny offer with its own hook (Sierra-6's is a free "Intel Brief" report that is never mentioned or sold anywhere on the page).
**Template:**
```
WAIT - don't leave without [the Report / Case Study / Cheat Sheet].
- [benefit] so that you can [outcome]
- [benefit] so that you can [outcome]
- [benefit] so that you can [outcome]
[one field: email]  [get it -> button]
```
Pair it with an always-on chat widget (see FAQ). Run both whenever traffic is paid and every lost visitor is expensive.
**Two triggers, arm after a short dwell, fire once per visitor (localStorage):**
- **Desktop:** cursor exits through the top of the viewport (toward the URL bar / tabs).
- **Mobile:** a fast scroll back UP while near the top of the page - the reach-for-the-address-bar tell. (Rule that works: armed, scrolling up, scrollY between 0 and ~300.) Mobile has no mouse-leave, so without this the pop never fires on phones - which is most of your paid traffic.
**Keep the offer's mini-copy from clashing with the page.** If the page teaches "3 simple steps," don't have the pop promise a "9-step roadmap" - reconcile the numbers.
