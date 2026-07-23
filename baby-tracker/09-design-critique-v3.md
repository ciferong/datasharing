# 09 · Design Critique — Punch-List Verification (v4)

*Follow-up to [08-design-critique-v2.md](./08-design-critique-v2.md). That
report ended with a 7-item punch list. This round: shipped fixes for the
top items, sent the [prototype](./prototype/index.html) back to the
designer-personas who could verify them, and — importantly — caught and
corrected a process error along the way. Recorded here in full rather than
cleaned up, because the correction is itself a useful result.**

---

## Scorecard

| Lens | v3 | v4 | Δ |
|------|:--:|:--:|:--:|
| **Accessibility** | 7 | **9** | **+2** |
| Inclusivity | 6 | **7** | +1 |
| Product/UX — Visual | 8 | **8.5** | +0.5 |
| Product/UX — UX/IA | 7.5 | 7.5 | 0 (see below) |
| Interaction / Ergonomics (original thread) | 8.5 / 7.5 | *not re-verified — see correction* | — |
| Swipe + sticky-CTA mechanisms (fresh, standalone review) | — | **5 → fix applied, not yet re-scored** | — |

---

## A correction, on the record

Mid-round, I sent the "verify swipe + sticky CTA" follow-up to the wrong
saved agent handle. The reply that came back was from the **product/UX
systems** designer (whose actual prior scores were Visual 8, UX/IA 7.5) —
not the **interaction/motion** designer (Interaction 8.5, Ergonomics 7.5)
I intended. The agent itself caught this: *"My last scores were Visual 8/10
and UX/IA 7.5/10 — not 'Interaction 8.5' and 'Ergonomics 7.5.' ... I never
mentioned a swipe gesture or the Bottle sheet's CTA position — those aren't
things I raised."*

Rather than discard the reply, I evaluated it on its own merits — and it
surfaced a real, unrelated defect (below) that the intended reviewer might
not have caught, because a product/UX systems reviewer thinks about
gesture conventions differently than an interaction/motion reviewer does.
**The interaction/motion designer's swipe-and-sticky-CTA-specific re-score
was never actually obtained this round** — that verification is still
outstanding.

---

## What shipped this round

1. **Simple mode vs. Accessible mode — split.** Two independent
   per-caregiver toggles (fewer-things-on-screen vs. larger-text-and-controls),
   neither inferred from identity, combinable freely, both reflected in the
   status banner.
2. **Contrast measured, not asserted.** Ran actual WCAG ratio math on every
   color-as-text token pair, both themes. Found and fixed real failures:
   light-theme caption text at 2.6–3.05:1 (needs 4.5), and — the sharpest
   catch — the dark-theme toast's Undo button at **1.48:1, functionally
   invisible**, because the toast is an inverted (bg/text-swapped) chip and
   the accent color doesn't survive the inversion without its own token.
   Also caught two avatar-badge fills failing white-text at 3.43/4.30.
3. **Glow scoped to one motif** — "happening right now" (live timer, Stop,
   the ribbon's now-marker) — removed from the idle hero number and generic
   buttons.
4. **Swipe-to-edit/delete** on activity rows, tap still works unconditionally.
5. **Sticky sheet CTAs**, initially on Bottle only.
6. **Discoverability coach-marks** for the long-press gestures.

## What the (correctly identified) reviews confirmed

- **Accessibility reviewer**, re-verifying their own two flagged items:
  *"This is the actual structural fix, not a relabel... This was my top
  flag two rounds running and it's resolved correctly."* On contrast:
  *"Finding those without me having to point at them is a good sign of
  process maturity, not just patching my list."* → **7→9**.
- Same reviewer's new ask: **automated contrast-regression testing** (CI
  linting on the token set), since intent-based review missed real
  failures before — a fair point given the toast bug had shipped once
  already under "we believe we hit 4.5:1."

## What the (mismatched, but valuable) review caught

- **A genuine safety defect in the shipped swipe gesture:** Delete was
  mapped to swipe-*right* — the easier, more natural direction for a
  right-handed thumb — while the safe action (Edit) sat on the harder
  swipe-left. *"You've made the accidental-trigger-easy direction the one
  that deletes a log entry."* **Fixed same-session**: swipe-left now
  reveals Delete (the more deliberate direction), swipe-right reveals Edit.
- **Sticky CTA was a one-sheet patch, not a system rule.** *"Feed/Nurse,
  Diaper picker, Settings, Profile, Edit sheets presumably have the same
  scrollport-vs-CTA relationship and weren't touched."* **Fixed
  same-session**: extended to the Solids, Edit-entry, and Baby-profile
  sheets' bottom actions.
- **Gesture-discoverability debt grew, not shrank** — two long-press
  gestures plus now two swipe directions, four total undiscoverable
  interactions, "in Simple mode this is now four undiscoverable
  interactions." **Partly addressed**: split the coach-mark into two short
  sequential tips covering hold *and* swipe; the underlying thumb-travel
  and stats-strip-relevance concerns from this reviewer's original round
  remain open and untouched (they were never in scope for this pass).

---

## Honest status of the punch list

| Item | Status |
|------|--------|
| Simple vs. Accessible mode split | ✅ Verified fixed (9/10) |
| Contrast (measured) | ✅ Verified fixed, + regression-testing ask logged |
| Swipe-to-edit/delete | ✅ Shipped; direction-safety bug caught and fixed; **not yet re-verified by a fresh review** |
| Sticky CTA (system-wide) | ✅ Shipped, extended beyond Bottle; **not yet re-verified** |
| Discoverability of gestures | 🟡 Partly — two tips now cover 4 gestures; still no persistent visible affordance |
| Localization (Tagalog) | ⬜ Unchanged, still placeholder, still honestly labeled |
| Dynamic type | 🟡 Scoped honestly as a web-prototype stand-in (zoom lever); real OS Dynamic Type is a native-build task |
| Typeface | ⬜ Deliberately deferred (per v2 report) |
| Contrast-regression CI | ⬜ New ask from this round, not yet actioned |

## Follow-up: a fresh, targeted interaction review

Since I couldn't resume the original interaction/motion reviewer (no live
handle survived), I spun a new one for a first-look, standalone critique of
specifically the swipe gesture and sticky-CTA pattern — framed honestly as
a fresh review, not a continuation. It scored the pair **5/10** and named
the real remaining risk precisely:

> *"Undo is a good safety net, but it's being asked to be the only safety
> net for a destructive action triggered by a small, easily-crossed
> threshold, in the exact usage context — one-handed, sleep-deprived, low
> light — most likely to produce false-positive drags."*

**Fixed same-session.** Delete no longer fires on drag-release. Swipe-left
now only *reveals* the Delete button; nothing is deleted until a distinct,
separate tap on it. Swipe-right (Edit, non-destructive) still auto-fires,
since there's no harm in that half firing directly — this was the
reviewer's own suggested split. Only one row can be revealed at a time.

The same review raised several other concerns — viewport jank from `vh`
vs `dvh`, missing safe-area padding, a gesture conflict with a
drag-to-dismiss sheet gesture, disabled-CTA states appearing tappable. I
checked each against the actual code rather than patching on faith:
**`dvh` is already used throughout** (not `vh`), **`env(safe-area-inset-bottom)`
is already applied** on every sticky CTA, **no drag-to-dismiss gesture
exists** on sheets (close is via scrim-tap/Escape/explicit buttons only —
so that conflict can't occur), and **no sticky CTA in this prototype is
ever disabled**. These read as reasonable assumptions from a reviewer
working off a written mechanism description rather than the source —
recorded here as verified-non-issues, not silently dropped.

## What's still genuinely open

- **A real re-score from the *original* interaction/motion reviewer**,
  now that the direction-safety bug is fixed — still not obtained; no live
  handle to that specific thread survived this round.
- **Delete-panel color** reuses the "feed" category hue for a destructive
  action — a legitimate collision the product/UX reviewer named. Not
  fixed this round; needs a dedicated danger token, deferred rather than
  rushed.
- **Keyboard-interaction with the Baby-profile sheet's sticky CTA**
  (the one sheet with text inputs) — a known cross-browser rough edge for
  `position: sticky` bottom elements when the OS keyboard opens. Needs
  real-device testing; flagged as a native-build concern rather than
  solved here.
- Thumb-travel loop, stats-strip relevance, contrast-regression CI,
  Tagalog native review — unchanged from earlier, still open.
