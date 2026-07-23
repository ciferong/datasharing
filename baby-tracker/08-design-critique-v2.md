# 08 · Design Critique — Redesign Verification (v3)

*The same 4 designer-parents from [07-design-critique.md](./07-design-critique.md)
re-reviewed the redesigned [prototype](./prototype/index.html) against their
own original critique. Same personas, same standards, told to "be as tough as
before." This is a verification pass, not a new panel.*

## Scorecard — before → after

| Lens | Before | After | Δ |
|------|:--:|:--:|:--:|
| Product/UX — Visual | 7 | **8** | +1 |
| Product/UX — **UX/IA** | 4 | **7.5** | **+3.5** |
| Visual/brand — Visual | 6 | **8** | +2 |
| Visual/brand — **Identity** | 3 | **5** | +2 |
| Interaction | 7 | **8.5** | +1.5 |
| Interaction — **Ergonomics** | 5 | **7.5** | +2.5 |
| Accessibility | 3 | **7** | **+4** |
| Accessibility — Inclusivity | 5 | 6 | +1 |

**Every score moved up. The four dimensions the panel flagged as weakest
(UX/IA, Identity, Ergonomics, Accessibility) all improved the most** — the
redesign landed where it was aimed, same as the round-2 user-panel result.

---

## What each lens confirmed as genuinely fixed

- **Hierarchy:** *"The screen finally answers the tired-parent question in one
  fixation... that's systems thinking."* Card-itis "actually cured, not just
  reduced" — tonal steps + lit top edge is called "a more sophisticated dark-mode
  move than 1px borders everywhere."
- **Identity:** *"Emission-as-accent is the single best move in this pass...
  the concept finally showing up in a rendering technique, not just a color
  choice."* The ribbon+moon motif is named as "the closest candidate" for an
  ownable mark.
- **Interaction:** *"Nurse as a toggle... collapses the highest-frequency,
  most time-critical action from sheet→tab→side→start down to one tap."*
  *"The core promise of 'invisible logging' finally delivered."*
- **Accessibility:** *"This was my #1 ask and it's genuinely solved"* (redundant
  shape+color+label encoding). Delete is now called "safe."

## What's still flagged — the next punch list

Ranked by how many lenses independently raised it:

1. **Simple mode ≠ Accessible mode (accessibility, unresolved — was explicitly
   called out as "not addressed").** Bigger-targets/high-contrast is still fused
   to "hide the timeline, act like the helper." A low-vision *primary* parent
   can't get large-type without losing their stats; a fully-sighted helper who
   just wants fewer buttons is stuck with jumbo everything. **Fix:** split into
   two independent settings — accessibility (contrast/type/targets) and Simple
   mode (reduced content) — decoupled from caregiver identity.
2. **List-row edit/delete is now the slowest interaction in the app, by
   contrast** (interaction). Nurse/Diaper are 1-tap; fixing a mislogged entry
   still routes through tap→sheet. **Fix:** swipe-left = edit, swipe-right =
   delete-with-Undo, reusing the trusted Undo pattern already in place.
3. **Bottle sheet's CTA still isn't pinned to the bottom** (interaction,
   confirmed unchanged) — the one sheet parents still open regularly keeps a
   two-handed reach at 3am. **Fix:** sticky bottom "Log bottle" button; let the
   stepper/presets scroll underneath.
4. **Discoverability of the new gesture layer** (product/UX): long-press for
   "other side" / the diaper picker is invisible beyond microcopy — risky for
   a helper in Simple mode who never learns it exists.
5. **Contrast is asserted, not measured** (accessibility) — run the actual
   surface/text token pairs through a real WCAG checker (both themes) before
   calling it done; also add OS dynamic-type support, not just a fixed px floor.
6. **Glow is becoming the new "one accent pop"** (visual/brand + product/UX,
   raised independently by both): hero number, timer, Stop button, *and* the
   moon marker all glow now — "pick one glow" / verify gold-glow "recurs enough
   to feel like a motif, not a moment," without sliding back into decoration.
7. **Typeface still isn't expressive** (visual/brand): `ui-rounded` (SF Rounded)
   was the honest, CSP-safe choice, and it's graded as "a nice default, not a
   distinctive one" — *"does not read Lull."* Docked Identity to 5/10 for this
   specifically. Real differentiation here needs a self-hosted custom face,
   which is a real engineering task (subset a .woff2, embed as a data URI) worth
   scheduling once the product direction is locked.
8. **Localization is now honestly labeled, not fixed** (accessibility) — a
   Tagalog-preferring caregiver still can't rely on it today; native review is
   still an open task, just no longer silently shipped as trustworthy.
9. Category shape-language (circle/bar/diamond) "needs to prove out beyond the
   ribbon" — extend it to stat icons, chips, and the activity-list glyphs so
   it reads as a system, not a one-screen flourish.

---

## Read on this result

Two consecutive verification loops (user-panel round 2, designer-panel v2) both
show the same pattern: **targeted fixes move the targeted scores, hard, and
leave what wasn't touched honestly flagged rather than accidentally fixed.**
That's a healthy signal about how this prototype is being iterated.

The punch list above is now small, concrete, and mostly cheap (a settings
split, a swipe gesture, a sticky CTA, a contrast audit) — good candidates for
a fast follow-up pass. The one genuinely bigger item (a real custom typeface)
is worth scheduling deliberately rather than rushing.

*Caveat: still a simulated panel — validate the accessibility claims in
particular with a real screen-reader and low-vision pass before launch.*
