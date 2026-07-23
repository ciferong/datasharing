# 🍼 Baby Tracker — "Best of the Best" Product Vision

> A plan for a baby-logging app that beats PiyoLog, Huckleberry, and the rest —
> by fixing the exact things parents complain about.

This folder is the **product brief**. There's no app code here yet — this is the
thinking that comes *before* building, so we build the right thing. It's written
to be read by a non-technical founder building with AI help.

## The one-sentence pitch

> **The fastest, calmest baby log you can use one-handed at 3am — with free
> real-time sharing between you and your helper, and predictions that actually
> tell you what to do next — no surprise subscriptions, no data lock-in.**

## Why this can win

Every popular app is great at one thing and annoying at another. The market
leaves three big doors open, and we walk through all three:

1. **They paywall sharing.** Most apps make you pay so a second caregiver can
   log. For a household with a **domestic helper co-caring for the baby**,
   shared logging isn't a luxury — it's the whole point. We make real-time
   multi-caregiver sync **free and core**.
2. **They lag when it matters.** Parents report timers freezing *mid-feed* and
   entries silently not saving. We are **offline-first** so logging is instant
   and never fails, even with no signal.
3. **Their "insights" are useless.** They show you "47 total diapers" instead of
   "next nap window: 1:10–1:40pm." We ship **actionable predictions**, not
   vanity stats.

## Our north-star principles

| Principle | What it means in practice |
|-----------|---------------------------|
| **One-handed, always** | Every common action reachable by a thumb, in ≤2 taps, while holding a baby |
| **Never loses data** | Works fully offline; syncs when it can; an entry tapped is an entry saved |
| **Sharing is free** | You + your helper both log and see each other live, at no cost |
| **Actionable > pretty** | Predictions and next-steps, not decorative charts |
| **Honest & private** | No dark-pattern subscriptions; health data stays yours; easy export |

## How to read this folder

Read in order — each doc builds on the last:

1. **[01-market-research.md](./01-market-research.md)** — Who the competitors
   are, what they do well, and exactly what parents complain about. This is the
   evidence behind every decision.
2. **[02-product-spec.md](./02-product-spec.md)** — What we're actually building:
   the features, the screens, how sharing works, what the predictions do, and
   how the data is structured.
3. **[03-roadmap.md](./03-roadmap.md)** — The build order, milestone by
   milestone, sized for one person building with AI.
4. **[04-tech-decisions.md](./04-tech-decisions.md)** — Which technology to build
   with (and why), how sharing/sync works under the hood, how your health data
   stays private, and how *you* preview the app on your own phone.

## What we decided up front

- **First deliverable:** this written spec (you're reading it). No app code yet.
- **Build target:** React Native + Expo — see [04-tech-decisions.md](./04-tech-decisions.md).
- **Data:** local-first (lives on the phone), designed so free real-time sharing
  drops in cleanly.
- **Roadmap order:** flawless manual logging + free sharing → predictions →
  (later) voice/AI logging.

## The 30-second summary of what v1 does

You open the app. A big **Feed / Sleep / Diaper** row sits under your thumb. One
tap starts a nursing timer (with a left/right toggle) — it keeps running even if
you lock the phone. Your helper, on her phone, sees that feed appear live. The
home screen shows a **daily timeline** of everything so far and a gentle nudge:
"Baby's usually ready for a nap around now." At the doctor, you tap once to
export a clean PDF summary. Nothing is behind a paywall that matters, and your
baby's data never leaves your control without you saying so.

That's the product. The rest of this folder is how we get there.
