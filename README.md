

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

<img width="360" height="800" alt="frame_001" src="https://github.com/user-attachments/assets/540bc179-4122-4fa9-b035-5bf166d820b4" />
<img width="360" height="800" alt="frame_002" src="https://github.com/user-attachments/assets/6435fa20-c893-4899-89a7-acf55c013a92" />
<img width="360" height="800" alt="frame_003" src="https://github.com/user-attachments/assets/c7d38d08-9502-414e-ae3e-e8056536dcaf" />
<img width="360" height="800" alt="frame_004" src="https://github.com/user-attachments/assets/71cc06d7-8560-4bfb-9040-06e3312e84cb" />
<img width="360" height="800" alt="frame_005" src="https://github.com/user-attachments/assets/54c7eaea-c687-46bb-b221-0b6474dff8db" />
<img width="360" height="800" alt="frame_006" src="https://github.com/user-attachments/assets/b91fefd6-2e3f-46bf-9539-e6f673b18be5" />
<img width="360" height="800" alt="frame_007" src="https://github.com/user-attachments/assets/93e33576-6edb-42ff-b1f3-ba5443b72514" />
<img width="360" height="800" alt="frame_009" src="https://github.com/user-attachments/assets/51957994-6757-4d70-8536-1caa4d16eeb9" />
<img width="360" height="800" alt="frame_010" src="https://github.com/user-attachments/assets/9af0f5cd-071e-4978-9cd7-f0719a357a61" />
<img width="360" height="800" alt="frame_011" src="https://github.com/user-attachments/assets/a4219276-ff85-414c-a14d-7018da220e39" />
<img width="360" height="800" alt="frame_012" src="https://github.com/user-attachments/assets/f3470ebf-931d-4cdc-a576-72fa9b41f4c1" />
<img width="360" height="800" alt="frame_013" src="https://github.com/user-attachments/assets/f4b3adf1-083d-4f90-a507-bc7c3a7995ab" />
<img width="360" height="800" alt="frame_014" src="https://github.com/user-attachments/assets/1a6834c0-556d-4f7e-ae81-ed96ae1167ec" />
<img width="360" height="800" alt="frame_015" src="https://github.com/user-attachments/assets/652bdd78-c46c-4521-a694-e78ed8d17853" />
<img width="360" height="800" alt="frame_017" src="https://github.com/user-attachments/assets/4bca79f8-9b07-44ca-a2b1-5c448c50ffde" />
<img width="360" height="800" alt="frame_018" src="https://github.com/user-attachments/assets/300159af-a662-4a19-83a8-b8a897dba7ca" />
<img width="360" height="800" alt="frame_019" src="https://github.com/user-attachments/assets/4dbfa64c-d89b-41eb-8c60-573f2ddde67e" />
<img width="360" height="800" alt="frame_020" src="https://github.com/user-attachments/assets/cc6dda36-e9a9-4037-80aa-e04a384fe8d5" />

---

## AI Logs

The `/ai-logs/` folder documents the full AI-assisted development process — architecture decisions, pivot from Vite/TypeScript to single-file, exercise library batching, chart implementation, and the major upgrade phase.

---

## License

MIT
