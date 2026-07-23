# 02 · Product Spec

*What we're actually building. Every feature here answers a specific complaint
from the [market research](./01-market-research.md).*

---

## 1. Design principles (the rules we never break)

1. **Thumb-zone first.** Primary actions (Feed / Sleep / Diaper) live in a fixed
   bar at the bottom of the screen, reachable one-handed. The most common log is
   ≤2 taps from anywhere.
2. **The tap is the save.** A tapped entry is written to the device immediately
   and locally. Sync is a background nicety, never a requirement. Nothing is ever
   lost because a network call failed.
3. **Timers are sacred.** A running nursing/sleep timer survives app
   backgrounding, screen lock, and phone restart. It shows live on the home
   screen (and later, a widget / watch).
4. **Calm at 3am.** A true dark mode, dimmable, large text, no jarring
   animations, no ads. Logging should feel quiet.
5. **Actionable, not decorative.** If a number doesn't help a parent decide what
   to do next, it doesn't get prime screen real estate.
6. **Sharing is free and obvious.** Inviting a caregiver takes one screen.
7. **Your data is yours.** Local by default, exportable anytime, importable from
   competitors, deletable completely.

---

## 2. Core v1 feature set

### 2.1 Logging — the heart of the app

**Feeds**
- **Nursing:** left / right toggle, independent timers per side, one running at a
  time or paused/resumed; presets (e.g. quick-log a 15-min feed); background- and
  lock-safe; optional alarm to switch sides.
- **Bottle:** amount (ml/oz, remembered unit), breast-milk vs formula.
- **Pumping:** left/right amount, duration (helps supply tracking).
- **Solids:** food name (with recent/favorites), reaction note.

**Sleep**
- Start/stop timer *or* manual start–end entry (for sleeps you forgot to start).
- Distinguishes naps vs night sleep automatically by time of day.
- Surfaces **longest stretch** and **total sleep** for the day.

**Diapers**
- One tap: **wet / dirty / mixed**, with optional color/consistency for dirty
  (useful for the doctor and for spotting problems).

**Health & misc**
- Temperature, medicine (name + dose + time, with a "next dose due" reminder),
  symptoms (cough, rash, vomit…), baths, tummy time, notes, and **photos**.

**Every entry:**
- Is timestamped (editable), attributed to **who logged it**, and editable/
  deletable. Quick "log in the past" for the "oh I forgot" case.

### 2.2 The daily timeline (home screen centerpiece)

A horizontal **24-hour ribbon** showing feeds, sleep, and diapers as colored
blocks — the beloved PiyoLog feature, modernized. Scroll back through past days.
Tapping a block opens/edits that entry. Above it: today's running totals and the
current active timer, if any.

### 2.3 Free real-time multi-caregiver sharing *(the core differentiator)*

- The **account owner** (parent) creates the baby profile and **invites
  caregivers** (partner, grandparent, and critically the **domestic helper**) by
  a simple link or code.
- Everyone sees the **same live log**. When the helper logs a feed, it appears on
  the parent's phone within seconds.
- **Per-caregiver attribution:** each entry shows a small avatar/initials of who
  logged it. No confusion about whether the baby was already fed.
- **Roles:** *Owner* (full control, manages members, billing if any) vs
  *Caregiver* (logs and views). Owner can remove a caregiver anytime.
- **Simple mode / localization** for a caregiver who prefers a stripped-down,
  possibly different-language interface — big buttons, fewer options.
- **Conflict handling:** because it's offline-first, two people can log at once;
  entries merge by unique ID and timestamp (see [tech decisions](./04-tech-decisions.md)).

### 2.4 Growth tracking (a quiet, strong differentiator)

- Log **weight, height/length, head circumference**.
- Plot on real percentile charts: **WHO** and **CDC**, plus **Fenton charts for
  preemies** (which almost no competitor offers) — the app asks for gestational
  age at birth to pick the right chart.
- Show the baby's **percentile** and trend, in plain language ("50th percentile
  for weight, tracking steadily").

### 2.5 Actionable predictions (v1, deliberately simple & honest)

Not AI hype — just useful math over the baby's own logged history:

- **Next nap window:** "Baby's usually ready to sleep around **1:10–1:40pm**"
  (based on recent wake-windows by age + observed pattern).
- **Next feed estimate:** "~**2h 15m** since last feed; typical interval ~3h."
- **Last night's longest stretch** and a gentle week-over-week trend.
- **Pattern nudges:** "Feeds have drifted ~20 min later each day this week."

Each prediction states *why* (the pattern it's based on) and never scolds. As the
data model matures we can layer smarter models — but even the simple version
beats "47 total diapers."

### 2.6 Export & import (no lock-in)

- **One-tap doctor PDF:** a clean summary (feeds/sleep/diaper averages, growth
  percentiles, meds, notes) for a date range — designed to hand to a pediatrician.
- **CSV export** of all raw events.
- **Import from Huckleberry / Baby Tracker / others** via their CSV export, so a
  switching parent keeps their history. This is both a kindness and an
  acquisition wedge.

---

## 3. Screen inventory (rough information architecture)

| Screen | Purpose | Key elements |
|--------|---------|--------------|
| **Home / Log** | The 90% screen | Daily timeline ribbon, running totals, active timer, fixed bottom **Feed / Sleep / Diaper +More** bar, prediction nudge |
| **Add-entry sheets** | Fast logging | Bottom sheets for each type; large controls; recent/favorites; "log in past" |
| **History / Timeline** | Browse days | Scrollable day list, filter by type, edit entries |
| **Growth** | Charts | WHO/CDC/Fenton charts, add measurement, percentile readout |
| **Insights** | Actionable summaries | Next nap/feed, longest stretch, weekly patterns |
| **Sharing** | Caregivers | Invite link/code, member list & roles, simple-mode toggle |
| **Baby profile** | Setup | Name, DOB, gestational age (for Fenton), photo, units |
| **Settings** | Control | Dark mode, units, export/import, privacy & data deletion, notifications |

---

## 4. Data model (shape only — details in tech doc)

Local-first, sync-ready. Core entities:

- **Baby** — id, name, date of birth, gestational age at birth (for preemie
  charts), preferred units, photo.
- **Caregiver / Membership** — user id, baby id, role (owner/caregiver),
  display name, avatar, language/simple-mode preference.
- **Event** — the universal log record:
  - `id` (globally unique, generated on-device so it works offline)
  - `babyId`, `loggedByUserId`
  - `type` (nursing | bottle | pump | solids | sleep | diaper | temp | med |
    symptom | bath | note | measurement | …)
  - `startAt`, `endAt` (for timed events), `at` (for point events)
  - `payload` (type-specific: side, amount, unit, wet/dirty, food, dose, value…)
  - `note`, `photoRef`
  - `createdAt`, `updatedAt`, `deleted` (soft-delete), `syncVersion`
- **Measurement** is just an Event of type `measurement` (weight/height/head).

Every event carries a **stable unique id + timestamps** so two devices logging
offline can merge cleanly when they reconnect. See
[04-tech-decisions.md](./04-tech-decisions.md) for the sync/merge strategy.

---

## 5. What is explicitly *not* in v1

To ship something excellent rather than sprawling:

- Voice / AI logging & recall *(comes later — see roadmap)*
- Apple Watch / Wear OS apps & home-screen widgets *(fast follow)*
- Sleep-training *programs* (Huckleberry-style paid coaching)
- Community/social features
- Ads (never)

These are deferred **on purpose**, not forgotten. The [roadmap](./03-roadmap.md)
says when each returns.
