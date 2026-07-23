# 01 · Market Research

*What the competition does, what parents love, and — most importantly — what
they complain about. Every design decision in [the product spec](./02-product-spec.md)
traces back to something on this page.*

---

## The landscape at a glance

| App | Origin / model | Loved for | Weakness we exploit |
|-----|----------------|-----------|---------------------|
| **PiyoLog** | Japan · free | Comprehensive tracking, one-handed use, the daily **timeline bar**, growth curves, real-time sharing, tracks *everything* (feeds, sleep, poop/pee, temp, baths, walks, rashes, meds…) | Dated UI, **no predictions or smart insights** |
| **Huckleberry** | US · freemium | Best **sleep-window predictions** ("SweetSpot"), detailed left/right nursing timers, actual sleep *plans* from your data | The good sleep help is **behind a subscription** |
| **Nara Baby** | US · free | Best **free traditional tracker** — every feature unlocked, no ads, caregiver sync, schedulable sleep windows | **No predictive/AI** features; traditional |
| **Robin Baby** | US · freemium | **Voice-first AI** logging & recall, Wear OS, WHO percentile charts, doctor-ready PDF, CSV **import from competitors** | Newer; AI transcription accuracy varies; needs review step |
| **Glow Baby** | US · freemium | Solid basic tracking, polished | Best features + sharing **locked behind subscription tiers** with weak value |
| **Baby Tracker** (classic) | US · freemium | Proven free **solo** tracking, reliable | **Sharing hits a paywall immediately** |
| **Baby Daybook** | freemium | Smart nap & bedtime **suggestions** from patterns | Cluttered; freemium gating |
| **Tinylog** | freemium | One of the few with **WHO *and* Fenton (preemie)** growth charts | Narrow scope |
| **Baby Connect** | US · paid | Deep multi-caregiver history, long-established | Dated UX, paid |
| **ParentLove** | freemium | One-tap **pediatrician PDF** with customizable averages | Smaller, less known |

---

## What the best apps get *right* (our table stakes)

These are the things we must match or beat just to be taken seriously:

- **The daily timeline bar (PiyoLog).** A single horizontal ribbon of the day
  showing feeds/sleep/diapers at a glance. Universally loved. We do this.
- **Left/right nursing timers with presets & alarms (PiyoLog, Huckleberry).**
  Must keep running in the background and while the screen is locked.
- **Real-time sharing between caregivers (PiyoLog, Nara, Baby Connect).**
  Both parents (and the helper) see the same live log.
- **Growth charts with real percentiles (Robin, Tinylog, Child Growth Tracker).**
  WHO + CDC, and **Fenton for preemies** — a real differentiator few offer.
- **Doctor-ready export (Robin, ParentLove).** One-tap PDF summary + CSV.
- **No-lock-in import (Robin).** Import CSV/Excel from Huckleberry and others so
  switching costs nothing — a powerful acquisition wedge.
- **Predictions that help (Huckleberry SweetSpot, Baby Daybook).** Next nap /
  next feed windows derived from the baby's own pattern.

---

## What parents *complain* about (our opportunities)

This is the gold. Real, recurring frustrations from App Store / Play Store
reviews and comparison write-ups:

### 1. Surprise & expensive subscriptions — with **sharing behind the paywall**
- Users report **spending $150+ on subscriptions they didn't realize they
  approved**, hidden at the bottom of an order, with no renewal reminders.
- The single most-needed feature — **a second caregiver being able to log** — is
  the very thing apps like Baby Tracker and Glow **paywall immediately**.
- **→ Our move:** real-time multi-caregiver sync is **free and core**. Honest,
  obvious pricing. Whatever we ever charge for, it's never *sharing* or *saving
  your data*.

### 2. Performance failures at the worst moment
- **Timers lag or freeze while breastfeeding.** App freezes mid-feed.
- **Entries silently fail to save.** Nap/feed timestamps come out "wildly
  inaccurate." No real-time update between devices.
- **→ Our move:** **offline-first architecture** — the tap writes locally and
  instantly, always; sync happens in the background and can never block or lose
  a log. Timers survive backgrounding and lock.

### 3. Bad one-handed ergonomics
- Reviews call out **tiny logging buttons that are hard to reach one-handed**
  while holding a baby, with **profile photos taking up huge space** and the
  actual controls crammed and small.
- **→ Our move:** thumb-zone-first layout. Big primary actions at the bottom.
  Common actions in ≤2 taps. Designed for the dark, one-handed, 3am reality.

### 4. Useless "insights" / milestones
- The milestone/stats sections are called **"useless"** — showing vanity metrics
  like **total diaper count** instead of useful things like **max time between
  feeds** or **longest sleep stretch**.
- **→ Our move:** every insight is **actionable** — "next nap window
  1:10–1:40pm," "longest stretch last night: 4h20m," "feeds are ~20 min later
  each day this week." No decorative counters.

### 5. Data lock-in & privacy fear
- Parents **don't want to lose old data** when switching apps, and are uneasy
  about where sensitive **baby health data** lives.
- **→ Our move:** local-first (your data is on *your* device by default),
  frictionless **export (PDF + CSV)** and **import** from other apps, and a
  clear, minimal privacy posture. No lock-in, ever.

---

## Special insight: the "helper" changes the product

Our founder's household includes a **domestic helper who co-cares for the baby**.
This is common globally and it reshapes priorities:

- **Shared logging is not optional** — two+ people log the same baby daily. This
  is exactly what most apps charge for. We make it free and central.
- **The UX must work for a non-parent caregiver:** possibly a different first
  language (→ **localization / simple mode**), and it must be unambiguous who
  logged what (→ **per-caregiver attribution** on every entry).
- **Trust & boundaries:** the account owner (parent) controls who's invited and
  what they can see/do (→ simple **roles**: owner vs caregiver).

This single fact is the strongest reason our differentiator ("free real-time
sharing done beautifully") is the right bet.

---

## Where AI/voice fits (deliberately later)

Robin Baby proves there's appetite for **voice logging** ("nursed 15 min on the
left, dirty diaper at 8") and **AI recall** ("when was the last bottle?",
"has reflux improved since I cut dairy?"). It's a real "wow."

But voice **cannot replace** fast manual logging — you can't talk in a silent
nursery next to a sleeping partner, and health data needs a deterministic,
offline, no-mistakes path. So voice/AI is a **force multiplier we add on top** of
excellent manual logging, not our v1 headline. See the [roadmap](./03-roadmap.md).

---

## Sources

- [PiyoLog on the App Store](https://apps.apple.com/us/app/baby-tracker-piyolog/id1252857347)
- [Best Baby Tracker Apps 2026 — Pebbi](https://pebbi.co/blog/best-baby-tracker-apps-2026)
- [Best Baby Tracking Apps 2026: Huckleberry vs Napper vs Nara vs Robin — OurKidsMom](https://www.ourkidsmom.com/best-baby-tracking-apps-2026-huckleberry-vs-napper-vs-nara-vs-robin-baby/)
- [The 5 Best Baby Tracker Apps — bestbabytracker.com](https://www.bestbabytracker.com/home)
- [10 Best Baby Tracker Apps in 2026 (Feeding, Sleep, Diapers, Growth, AI) — Outreachz](https://outreachz.com/blog/best-baby-tracker-ai-apps/)
- [Robin Baby on Google Play](https://play.google.com/store/apps/details?id=com.robinbaby)
- [Nara — Baby & Mom Tracker on Google Play](https://play.google.com/store/apps/details?id=com.naraorganics.nara)
- [6 Best Baby Growth Tracker Apps (2026) — Tinylog](https://tinylog.app/guides/best-baby-growth-tracker-apps)
- [Baby Daybook](https://babydaybook.app/)
- [ParentLove](https://parentlove.me/)
- [Best Baby Tracker Apps in 2026, an honest comparison — Medium](https://medium.com/@muharremyurtsever/best-baby-tracker-apps-in-2026-an-honest-comparison-from-a-parent-who-tried-them-all-8fa1f738c681)
