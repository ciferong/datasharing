# 11 · Design Critique — Colour Panel

*Five simulated UI designers, each with a distinct colour lens, independently
reviewed the current [prototype](./prototype/index.html) — the one just through
the "de-noise" pass (grey shortcut row, softened prediction tiles, muted
timeline, fixed reveal slabs). Each read the actual token blocks and usage; the
accessibility and dark-mode reviewers computed real WCAG ratios in a terminal.
Still simulated — validate with a real screen-reader / low-vision pass and real
colour-blind users before locking a palette.*

The five lenses:

1. **Colour & design-systems** — palette cohesion, hue harmony, token architecture
2. **Accessibility & inclusive colour** — computed WCAG contrast + colour-blindness
3. **Brand & emotional design** — what the palette *says*; distinctiveness
4. **Dark-mode / theming** — the 3am case: elevation, saturation, glow
5. **Product visual / hierarchy** — does colour lead the eye on the home screen

---

## Aggregate scorecard

| Dimension | Score | Who / note |
|---|:--:|---|
| Palette cohesion | 6/10 | Lovely warm-neutral ground; the 3 category hues don't belong to it |
| Hue harmony | 5/10 | Real collisions: accent≈feed, success≈diaper |
| Semantic/category logic | 4–5/10 | Weakest axis — delete wears "feed", accent doubles as "misc" |
| Token architecture | 6/10 | Good layering; 4 hand-synced blocks; "gold" token is actually orange |
| **Light-mode a11y (category colour)** | **FAIL** | feed/diaper used as *text* at ~2:1; every category mark <3:1 |
| Dark-mode build | B/B− | Thoughtful; **surface elevation ramp is crushed** (s0→s1 = 1.03:1) |
| Colour hierarchy | 6/10 | Loudest colour is on the *retrospective* hero, not the *actionable* tiles |
| Emotional fit | 7/10 | Genuinely calm; but wearing a "sunrise" costume for a bedtime brand |

---

## Where they agreed (ranked by how many raised it)

**1. The accent orange IS the feed orange. (all 5, unanimously the #1 hit)**
`--gold #f0713a` (hue ~17°) and `--feed #ff7a45` (hue ~17°) are the same orange;
`--gold-text #bd4515` too. When the predicted action is a feed, the top of the
screen stacks *rust hero number → gold-washed tile → orange feed icon* — three
warm oranges in a column, and hue can't tell "brand accent" from "feed
category." **Worse in dark:** `--gold #ffb37a` and `--feed #ffab7a` are nearly
identical. Only *form* (large text vs. small fill) currently rescues it.

**2. Light-mode category colours fail WCAG — including as literal text. (a11y, corroborated by all)**
Computed, light theme:

| Use | Pair | Ratio | Need | |
|---|---|:--:|:--:|:--:|
| "Switch back" button text (helper-facing) | diaper `#2bc48a` on s1 | **1.98** | 4.5 | ❌ |
| Timer "Switch" / danger-CTA label | feed `#ff7a45` text | **2.3** | 4.5 | ❌ |
| Timeline node icons on their 15% tint | feed/sleep/diaper | **1.8–2.8** | 3.0 | ❌ |
| Stat dots / legend on surfaces | feed/diaper | **2.0–2.6** | 3.0 | ❌ |
| (sleep dot is the only category mark that clears 3:1) | sleep `#8a6ff0` | 3.30 | 3.0 | ✅ |

The `:root` comment claims "every pairing WCAG-verified" — true for text/CTAs,
**false for every category token.** Dark theme, by contrast, is clean (all pass).

**3. The prediction tiles over-corrected to grey. (systems, hierarchy, brand)**
The de-noise softened the tile wash to 7% + muted the lead to `--dim`. But the
tiles are the *primary "do this next"* moment — the hero of the interaction —
and they're now the palest thing on screen. Worse (hierarchy): the **"Ready" vs
"in ~40m" urgency carries zero colour**, so an overdue action and a not-yet-due
one look identical. Quieting was right *everywhere it happened* except here.

**4. The diaper green is the palette's outlier. (systems, dark-mode, a11y)**
`--diaper #2bc48a` is the coldest, most saturated, "clinical-scrub" hue in a soft
warm field — reads "medical app." On the dark ground it's the one hue that
"vibrates" (green-on-violet-black). And under red-green colour-blindness, **feed
(orange) and diaper (green) collapse into the same muddy yellow/tan** — the
classic deuteran/protan confusion; the app is saved only by its shape+label
backup.

**5. Semantic reuse bugs. (hierarchy, systems)**
- **Delete/danger paints in the feed hue** (`.sw-del`, `.cta.danger`) — "delete
  wears feed" in a feeding app.
- **`--good` success-green ≈ `--diaper` green** — diaper wears "go/confirm."
- **The accent doubles as the "misc/other" category** (`.node.other`,
  `colorFor` fallback for bath/meds/temp) — so health events like meds/temp get
  the generic brand accent instead of a distinct signal.

**6. Dark surface elevation ramp is crushed. (dark-mode)**
Computed steps `--bg #181022 → s0 #1f1629 → s1 #221830 → s2 #2b1f3d`: the
**s0→s1 step is 1.03:1** — below perception on OLED at low brightness. The
recessed timeline track and the card it sits in are tonally the same colour;
elevation is carried entirely by a 7%-alpha hairline. (`#181022` as the ground
is the *right* call, though — a violet near-black, correct for OLED/halation.)

---

## The one real disagreement: **Dawn vs. Dusk**

This is a genuine fork, and it's a founder call — the fixes above apply either way.

- **Keep "Refined Dawn"** *(colour-systems)*: the peach-horizon-into-lilac-sky
  gradient (`--bg-glow #ffe9d6` → `--bg #f6eef9` under plum ink `#2b1f3d`) is
  genuinely distinctive — *nobody* in baby-tech owns peach-into-lilac (they're
  all mint/teal/navy clinical). Make the accent a softer **rose-coral**
  (`#ef7a5e`) so the brand becomes an ownable *"coral over lilac"* warm/cool
  pair, and fix the collisions. Stays warm, friendly, cozy.

- **Pivot to "Dusk"** *(brand)*: "Dawn is when the baby *wakes up*." The
  emotional job — soothing back to sleep at 3am — is a **dusk** job, and peach is
  a stimulation/morning colour. The app's best asset (`#181022` plum-black dark
  mode) should be the brand's *home*, not a mode; the signature hue should be the
  **sleep-periwinkle you've demoted to a category dot** (`#8a6ff0` → `#7C6DE0`),
  promoted to the one "happening right now" glow, with a single warm **lamplight
  amber** (`#F2B65C`) as the one point of light in the dark. Cool ground + one
  warm glow = a nightlight, and it's the opposite of every competitor.

Both are defensible. Dawn is lower-risk and keeps the warmth the founder likes;
Dusk is bolder, more ownable, and more on-name — but a bigger change and it
leans dark-first.

---

## No-regret fixes (do these regardless of the fork)

All values below computed and verified (WCAG text 4.5 / graphic 3.0, light theme;
dark tokens already pass):

1. **Recolour the light-mode category tokens** to clear contrast everywhere:
   - `--feed: #c23a1a` (redder orange — text 5.3:1; also steps away from the accent)
   - `--sleep: #6b4bcc` (deepened — text 5.9:1)
   - `--diaper: #0f7a72` (**teal** — text 5.1:1; fixes the colour-blind feed↔diaper collapse, raising CVD separation ~80→~122)
2. **Break the accent↔feed collision** — with feed moved redder above and the
   accent reserved for large text/CTA, they stop reading as one hue. (Or, if you
   take the Dusk fork, the accent leaves orange entirely and the problem dissolves.)
3. **Give destructive its own token:** `--danger: #c62233` (white-on-fill 5.7:1),
   used by `.sw-del` and `.cta.danger` instead of `--feed`.
4. **Separate success from diaper:** move `--good` to a blue-green
   (`#0d7a6e`-ish) or drop green-success entirely; reserve green(→teal) for diaper.
5. **Bring warmth back to the prediction tiles** (wash ~12%, warm) **and encode
   urgency in colour** — the most-due tile gets a stronger category tint /
   coloured lead so "what next" is *seen*, not just read.
6. **Rebalance the home-screen colour budget:** drop the **stat dots to `--faint`
   grey** (you read the strip by its numbers — the dots decide nothing) and
   **desaturate the repeated timeline node glyphs** (full-saturation ×13 rows
   dilutes meaning) — spend the freed colour on the primary prediction tile.
7. **Widen the dark surface ramp** so elevation is perceptible:
   `--bg #171021 · s0 #221733 · s1 #2b1e40 · s2 #372a4e` (even ~1.09–1.18 steps;
   all text still passes).
8. **De-collide `--gold`/`--gold-text` in dark** (currently identical) — give the
   text role a slightly different value so fill vs. inline text differ in both themes.
9. **3am safety:** light-mode `--s1 #fffefb` is a ~99%-luminance retina flash in a
   dark room, and dark is gated on the OS setting. Use the `data-tod` clock you
   already compute to **default/auto-suggest dark at night** (or dim light-mode
   `--s1` after dark), rather than only tinting a dark ground.
10. **Token hygiene:** rename `--gold*` → `--accent*` (it's orange, not gold);
    collapse the 4 duplicated light/dark blocks to one source each to stop drift.

**Minor/optional:** trim the live-timer glow for the long nursing dwell
(`--glow` .3→.22, 18px→14px); optionally soften dark body text `#f7f0fb`→`#e8dff0`
to cut halation.

---

## Recommendation

The **no-regret list is the priority** — items 1–4 include genuine accessibility
*failures* and semantic bugs that should be fixed no matter the brand direction,
and they're small, mechanical, and already verified. Items 5–6 recover the
"friendly, not flat" the founder wants without reintroducing noise (fix the
*root* of noise — three clashing hues in tiny marks — instead of desaturating
everything). Item 9 is a real product decision for a 3am-first app.

Then make the **Dawn-vs-Dusk call deliberately** — it's the one thing that
changes the app's identity, and both paths are good. Everything else is polish
on top of whichever ground you choose.
