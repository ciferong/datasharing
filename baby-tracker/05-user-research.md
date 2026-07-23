# 05 · User Research — Simulated Parent Panel (Round 1)

*A simulated/synthetic study: 8 AI-personas, each interviewed independently
(blind to the others) against the [Lull prototype](./prototype/index.html).
These are directional signals to prioritize real work — not a substitute for
testing with real parents, which we should do before launch.*

**Method:** 8 distinct caregiver personas, one moderated concept/usability
interview each, structured output (first impression → walkthrough → ranked
frustrations → gaps → delights → switch/pay → verbatim quotes → score).

---

## Executive summary

The **design and taste are validated** — every single persona praised the
night-first calm look and the one-tap interactions, unprompted. As one put it,
*"I can tell the team is good."* The gap is **not craft — it's workflow
coverage.** Adoption scores are low today (avg ≈ **3.7/10**) for one repeating
reason: **the feature each person needs to *rely* on it is the part that isn't
built yet.** Latent willingness is high — most said they'd switch *and pay* the
day their blocker ships.

The clearest strategic confirmation: **free multi-caregiver sharing is the #1
blocker and the #1 opportunity**, named by the majority and disqualifying for
the household-with-helper user — which is exactly our founder's case.

### Adoption scorecard

| Persona | Segment | Score | Their one blocker |
|---------|---------|:---:|-------------------|
| Marcus | Working dad, "not another app" | **6/10** | No partner sync; wants status, not totals |
| Grace | Domestic helper (ESL) *(ease score)* | **6/10** | Can't log at an earlier time; colors unlabeled |
| Aisha | First-time, exclusively breastfeeding | **5/10** | No save-confirmation trust; no sharing/backup |
| Sofia | Formula, tracking amounts for doctor | **4/10** | No daily **total volume**; oz entry friction |
| Priya | Working mom **+ live-in helper** | **3/10** | Sharing/attribution/simple-mode not built |
| Deepa | **Preemie** / NICU grad | **3/10** | No corrected age; growth/meds/export missing |
| Hannah | Exclusive **pumper** | **3/10** | Pump is "coming soon," not first-class |
| Yuki | **Twins** | **2/10** | Only one baby supported |

---

## What's working — protect these

Consistent, unprompted praise across very different users:

- **Night-first dark design.** Universal. *"Someone who's been awake at 3am
  designed this."* This is our validated signature — do not water it down.
- **One-tap Sleep (→ "Wake") and one-tap Diaper (Wet/Dirty/Mixed).** Repeatedly
  called the best interactions. Grace (ESL): *"This one I press with no thinking."*
- **Nursing timer that survives lock/reload.** Aisha: *"the most important
  sentence in this whole app."*
- **The "next feed" prediction *with a why-line*.** The transparency earns
  trust even from skeptics — *"it tells me it's a guess."*
- **Undo on delete**, and the **Recent-activity list in words** (easier than the
  color ribbon for the ESL caregiver).

**Takeaway:** the UX foundation is right. Keep it; close the workflow gaps around it.

---

## Findings, severity-ranked

### 🔴 Blockers (lose whole users/segments)

**1. No real-time multi-caregiver sharing — and data is local-only.**
Named by Priya (disqualifying), Marcus (dealbreaker), Aisha, Grace, Deepa.
This is simultaneously the top complaint *and* our core differentiator *and*
our founder's exact need. The single-device storage also reads as a **data-loss
risk** ("one dropped phone and weeks are gone"). Grace couldn't even understand
*how* the mother would see her daytime logs.
→ **Do first (roadmap M2), and pull backup/sync forward.** Free sharing + "who
logged it" attribution + cloud backup.

**2. Entire segments have no home:**
- **Pump isn't first-class** (Hannah, dealbreaker; Aisha wants it now). Painful
  irony: the L/R **Nursing timer *is* the pumping UI** — just relabel/duplicate it.
- **No multiple babies** (Yuki, near-disqualifying for twin/sibling parents).
- **No preemie model** (Deepa): no gestational-age/corrected-age concept, and
  Growth (Fenton) + Meds are "coming soon."
→ **Decide the data model for pump + multi-baby NOW** (cheap to design in early,
expensive to retrofit). See "Design-in-now" below.

### 🟠 High-impact, low-effort (quick wins)

**3. Can't back-date an entry — everything logs at "now."**
Grace's #1, and a daily stress: she logs 20–30 min late, so the mother sees
wrong times and Grace fears looking careless. Small build, big trust payoff —
especially for the *helper*, our actual co-user. Add a quick "how long ago?
now / 15m / 30m / 1h / custom" on every log.

**4. Make "Saved" unmistakable.**
Aisha's #1 trust issue after being burned by a laggy tracker. *(The prototype
does show a toast — so this is about making save-confirmation prominent and
explicit, e.g. echo "Left · 16m saved," not adding it from scratch.)*

**5. The summary tiles show the wrong thing for several users.**
- Sofia (medical): **no daily total volume** — her one must-have number is
  absent. *"I need to know she drank 24 ounces today, and this app won't tell me."*
- Marcus: wants **"last diaper" and current awake/asleep state**, not daily
  totals — *"a scoreboard I don't need at 2am."*
- Priya/Deepa: want **wet vs dirty breakdown** (what the doctor asks).
→ Make the stat tiles **segment-aware or user-configurable**; add total-volume
and current-state options.

**6. Nursing takes too many taps to start.**
Aisha: Feed → Nursing tab → side → Start = up to 4 taps with a screaming,
latching newborn. Let users **start the timer first and confirm the side after**,
or start a feed timer straight from the bottom bar.

**7. Bottle entry friction.**
Marcus wants **quick-pick presets** (120/150/180) over a stepper. Sofia (US)
wants the **oz preference to stick**, **fractional (0.25 oz) increments**, and
ideally **direct number entry** — and questions why the default is 120 ml.
→ Persist unit choice; finer increments; presets; allow typing.

**8. The color-coded timeline isn't self-explanatory.**
Grace (ESL) couldn't decode coral/periwinkle/aqua and would ignore it; Aisha
wanted a legend. *(A legend exists below the ribbon — so this is about putting
words/icons closer to the marks and a "simple mode."*) Also flagged: **density**
on a real 10+-feed newborn day, and taps landing on the wrong mark.

### 🟡 Important, larger scope (mostly already on the roadmap)

**9. Preemie support (Deepa):** gestational-age input + **corrected-age** shown
everywhere; **Fenton** growth curves (pre-term) then corrected-age WHO; med
logging with dose/time + reminders. The roadmap already *names* Fenton — she
noticed and appreciated it; it just needs building.

**10. Doctor-ready export (Sofia, Deepa):** one-tap PDF + CSV over a date range,
with daily-totals and trends. Roadmap M4 — validated as a *paid-tier-worthy* need.

**11. Predictions: relevance + tone.** Assume a typical *cued-feeding* baby, so
they feel off for **scheduled feeders** (preemie/formula) and miss what pumpers
want (**"next pump" / supply runway**). Must never feel **naggy or judgmental**
when the baby is off-schedule; allow **mute/dismiss**.

**12. Plain-language privacy answer (Marcus):** where does baby data live once
sharing arrives, is it ever sold, can I delete everything. Answer it in-product.

**13. Simple/large-button mode + localization for the helper (Grace, Priya).**
Not a "later" nicety — it's what makes the app usable in a household with a
less app-savvy, ESL caregiver, i.e. our core scenario.

---

## Two things to design-in *now* (cheap early, costly later)

Even though these ship later, the **data model** should assume them from the
next build so we don't rework everything:

1. **Multi-baby:** every event already needs a `babyId` — make "baby" a
   first-class, switchable entity now, even if the UI initially shows one.
2. **Pump as a first-class event type** (milk *out*), distinct from bottle
   (milk *in*) — enabling Hannah's supply-vs-consumption ledger later. The
   nursing-timer component is reusable for it.

Also cheap to bake in: **editable/back-dated timestamps** on every event, and
**gestational age / due date** on the baby profile (unlocks corrected age).

---

## How this reshapes the roadmap

- **Confirms M2 (free sharing) as the top priority** — it's the recurring
  blocker and our differentiator. **Pull cloud backup forward** with it.
- **Adds cheap, high-trust wins to M1** that weren't scoped: back-dating,
  prominent save-confirmation, configurable tiles (incl. daily total volume &
  current state), nursing quick-start, bottle presets/oz persistence, timeline
  labels + a simple mode.
- **Elevates "simple mode + localization for the helper"** from "later" to core.
- **Make the multi-baby + pump data-model decision before the next build.**
- Growth (**Fenton**/corrected-age), meds, and doctor export (M3–M4) are
  validated as real, **pay-worthy** needs — especially for medical/preemie users.

## Representative quotes

- *"This is the prettiest logging app I've ever seen for a problem I don't have.
  My problem is my helper, and she's not in here yet."* — Priya
- *"If my wife can't see what I logged, what did I even log it for?"* — Marcus
- *"Many times I remember only after half hour. If the app write 'now', the
  time is wrong, and the mother think I forget."* — Grace
- *"You built the exact screen I need — L/R and a timer — and pointed it at the
  one thing I can't do."* — Hannah (pumper)
- *"It thinks my baby is three months old, and he's really about three weeks.
  That one wrong number colors everything."* — Deepa (preemie)
- *"One 'next feed' card for two babies isn't helpful, it's a trap."* — Yuki (twins)

---

*Caveat: personas are simulated. Treat as hypothesis-generation and
prioritization input; validate the top findings with real caregivers (and a
real domestic-helper co-user) before committing the roadmap.*
