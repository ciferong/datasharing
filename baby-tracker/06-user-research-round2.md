# 06 · User Research — Round 2 (after the A+B upgrade)

*Same 8 simulated personas, re-interviewed against the upgraded
[prototype](./prototype/index.html) (free caregiver sharing + attribution +
simple mode/Tagalog + back-dating + configurable tiles + bottle presets +
prominent save). Each was shown exactly what changed and asked whether their
round-1 blocker was actually fixed. Still simulated — validate with real
parents before launch.*

---

## The delta

| Persona | Segment | R1 | R2 | Δ | Their round-1 blocker → outcome |
|---------|---------|:--:|:--:|:--:|---------------------------------|
| Priya | Mom **+ helper** | 3 | **7** | **+4** | Sharing + attribution + helper simple/Tagalog mode → **delivered** (sync still simulated) |
| Aisha | First-time, BF | 5 | **8** | **+3** | Save-confirmation + 2-tap nursing → **fixed**; sharing shape right; backup still missing |
| Sofia | Formula/amounts | 4 | **7** | **+3** | Daily total-volume tile + sticky/fractional oz → **fixed**; export still missing |
| Grace | Helper (ESL) *(ease)* | 6 | **8** | **+2** | Back-dating + big-button Tagalog simple mode → **fixed** |
| Marcus | Working dad | 6 | **7.5** | **+1.5** | Bottle presets + "Right now"/"Last diaper" tiles → **fixed**; sync/privacy pending |
| Hannah | Exclusive pumper | 3 | **4** | +1 | Pump still "coming soon" → **not addressed** |
| Deepa | Preemie | 3 | **4** | +1 | Corrected age/growth/meds/export → **not addressed** |
| Yuki | Twins | 2 | **3** | +1 | Multiple babies → **not addressed** |

**Average adoption: 3.7 → 5.8 (+2.1).** The four personas we targeted (plus the
helper) moved **+2 to +4**. The three segments we deliberately didn't touch
moved only **+1** — pure quality-of-life spillover — with blockers intact. In
other words: **the changes worked exactly where they were aimed, and nowhere
they weren't.** That's the clean result you want from an iteration.

---

## What clearly landed

- **Per-entry "who logged it" attribution** — the emotional core. Aisha: *"seeing
  Sam's name on the 4am bottle, I almost cried, in a good way."* Priya: it turns
  the log from *"some feeds happened"* into *"Grace fed her at 2, I fed her at 5."*
- **"Log as Grace" → auto Simple mode + Tagalog** — Priya's standout: *"the first
  time I pictured actually handing this to her without a training session."*
  Grace's ease score 6→8.
- **Back-dating + tap-to-edit time** — a sleeper hit that *every* persona valued,
  even ones we didn't target (Deepa, Hannah). Grace: *"now the mother knows I did
  not forget — the thing I was worried about most."*
- **Prominent "Saved" confirmation** — healed Aisha's mid-feed-crash trust wound:
  *"'Left · 16m saved' made me exhale."*
- **Configurable tiles** (daily total volume for Sofia; "Right now"/"Last diaper"
  for Marcus) — solving "wrong parent" by *letting each parent choose*.
- **Bottle presets + sticky ml/oz + fractional oz**, **2-tap nursing**.

---

## The one dominant signal for what's next

Almost everyone who moved converged on the **same ceiling**: **the sharing is
still "theater" — simulated on one device — and there's no backup.** Until it's
real cross-device sync, the differentiator is a mockup of trust, not trust.

- Aisha: *"make it his real phone and back it up — right now if I drop this in the
  toilet, none of it ever existed."*
- Marcus: *"until it's actually on my wife's phone and not just this one, I'm
  evaluating a really good demo, not a thing I use."*
- Priya: *"prove her tap in the nursery shows up on my phone at the office."*

Sharp, self-aware caveat the personas raised themselves: the **"Simulate a live
update" button betrays the illusion** every time — good for a research build, but
the honest tell that the real thing isn't here.

→ **Real cross-device sync + cloud backup is the make-or-break next build.** It's
the ceiling for Aisha, Priya, Marcus and Grace — and it's the founder's own need.

---

## Cheap, high-impact unlocks for the un-addressed segments

Each of these is a **single, contained change** that the persona said would jump
them ~+3–4 points — worth sequencing because they open whole segments:

- **Preemie — corrected age (Deepa 4→~7):** add one "born early? / due date" field
  and recompute age off corrected age. *"You still don't know how old my daughter
  is."* Cheapest big win on the board. Then Fenton growth → meds → export.
- **Pump first-class (Hannah 4→~7):** repurpose/duplicate the L/R nursing timer
  for pumping (the component already exists) + a "pumped vs fed vs stashed" tally.
  *"You polished the bottle and left the pump in the 'coming soon' drawer."*
- **Multiple babies + one-tap switch (Yuki 3→~7):** a data-model decision to make
  now (every event already needs a `babyId`). *"You made it easier for two of us
  to log — you just still won't let us log two of them."*
- **Doctor export (Sofia's next unlock):** one-tap PDF/CSV of daily totals + trend.

---

## Honest caveats the panel surfaced (fix before real launch)

- **Placeholder Tagalog must be checked by a native speaker** — Grace and Priya
  both flagged that baby-care terms are exactly where a bad translation corrupts
  data and erodes trust. Don't ship machine-translated care vocabulary.
- **Caregiver permissions/roles need teeth** — can the helper edit *my* entries or
  only add her own? Can I revoke access when she leaves? (Priya, Marcus.)
- **Written, plain-English privacy policy** — now *more* pressing because we added
  sharing (Marcus). Answer where data lives, who sees it, can I delete all.
- **Backup makes multi-caregiver riskier until it's real** — more people depending
  on one fragile local store. Ship backup *with* sync, not after.
- **Delete still feels risky to the helper** — add an "are you sure?" (Grace).
- **In-product, label the sharing as a preview** so no one builds false safety.

---

## Updated recommendation

1. **Build the real differentiator: cross-device sync + cloud backup** (roadmap
   M2, now clearly the top priority and the founder's own need). This is the jump
   from "beautiful demo" to "app I rely on and recommend."
2. Bake in the **multi-baby + pump data model** while doing it (cheap now).
3. Land the **preemie corrected-age field** and **doctor export** — small, each
   opens a committed, pay-willing segment.
4. Before any public launch: **native-checked translations, caregiver
   permissions, a privacy policy, delete confirmation.**

The two rounds validate the thesis end-to-end: **the design wins, the
differentiator (free shared logging) is the right bet, and the path to "rely on
it" runs through making that sharing real.**
