# 07 · Design Critique — Designer-Parent Panel

*4 simulated senior designers (who are also parents), each with a distinct lens,
critiqued the v2 prototype's craft. The founder's instinct — "the UI isn't super
good yet" — was confirmed, precisely.*

| Lens | Scores | One-line verdict |
|------|--------|------------------|
| Product/UX (IA, hierarchy) | Visual 7 · **UX/IA 4** | "A dashboard, not a tool — read-only chrome leads, actions are buried" |
| Visual/brand (type, identity) | Visual 6 · **Identity 3** | "Seen this exact app 50 times — tasteful default template, not *Lull*" |
| Interaction/motion | Interaction 7 · **Ergonomics 5** | "Timer banner is the best decision; sheet-overuse taxes the 3am moment" |
| Accessibility/inclusive | **A11y 3** · Inclusivity 5 | "'Calm' currently means 'low contrast'; meaning carried by color alone" |

**The confirmation:** the *ideas* score well (timer banner, rhythm ribbon,
category system, toasts+undo, simple mode). The *execution* scores poorly on
hierarchy, identity, ergonomics, and accessibility. The bones are right; the
skin and the reflexes need a real design pass.

---

## Where all four converged (highest-confidence problems)

1. **Card-itis / flat hierarchy.** Everything is an equal rounded card with a
   1px border and shadow → nothing leads. A tired parent needs ONE dominant
   answer. *(UX: "uniform containers destroy contrast." Brand: "border overuse
   kills the calm — pick elevation or outline, not both.")*
2. **The home screen leads with read-only chrome; actions are exiled.** The top
   60% is dashboard; Feed/Sleep/Diaper sit in a bottom strip whose position
   *shifts* when the timer banner appears. Three components (Last-feed tile,
   Next-up card, ribbon) redundantly tell the same feed-timing story.
3. **Generic template look — no identity.** System font + rounded cards + one
   accent = "could be a crypto wallet." "Night-first is asserted, not designed —
   a dark background is a dark mode, not a night concept."
4. **Sheet-overuse vs the 3am reality.** Diaper (highest-frequency event) costs
   2 taps + an animation; nursing routes through a sheet+tab; sheet controls sit
   at the *top* (worst thumb zone). No gestures, no haptics.
5. **Accessibility debt at the core.** Color-only category meaning (WCAG 1.4.1),
   faint text ~2.5:1 (needs 4.5), 10–11px functional text, sub-44px targets
   (header icons, avatars, the per-row trash), a dangerous always-visible delete.

---

## The agreed direction (synthesized)

### Identity: **"a small light in a dark room" — the app is a nightlight**
- The screen is night; the interface is the *glow*. Moon-gold is not a fill —
  it's **emission** (soft outer glow, radial falloff) on the things that matter
  now: the active timer, the next-up state.
- **Kill ~80% of the 1px borders.** Depth via tonal surface steps
  (#141a2e → #1a2338 → #212c46) + a **1px lit top edge** (moonlight from above)
  instead of full outlines. Reserve a stroke for *selected/active* only.
- **One self-hosted display face** (CSP blocks CDNs → embed a subset .woff2):
  a warm humanist sans (e.g. Hanken Grotesk / Bricolage Grotesque) for the baby
  name + hero numbers; system stack for dense data. One typeface kills 60% of
  the generic read.
- **Real type ramp** (~1.25 modular): 32+ display (hero elapsed-time / timer) /
  20 / 15 / 13-quiet / 11-caps-rare. Labels recede; values carry. The running
  timer goes BIG (32–40px tabular) — it's the emotional number at 3am.
- **Time-of-day tints the background** (dusk-indigo → deep night → pre-dawn):
  "night-first" becomes a *behavior*, ownable, not a swatch.
- **The rhythm ribbon is the signature component** — invest here (category-
  tinted marks on a night band, a moon/sun marker riding "now"). It's the App
  Store screenshot and the app-icon DNA.

### Home screen: **answer two questions, then get out of the way**
1. *How long since the last thing?* → ONE hero block: big elapsed-time line
   ("Last fed **2h 15m** ago · next ~3:40") sitting on the rhythm ribbon (the
   only hero surface).
2. *What do I tap to log the next thing?* → big, positionally-stable log
   actions.
- **Cut:** the standalone Last-feed tile + the Next-up card (merged into the
  hero), the "Logging as" bar (→ a small avatar chip in the header).
- Recent activity collapses to 2–3 rows + "see all". Stats/sharing/settings
  move one tap away.

### Interaction: **make the 90% path 1 tap, no sheet**
- **Tap Feed = start nursing immediately** on the alternation-implied side;
  **long-press = other side**. Sheet only for Bottle/Solids.
- **Tap Diaper = log Wet instantly** (undo toast); **long-press = Wet/Dirty/
  Mixed picker under the thumb.** Sleep already nails this pattern.
- While a timer runs, **the banner is the whole UI**: huge timer, L/R toggle,
  full-width Stop at the bottom edge.
- **Haptics** on timer start/stop and undo (separate from reduced-motion).
- **Swipe rows**: left = edit, right = delete-with-undo. Sheet primary buttons
  move to the *bottom*, full-width.
- Toast + banner always name **who/which baby**: "Left · 16m · by Grace."

### Accessibility: **non-negotiables before any launch**
- **Redundant encoding everywhere**: category = color + icon + shape (+ label);
  timeline marks get aria-labels ("Feed, 2:10 AM, left").
- **Contrast to 4.5:1**: raise dim text (~#c4ccdf), demote the faint tier to
  decorative-only; verify category colors as text/border in BOTH themes.
- **Type floor 13px** for functional text (timeline hours 12–13px, captions up).
- **44px minimum targets** (48px for the night action bar); pad hit areas.
- **Safer delete**: no always-visible trash → swipe/long-press + undo.
- **Decouple "accessible" from "simple"**: big-type/high-contrast is a global
  setting; Simple mode stays a separate helper reduction. Human-checked
  translations for care vocabulary.

---

## Priority order for the redesign pass

1. Hero block + merge the feed-timing trio + de-card the layout *(hierarchy)*
2. 1-tap Feed/Diaper + big-timer banner + haptics *(the 3am moment)*
3. A11y non-negotiables (contrast, encoding, targets, delete, type floor)
4. Identity layer: emission accent, lit top edges, display face, ramp
5. Signature rhythm ribbon + time-of-day background *(the ownable moment)*

*Caveat: simulated panel. The direction is consistent and actionable, but real
usability tests (especially with colorblind and ESL caregivers) should verify.*
