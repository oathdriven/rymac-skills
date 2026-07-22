---
name: rymac-call-funnel
description: Builds the conversion plumbing that turns site traffic into scheduled calls: chat scheduler, AI voice agent, emergency escalation that pings a live on-call human, non-emergency booking into one shared calendar engine, and after-hours handling. Use when the user asks to "wire up the call funnel", "add the chat scheduler", "set up the voice agent", "convert traffic into scheduled calls", "handle after-hours calls", or builds any page whose goal is booked calls. Make sure to use this skill whenever call-booking, voice-agent, or emergency-routing plumbing is being designed or built.
argument-hint: [site/business to wire, calendar target, on-call contact]
---

# RyMac Call Funnel

Wire a site to convert visitors into scheduled calls, with a human-ping
path for emergencies. This is the architecture running live on RyMac's own
CRM platform; the pattern works with any stack (a CRM with AI channels, or
Vapi/Twilio + a calendar API wired directly).

## The architecture (one persona, many channels)

One AI persona serves web chat, SMS, and voice. The persona is rebuilt
server-side on every turn from a single profile (business facts, hours,
escalation config), so every channel answers with the same brain and the
same rules.

## Emergency vs non-emergency: it is a COMPOSITE, not a boolean

Do not build a single `if (emergency)` classifier. The proven pattern is
four separable mechanisms, configured per business:

1. **Escalation keywords (the instant human ping).** Case-insensitive
   keyword match on inbound messages ("urgent", "emergency", "complaint",
   "speak to manager", plus the niche's own panic words). On match: the AI
   GOES SILENT and the on-call human is notified immediately with a deep
   link to the contact. Allow per-channel keyword and notify-address
   overrides.
2. **Live transfer (the ring-a-human path).** Phone-system dial forward
   (e.g. Twilio Dial) to the on-call number with a ring timeout (~18
   seconds) and an automatic text-back to the caller if unanswered.
3. **Callback capture (the deferred queue).** Voice calls run a structured
   extraction for "callback requested"; when true, a follow-up task lands
   on the operator's today list plus a notification email. Pure-info calls
   create nothing.
4. **Booking tools (the non-emergency default).** The agent gets
   get-availability / book / reschedule / cancel tools against ONE shared
   calendar-aware booking engine, so chat, voice, and the public booking
   page all see the same availability truth and send the same confirmation,
   invite, and reminders. Never let the model invent slots; hard-rule the
   booking protocol to real availability.

## After-hours (where the money leaks)

Configure explicitly: business hours, after-hours behavior (AI handles and
books vs capture-and-morning-queue), and when the AI hands off. For
emergency-natured niches, after-hours emergency keywords route to the live
on-call ping (mechanisms 1-2); everything else books the morning slot
(mechanism 4). This is the beachhead pitch for any business losing
overnight leads: the morning-missed-leads pile becomes booked calls.

## Build order for a new site

- [ ] Define the niche's emergency vocabulary + the on-call contact
- [ ] Stand up the calendar (who takes the calls, when)
- [ ] Wire chat widget → persona → booking tools
- [ ] Add voice number → same persona → same tools
- [ ] Configure escalation keywords + notify address (+ live transfer if
      the business runs a real on-call)
- [ ] Set after-hours behavior explicitly
- [ ] Test all four paths: panic keyword pings, transfer rings + text-back
      fires, callback request creates the task, normal chat books a real
      slot and the confirmation lands

## Rules

1. AI silence on escalation is a feature: after the ping, the human owns
   the thread. The bot resuming over a live human is the cardinal sin.
2. One booking engine, one availability truth. Two calendars = double
   bookings = dead client.
3. Disclose honestly: the assistant speaks as the business's intake
   assistant, never impersonates a specific human.
4. Every mechanism must degrade safely: failed webhook still captures the
   lead, unanswered transfer still texts back, failed booking still takes
   a callback.
