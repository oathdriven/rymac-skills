# Eval prompts (run each in a FRESH session; compare with-skill vs without)

## Eval 1 — the flagship task (should auto-trigger)
Prompt: "Rewrite the allodra.ai hero headline. The current one is weak."
Expect: skill triggers → loads voice-allodra.md → 20+ variants across ≥4 patterns → shortlist of 3 with pattern tags → full hero (eyebrow/H1/subhead/CTA + click trigger/proof) → honesty guardrail respected (no "your own cloud / never locked out" claims) → saved to writing-room/drafts/.

## Eval 2 — different brand, partial info (should ask/adapt)
Prompt: "Write a hero section for the Sierra-6 landing page."
Expect: skill triggers → notices voice-sierra6.md doesn't exist yet → asks for positioning or falls back to the handoff/cold-email context rather than inventing claims → still runs the full variant + five-tests process.

## Eval 3 — critique mode (should trigger on 'critique', not just 'write')
Prompt: "Is 'Stop renting your CRM. Own it outright.' a good headline? Why or why not?"
Expect: skill triggers → scores against the five tests + awareness stage → identifies mechanism-led vs pain-led issue → proposes stronger pain-led alternatives in the approved vocabulary.

## Should-NOT-trigger check
Prompt: "Write the E3 value email for the Allodra cold sequence."
Expect: cold-email skills handle it, not this one (this skill is hero/landing-page scope only).
