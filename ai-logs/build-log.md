# LiftOff — AI-Assisted Build Log

This log documents the development of LiftOff, a gamified workout tracker, built with Claude AI assistance for the 8x contest.

---

## Session 1 — Initial Architecture

**Prompt:** Build a Liftoff clone — gamified workout tracker. Features: routine builder with 500+ exercise library, set/rep/weight logger with rest timer, personal record tracking, strength progress charts per muscle group, weekly/monthly volume leaderboard.

**AI decisions:**
- Chose React + TypeScript + Vite + Firebase Firestore + TailwindCSS
- Planned component structure: ExerciseLibrary, RoutineBuilder, WorkoutLogger, ProgressCharts, Leaderboard, Profile

**Problem:** lucide-react peer dependency conflict with React 19. Fixed by upgrading lucide-react to ^0.469.0.

---

## Session 2 — Tooling Failures & Pivot

**Problem cascade:**
1. Vite 8 requires Node 20+, machine has Node 18 → downgraded Vite to 5.x
2. TypeScript source files written via file tools consistently came out with null bytes/truncation
3. This caused `SyntaxError: doesn't provide an export named X` for every module
4. Firebase caused `Auth is not exported from 'firebase/auth'` (type import used as value)

**AI reasoning:** After multiple attempts to fix the TypeScript corruption, the fundamental problem was the file sync layer between the AI tool environment and Windows filesystem. No amount of TypeScript fixes would solve a binary corruption issue.

**Pivot decision:** Abandon Vite/TypeScript entirely. Build a single `index.html` using:
- React 18 UMD loaded from unpkg CDN
- Babel standalone for JSX compilation in the browser
- localStorage instead of Firebase (simpler, no auth needed)
- Tailwind CDN

**Result:** App rendered successfully on first try after pivot.

---

## Session 3 — Exercise Library

**Prompt:** Need 500+ exercises with muscle group and equipment metadata.

**AI approach:** Built the library in 3 batches:
- Batch 1: 365 exercises across Chest/Back/Shoulders/Biceps/Triceps/Legs/Core/Cardio/Forearms
- Batch 2: 130 more — Olympic lifts, Kettlebell, Full Body, Glutes, Calves, Calisthenics, Strongman, Plyometrics, Stretching
- Batch 3: 10 final exercises (Hack Squat, Meadows Row, Tate Press, Copenhagen Plank, Pallof Press, etc.)

**Final count:** 505 exercises

---

## Session 4 — Recharts Failure & SVG Charts

**Problem:** `Recharts is not defined` at runtime — Recharts UMD depends on prop-types, and Babel load order caused it to fail even when loaded before Babel.

**AI decision:** Remove Recharts entirely. Write custom `SVGChart` component using plain SVG paths with:
- Gradient area fill under the line
- Dot markers at each data point
- Y-axis labels with range detection
- X-axis date labels

**Benefit:** Zero external dependency, more customizable, loads faster.

---

## Session 5 — Capacitor Android Setup

**Prompt:** Convert to mobile app (APK format).

**Steps:**
1. `npm install @capacitor/core @capacitor/cli @capacitor/android --legacy-peer-deps`
2. Created `www/` folder and set `webDir: "www"` in capacitor.config.json
3. `npx cap add android` — created Android project
4. `npx cap sync android` — copied web assets
5. `npx cap open android` — opened Android Studio

**Problem:** Emulator (Pixel 9a API 37) crashing — too resource-intensive.
**Solution:** Build APK via Build → Build APK(s) in Android Studio without emulator.

---

## Session 6 — Major UI/UX Upgrade

**Prompt feedback:** Need to win the contest. Judges score on: polished UI, Loom demo, AI logs, code quality, reflection. Reference app is Liftoff (iOS 4.8★).

**AI analysis of gaps vs Liftoff:**
- Missing: XP leveling, badges, per-muscle charts, onboarding, weekly volume chart, muscle focus viz
- Weak: Bottom nav icons (emoji), rest timer (single duration), workout completion screen

**Upgrades implemented:**
- XP system: 100 XP/workout + 50 XP/PR + 0.01 XP/kg lifted
- 7 rank levels: Beginner → Rookie → Athlete → Beast → Elite → Legend → Immortal
- XP progress bar shown on Home and Profile
- 8 achievement badges (unlocked/locked states)
- Onboarding flow: welcome screen + username setup
- Confetti animation (30-particle CSS) on PR achievement
- Muscle donut chart (SVG pie) on home screen
- Weekly bar chart — 7-day training volume
- Per-muscle-group volume charts with per-muscle colors
- Progress page with 3 tabs: By Exercise / By Muscle Group / All PRs
- Configurable rest timer: 60s/90s/120s/180s buttons
- SVG icons in bottom nav (replaced emoji)
- Live elapsed timer during workout
- Set number badges turn orange when filled in
- Last set values pre-filled on "Add Set"
- Muscle group tags on routine cards
- Muscle group filter pills in exercise search

**Final file:** 1648-line `www/index.html`. `npx cap sync android` confirmed.

---

## Key Prompting Patterns Used

1. **Diagnosis before fixing** — always checked actual error output before suggesting a fix
2. **Radical simplification** — when toolchain failed, proposed removing it rather than patching
3. **Incremental batching** — broke 500+ exercise library into chunks to avoid timeouts
4. **Constraint-aware design** — knew Node 18 limitation and worked around it throughout
5. **Feature parity check** — explicitly compared against Liftoff reference app before upgrade

---

## File Structure

```
Gamified-Workout-Tracker/
├── www/
│   └── index.html          ← Main app (1648 lines, self-contained)
├── android/                ← Capacitor Android project
├── capacitor.config.json   ← webDir: "www"
├── manifest.json           ← PWA manifest
├── package.json            ← Capacitor deps
├── MOBILE_BUILD.md         ← APK build instructions
├── REFLECTION.md           ← Contest reflection doc
└── ai-logs/
    └── build-log.md        ← This file
```
