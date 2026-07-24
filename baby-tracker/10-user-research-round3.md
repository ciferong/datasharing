# 10 · User Research — Round 3 (current build)

*The same 8 simulated personas, re-interviewed independently against the current
prototype — the one that's had the two-tile predictions, the expanded scrollable
shortcut row, real Bath/Meds/Temp logging, and the warmth/density overhaul added
since Round 2. Still simulated; validate with real parents before launch.*

## Scoreboard — R1 → R2 → R3

| Persona | Segment | R1 | R2 | R3 | R3 move |
|---------|---------|:--:|:--:|:--:|:--:|
| Aisha | First-time, breastfeeding | 5 | 8 | **8** | — |
| Priya | Working mom **+ helper** | 3 | 7 | **7** | — |
| Marcus | Working dad | 6 | 7.5 | **8** | ▲ |
| Sofia | Formula / amounts | 4 | 7 | **7** | — |
| Deepa | **Preemie** | 3 | 4 | **5** | ▲ |
| Hannah | Exclusive **pumper** | 3 | 4 | **4** | — |
| Yuki | **Twins** | 2 | 3 | **3** | — |
| Grace | Helper (ESL) *(ease)* | 6 | 8 | **8.5** | ▲ |

**Average adoption: 5.8 → 6.0.** Nearly flat — and *that flatness is the most
important finding in this round.*

---

## The headline: we've hit the ceiling of what polish can buy

Every persona **loved** what shipped this round — the warmth, bigger fonts,
one-tap tiles, real Bath/Meds/Temp, back-dating, the ✓-logged confirmation.
Nobody's UX complaints drove their score this time. And yet the numbers barely
moved, because **every remaining adoption gate is now a missing *capability*,
not a UX problem** — and each is a specific, already-known deferred item:

| Persona | What now gates their score |
|---------|----------------------------|
| Aisha, Priya, Marcus | **Real cross-device sync + cloud backup** (sharing is still simulated on one device) |
| Sofia | **Doctor PDF/CSV export** + **multi-day trend** |
| Deepa | **Corrected age** + **Fenton growth charts** |
| Hannah | **Pump** as a first-class tracker |
| Yuki | **Multiple babies** |

The panel is telling us, in unison: *the prototype has proven the experience;
the remaining points require building the real features.* This is the clearest
signal yet that the next step is **leaving the single-device prototype behind.**

---

## The loudest single signal: make sharing real

**Three of the four highest scorers (Aisha, Priya, Marcus) named real
cross-device sync + backup as the exact thing between them and a 9.** It's the
founder's own need, and Round 3 surfaced a sharper reason it matters than
"partner convenience":

> Predictions are only as trustworthy as the log they're built from. Priya:
> *"If my helper fed the baby at 2pm and the app doesn't know because that log
> never reached me, the tile will be confidently wrong the moment I pick up the
> baby after work."*

So **sync isn't just a feature — it's what makes the prediction feature actually
work in a two-caregiver home.** The two headline capabilities of this product
(free sharing + predictions) are coupled: the second is unreliable without the
first being real. Backup fear was near-universal too — *"three months of feeds
gone if my phone dies?"*

---

## The two-tile prediction: validated, with a real refinement list

The concept landed — *"when it's right, it's the dream"* (Aisha), *"less fuss
than anything else in the app"* (Marcus). But the panel returned a consistent,
actionable set of caveats, several of which complicate the "show two tiles"
decision specifically:

1. **The helper found two tiles *harder* than one.** Grace: *"When there is two
   tiles, I stop and think 'which one is right?' … For a second I feel like the
   app is telling me what to do, and I worry maybe I am late."* She trusts one
   tile more than two, and wants softer, question-framed copy (*"Did you feed?"*)
   so it reads as a guess, not a command. → Consider **one tile in Simple mode,
   two in full mode**, and gentler wording.
2. **One-tap "usual bottle" is risky for exact-amount tracking.** Sofia wants
   **confirm-not-commit**: tapping the bottle tile should open the amount sheet
   *pre-filled* with the usual amount, not silently log it — *"don't let me
   one-tap the usual bottle when the doctor's counting the actual one."* It must
   also respect her **oz** preference (not show ml).
3. **Single-baby prediction is a mis-logging *trap* for twins.** Yuki: a big
   one-tap tile invites fast tapping → logs the wrong twin. *"You gave me a
   faster way to log the wrong baby."* (Resolved only by multi-baby support.)
4. **Off-target for scheduled/rhythm users.** Deepa (preemie) wants
   *schedule-driven* prompts (fixed feed/med times), not history-inferred ones.
   Hannah (pumper) wants the one prediction the app can't make — *"you're due to
   pump in ~20 min"* — because pumping isn't tracked.
5. **Trust is fragile & pattern-based.** Aisha: must be right ~80%+ or it becomes
   clutter in the best screen real estate; growth spurts/cluster feeds are
   exactly when the "typical gap" math breaks and she's most frazzled. Undo on a
   mis-predicted tap is essential (it exists — good).

**Note for the founder:** the two-tile layout was your call, and the panel's
verdict is genuinely mixed — great for experienced solo parents, a step *back*
for the ESL helper (a core user) and a hazard for twins. Worth deciding
deliberately: keep two but make it adaptive (one in Simple mode) and reframe the
copy as a question.

---

## Cheap, high-trust fixes worth doing regardless of the big builds

- **Confirm-not-commit + respect oz** on the bottle tile (Sofia) — protects data
  integrity; small change.
- **Softer, question-framed prediction copy** and **one tile in Simple mode**
  (Grace) — fixes the "is it bossing me?" hesitation for the helper.
- **A plain-language privacy policy in-product** (Marcus) — *"'Free forever'
  makes me more nervous, not less: what's the business model, where does the
  data go?"* Cheap, and a real trust gap now that sharing is being promoted.
- **Med "next dose due" reminder** (Deepa) — logging meds records history but
  doesn't prevent the actual risk (a doubled/missed dose across two caregivers).
- **Diaper hold-hint discoverability** — Grace forgot you can hold for
  dirty/mixed and only ever logged "wet."
- **Native Tagalog review** — still placeholder; Grace and Priya both flag that a
  wrong care-word is *more* confusing than English.

---

## One strategic critique to internalize

Hannah (pumper): shipping **Meds/Temp (used ~twice a month) before Pump (used
~8×/day)** read as a negative signal about how the roadmap is prioritized —
*"you're polishing the app around the exact hole I fall into."* The lesson isn't
"pump next" specifically; it's **weight the roadmap by frequency-of-use**, not by
ease of building.

---

## Recommendation

Three rounds now point the same direction, and Round 3 makes it unambiguous:

1. **Build real cross-device sync + cloud backup.** It's the ceiling for the top
   of the panel, the founder's own need, *and* the thing that makes predictions
   trustworthy in a shared household. This is the single highest-leverage next
   step — and it can't be done in the web prototype, which means it's time to
   **start the real app (Expo + a sync backend).**
2. Alongside it, do the **cheap trust fixes** above (confirm-not-commit, privacy
   copy, adaptive/softer predictions) — they're small and lift the personas who
   are already close.
3. Sequence the **segment-unlocking capabilities** by reach: sync (unlocks the
   3 biggest scorers) → then pick among doctor-export, multi-baby, pump,
   corrected-age/growth based on which segment you most want.

The prototype has done its job. The research is now saying: *stop polishing the
demo, start building the real thing — beginning with sync.*
