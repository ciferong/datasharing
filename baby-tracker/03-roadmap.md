# 03 · Roadmap

*The build order, sized for one non-technical founder building with AI help. Each
milestone is a thing you can actually open on your phone and feel — we never
build for months without something to hold.*

Guiding rule: **get a real, tappable app on your phone as fast as possible, then
make it excellent one layer at a time.** Ship the foundation before the flourishes.

---

## M0 · "Hello, it runs on my phone" *(smallest possible start)*

**Goal:** prove the setup works — you can see a live app on your own phone.

- Scaffold the React Native + Expo project.
- One screen with the bottom **Feed / Sleep / Diaper** bar that does nothing yet.
- You scan a QR code and see it running on your phone (Expo Go).

**Done when:** you're holding your phone looking at *your* app. No features
needed — this de-risks everything else.

---

## M1 · Flawless manual logging (local-first) *(the foundation)*

**Goal:** the core loop — log fast, one-handed, offline, never lose data.

- Baby profile (name, DOB, units).
- Log **feeds** (nursing L/R timer that survives lock/background, bottle, pump,
  solids), **sleep** (timer + manual), **diapers** (wet/dirty/mixed).
- Local database so everything works offline and instantly.
- The **daily timeline ribbon** + today's totals + active-timer display.
- Edit / delete / log-in-the-past.
- Dark mode.

**Done when:** you could genuinely use it to track a full day solo, offline, and
it feels faster and calmer than PiyoLog. **This is the make-or-break milestone.**

---

## M2 · Free real-time caregiver sharing *(the differentiator)*

**Goal:** you and your helper both log the same baby, live.

- Accounts + baby "spaces."
- Invite a caregiver by link/code; roles (owner vs caregiver).
- Real-time sync of the shared log across phones (offline-first merge).
- **Per-caregiver attribution** on every entry.
- **Simple mode / language toggle** for the helper.

**Done when:** you log a feed and it appears on the helper's phone within
seconds, and vice versa — for free.

---

## M3 · Actionable predictions & insights

**Goal:** the app tells you what's likely next, not just what happened.

- **Next nap window** (wake-windows by age + observed pattern).
- **Next feed estimate**, **longest sleep stretch**, weekly pattern nudges.
- The Insights screen — every item actionable, each explains its "why."

**Done when:** the home screen gives a genuinely useful nudge you'd trust.

---

## M4 · Growth charts + export/import (no lock-in)

**Goal:** doctor-ready, and switching-friendly.

- Log weight/height/head; plot on **WHO / CDC / Fenton (preemie)** percentile
  charts with plain-language readouts.
- **One-tap doctor PDF** + **CSV export**.
- **Import from Huckleberry / Baby Tracker** CSV so you keep old history.

**Done when:** you can hand a clean PDF to a pediatrician and import a friend's
data from another app.

---

## M5 · Polish & platform reach *(fast follow)*

**Goal:** make it feel premium and always-at-hand.

- Home-screen **widgets** (tap to log / see last feed) and **Apple Watch / Wear
  OS** quick-logging.
- Medicine "next dose" reminders, richer health tracking, photos/diary.
- App Store / Play Store release polish.

---

## M6 · Voice + AI (the "wow", added on a solid base)

**Goal:** the force-multiplier — *on top of* excellent manual logging.

- **Voice logging:** "nursed 15 on the left, dirty diaper at 8" → structured
  entries with a review step before saving.
- **AI recall:** "when was the last bottle?", "wet diapers this week?"
- **Pattern Q&A:** "has reflux improved since I cut dairy?"

**Why last:** voice can't work in a silent nursery and needs the reliable manual
foundation + clean data model beneath it. Built here, it's a delight; built
first, it's a liability.

---

## Sequencing logic (why this order)

- **M1 before everything** — if fast, reliable, one-handed logging isn't
  excellent, no feature on top matters. It's also the #1 competitor complaint.
- **M2 next** — free sharing is our sharpest wedge and directly serves the
  you-plus-helper reality.
- **M3–M4** — turn logged data into value (predictions) and trust (charts,
  doctor PDF, no lock-in).
- **M5–M6** — reach and delight, once the core is unshakeable.

Each milestone is independently shippable — you could stop after M2 and still
have something better than most paid apps for a two-caregiver household.
