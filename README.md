# LiftOff — Gamified Workout Tracker

A mobile workout tracking app with a competitive twist. Built with React 18, pre-compiled JSX, and Capacitor for Android.

[![Contest](https://img.shields.io/badge/8x-contest-orange)](https://github.com/8xsocial/template-mobile)

---

## Features

- **505+ exercise library** — searchable, filterable by muscle group and equipment
- **Routine builder** — create custom routines with any combination of exercises
- **Workout logger** — log sets/reps/weight with configurable rest timer (60/90/120/180s)
- **PR detection** — auto-detected personal records with confetti celebration
- **XP & leveling** — earn XP from every workout, PR, and kg lifted. 7 ranks: Beginner → Immortal
- **Progress charts** — per-exercise max weight over time + per-muscle-group volume charts
- **Leaderboard** — weekly / monthly / all-time volume rankings
- **Badges** — 8 achievement badges
- **Fully offline** — no internet required, all data stored in localStorage

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| UI | React 18 (UMD, pre-compiled) | No build step needed in Capacitor |
| Styling | Inline styles | Zero dependencies, works offline |
| Charts | Custom SVG | No external lib, fully controlled |
| Storage | localStorage | Simple, offline-first |
| Mobile | Capacitor 8 + Android | Native APK wrapper |

> **No Vite. No TypeScript. No CDN.** The entire app is one self-contained `www/index.html` — JSX pre-compiled to vanilla JS at build time, React 18 bundled inline. This guarantees it works offline in the Android WebView.

---

## Project Structure

```
liftoff-workout-tracker/
├── www/
│   ├── index.html        ← Entire app (React + all logic, self-contained)
│   ├── manifest.json     ← PWA manifest
│   ├── icon-192.png
│   └── icon-512.png
├── android/              ← Capacitor Android project (open in Android Studio)
├── capacitor.config.json ← Capacitor config (webDir: "www")
├── package.json          ← Only Capacitor deps
├── ai-logs/
│   └── build-log.md      ← Full AI-assisted development log
├── REFLECTION.md         ← Build reflection (what was easy, hard, what I'd change)
└── MOBILE_BUILD.md       ← Step-by-step APK build guide
```

---

## Build the APK

### Prerequisites
- Node.js 18+
- Android Studio with Android SDK

### Steps

```bash
# 1. Install Capacitor
npm install

# 2. Sync web assets into the Android project
npm run sync

# 3. Open in Android Studio
npm run open
```

In Android Studio:
1. Wait for Gradle sync to finish
2. **Run ▶** to launch on emulator or device
3. **Build → Build Bundle(s)/APK(s) → Build APK(s)** for a release APK

> See [MOBILE_BUILD.md](./MOBILE_BUILD.md) for detailed instructions including emulator setup tips.

---

## App Screens

| Screen | What you see |
|---|---|
| **Onboarding** | Dark welcome screen with orange barbell icon → username entry ("What should we call you?") — shown once on first launch |
| **Home** | Greeting with rank (e.g. "Hey, Cookie · Level 1 · Beginner"), XP progress bar, streak counter, Start Workout CTA, stats grid (Workouts / Volume / PRs), 7-day volume bar chart, recent workouts list |
| **Routines** | Routine list with muscle group tags; tap a routine to view exercises; "+ New" to build one from scratch |
| **Routine Builder** | Exercise list with numbered order + remove button; search bar across all 505 exercises; muscle group filter pills (All / Chest / Back / Shoulders / Biceps / Triceps…); tap "+" to add |
| **Workout Logger** | Active workout header with live elapsed timer (mm:ss) and routine name badge; exercise name + muscle tag; set rows with REPS / KG inputs; rest timer quick-select (60s / 90s / 120s / 180s); Prev / Next Exercise navigation; dot progress indicator; confetti on PR |
| **Progress** | 3 tabs — By Exercise (SVG line charts of max weight over time), By Muscle (per-muscle-group volume charts with unique colors), All PRs (full PR history table) |
| **Leaderboard** | Weekly / Monthly / All-time tabs; volume rankings with simulated community entries and top workout callouts |
| **Profile** | XP bar with rank level, total stats, 8 achievement badge grid (locked/unlocked), username edit |

### Screenshots (running on Android emulator — Pixel 6, API 34)

The app uses a dark `#0a0a0a` theme with orange (`#f97316`) accents throughout. All icons are custom SVG — no emoji anywhere. The launcher icon is a dark barbell on an orange circle, consistent with the in-app theme.

---

## AI Logs

The `/ai-logs/` folder documents the full AI-assisted development process — architecture decisions, pivot from Vite/TypeScript to single-file, exercise library batching, chart implementation, and the major upgrade phase.

---

## License

MIT
