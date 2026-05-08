# LiftOff — Build Reflection

## What I Built

LiftOff is a gamified workout tracker built as a single-file React PWA wrapped in Capacitor for Android. The app lets users build workout routines from a library of 505+ exercises, log sets during active workouts, automatically detect personal records, and visualize strength progress over time through multiple chart types.

Key features delivered:
- **505+ exercise library** organized by muscle group and equipment, with search and filter
- **Routine builder** with drag-and-drop exercise selection and muscle group tagging
- **Active workout logger** with rest timer (configurable: 60/90/120/180s), per-exercise set tracking, and a live elapsed timer
- **XP leveling system** — earn XP from every workout, PR, and kg lifted; advance through 7 ranks from Beginner to Immortal
- **Badges** — 8 achievement badges unlocked by hitting milestones
- **Personal record detection** — auto-detected on every workout completion with confetti celebration
- **Per-exercise progress charts** — SVG line charts of max weight over time
- **Per-muscle-group volume charts** — track volume progression for each muscle group with colored charts
- **Muscle donut chart** on home screen showing training focus breakdown
- **Weekly bar chart** showing daily training volume for the last 7 days
- **Leaderboard** with weekly/monthly/all-time views and simulated community rankings
- **Onboarding flow** — first-time setup with username
- **Profile page** with stats, badge collection, and XP bar
- **Android APK** via Capacitor — ready to build in Android Studio

## What Was Easy

The exercise library was straightforward to build up — adding 500+ entries is tedious but mechanical. React's component model made it natural to break the app into isolated, reusable pieces. Tailwind CDN made styling fast without a build step. The localStorage persistence pattern was dead simple and reliable.

The rest timer and workout logger logic was clean — React hooks (`useState`, `useEffect`, `useRef`) handled the countdown and elapsed time without any external state library.

## What Was Hard

**The biggest challenge was the build toolchain.** I started with Vite + TypeScript + React 19, which hit multiple compounding issues:

1. `lucide-react` had a peer dependency conflict with React 19 (required React ^18)
2. Vite 8 requires Node 20+, but the machine has Node 18
3. After downgrading both, TypeScript files written through the file tools consistently came out corrupted — null bytes and truncation caused `SyntaxError: doesn't provide an export named X` at runtime even when files looked correct in the editor

The fix was radical: **abandon the entire Vite/TypeScript build system** and switch to a single `index.html` using React 18 UMD + Babel standalone in the browser. This eliminated the build step entirely and made file corruption irrelevant. The tradeoff is no TypeScript safety and a CDN dependency, but for a contest the result is a fully working app.

**Recharts also caused issues** — its UMD bundle depends on `prop-types` and load ordering with Babel caused `Recharts is not defined` errors. Solution: wrote a custom SVGChart component using plain SVG, which turned out to produce cleaner, more performant charts anyway.

## What I'd Change

1. **Add cloud sync** — currently everything is in localStorage. Real competition between friends requires a backend. I'd use Firebase Firestore with anonymous auth for a quick real-time leaderboard.

2. **Exercise video thumbnails** — Liftoff's killer feature is the animated exercise demos. Adding even static form cue images would massively improve the experience.

3. **Plate calculator and 1RM estimator** — power users want to know their theoretical max and which plates to load. This would be a high-value addition.

4. **TypeScript + Vite build** — with Node 20+ the project should be rebuilt with proper typing. The current single-file approach is fragile at scale.

5. **Haptic feedback** — on mobile, a vibration pulse when completing a set or hitting a PR would make the gamification feel more satisfying.

6. **Social features** — the leaderboard currently uses simulated entries. Real friend invites and shared PRs would make the competition meaningful.

## What I Learned

- Sometimes the right answer is to remove tooling complexity rather than fight it
- Single-file apps are underrated for rapid prototyping — zero build errors, instant reload
- SVG charts from scratch are more controllable than charting libraries and lighter on dependencies
- The constraint of localStorage actually simplified the data model significantly vs. designing for a database
