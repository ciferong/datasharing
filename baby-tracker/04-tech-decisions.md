# 04 · Technology Decisions

*Written for a non-technical founder building with AI. The point of this page is
so that when AI writes the code, it builds on the right foundations — and so you
understand the choices without needing to code.*

---

## 1. What we build the app with: **React Native + Expo**

**The recommendation: React Native, using Expo.**

- **React Native** lets one codebase become **both an iPhone and Android app** —
  you don't build (and pay for) two separate apps.
- **Expo** is a toolkit on top of React Native that makes it dramatically easier
  for a solo, non-technical, AI-assisted builder:
  - **See it on your phone instantly.** Install the free "Expo Go" app, scan a QR
    code, and your app runs on your real phone — no Mac, no Xcode, no Android
    Studio required to start.
  - **Push updates over the air** without waiting on app-store review.
  - Batteries-included access to camera, notifications, storage, etc.

### Why not the alternatives?

| Option | Verdict | Why |
|--------|---------|-----|
| **Flutter** | Great, but not for you | Excellent, smooth UI — but uses the **Dart** language, which has a smaller talent pool and less AI training data than JavaScript. React Native's JS/TypeScript is the best-supported ecosystem for AI-assisted building. |
| **Native iOS (Swift) only** | No | Best performance, but **iPhone-only** and slowest to also reach Android — twice the work. |
| **Web app / PWA** | Good *on-ramp*, not the destination | A browser-based app is the **fastest way to see something early** and could be a great first prototype. But baby trackers live or die on native feel: reliable background timers, notifications, widgets, watch, and being one tap away on the home screen. React Native gives us those; a PWA fights us on them. |

**A reasonable path:** if you want to *see and feel* the concept in days, an
early web/PWA prototype is fine — but plan to build the real product in React
Native + Expo. Don't invest heavily in two codebases.

---

## 2. How "works offline & never loses data" actually works: **local-first**

The #1 competitor complaint is lost entries and frozen timers. We avoid it by
design:

- The app keeps a **database on the phone itself** (e.g. **SQLite**, the standard
  embedded database, via an Expo-compatible library). Suggested options for AI to
  choose among: **Expo SQLite**, **WatermelonDB**, or a local-first sync engine
  (see below).
- **Every tap writes to that local database immediately.** The app reads and
  writes locally, so it's instant and works with **zero internet**.
- Timers store their *start time*, not a ticking counter — so even if the phone
  restarts, "started at 2:04pm" is still true and the timer resumes correctly.

This alone makes us faster and more reliable than the apps parents complain about.

---

## 3. How free real-time sharing works: **sync on top of local-first**

Both the parent and the helper have the app, each with their own local database.
We keep them in sync:

- Each device logs locally (so it always works offline), then **syncs changes to a
  small cloud backend** when it has a connection. Other caregivers' devices pull
  those changes and merge them in.
- **Merging without conflicts:** every entry has a **globally unique id** created
  on the device (so two offline phones never collide) plus `updatedAt` timestamps
  and soft-delete flags. When devices reconnect, changes merge by id; the latest
  edit wins. This is a well-trodden pattern — AI can implement it with an existing
  sync engine rather than from scratch.
- **Backend options** (for the AI/engineer to pick — all support real-time + auth
  + reasonable free tiers):
  - **Supabase** (Postgres + realtime + auth) — great default, generous free tier.
  - **Firebase / Firestore** — battle-tested realtime, easy offline support.
  - **PowerSync / ElectricSQL / Instant** — purpose-built local-first sync engines
    that pair with the above.
- Because sync is **background and additive**, a network failure never blocks
  logging and never loses an entry — it just syncs later.

We commit to **not paywalling sharing**. If we ever charge, it's for advanced
extras — never for a second caregiver or for your data.

---

## 4. Privacy & security posture (health data — take it seriously)

Baby health data is sensitive; parents are (rightly) wary. Our stance:

- **Local-first means less exposure** — the primary copy lives on the parent's
  device, not a company server.
- **Encrypt in transit and at rest.** Standard HTTPS/TLS to the backend; the
  backend encrypts stored data.
- **Least data collected.** No selling data, no ad networks, no third-party
  trackers in the app.
- **You control access.** The owner invites/removes caregivers; roles limit what
  a caregiver can do.
- **Full export and full delete.** You can take all your data out (CSV/PDF) and
  delete everything, anytime.
- Be mindful of children's-data regulations (e.g. COPPA in the US, GDPR-K in the
  EU) when we get to launch — worth a proper review before the app stores.

---

## 5. How *you* (non-coder) will work with this

- You describe features; **AI writes the React Native/Expo code**. This spec is
  what keeps that code pointed the right way.
- You **preview on your own phone** via Expo Go by scanning a QR code — no
  developer tools needed to look at progress.
- When ready for the app stores, Expo has a build service (**EAS**) that produces
  the installable apps; that step needs Apple/Google developer accounts (a small
  annual fee) but not deep coding from you.

---

## 6. Summary of decisions

| Decision | Choice | One-line reason |
|----------|--------|-----------------|
| App framework | **React Native + Expo** | One codebase, best AI/ecosystem support, preview on your phone instantly |
| Data storage | **Local-first (SQLite-based)** | Instant, offline, never loses an entry |
| Sync/sharing | **Background sync via Supabase/Firebase + unique-id merge** | Free real-time multi-caregiver sharing that survives offline |
| Growth charts | WHO + CDC + **Fenton (preemie)** | Real percentiles; a rare differentiator |
| Privacy | Local-first + encryption + minimal collection + full export/delete | Earns trust with sensitive baby data |
| Early prototype (optional) | Web/PWA to *see* the idea fast | Cheap way to feel the concept before committing |

These are recommendations, not handcuffs — but changing any of them should be a
deliberate decision, because the rest of the plan assumes them.
