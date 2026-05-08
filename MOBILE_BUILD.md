# Building LiftOff as a Mobile App (Capacitor)

## Prerequisites
- Node.js 18+ ✅ (you have this)
- Android Studio (for Android .apk) → https://developer.android.com/studio
- OR Xcode on Mac (for iOS .ipa)

---

## Step 1 — Install Capacitor

```bash
cd C:\Users\aarus\OneDrive\Desktop\Gamified-Workout-Tracker
npm install @capacitor/core @capacitor/cli @capacitor/android
```

## Step 2 — Initialize Capacitor

```bash
npx cap init LiftOff com.liftoff.workouttracker --web-dir .
```

## Step 3 — Add Android Platform

```bash
npx cap add android
```

## Step 4 — Sync web files into Android project

```bash
npx cap sync android
```

## Step 5 — Open in Android Studio

```bash
npx cap open android
```

This opens Android Studio. From there:
1. Wait for Gradle sync to finish
2. Click **Run ▶** (or press Shift+F10) to run on an emulator or connected phone
3. To build a release APK: **Build → Build Bundle(s) / APK(s) → Build APK(s)**

---

## Quick rebuild after changes

Whenever you edit `index.html`, run:
```bash
npx cap sync android
```
Then rebuild in Android Studio.

---

## iOS (Mac only)

```bash
npm install @capacitor/ios
npx cap add ios
npx cap sync ios
npx cap open ios
```
Then build in Xcode.

---

## Tips
- The app already has a `manifest.json` and mobile meta tags
- The `capacitor.config.json` is already configured with app ID `com.liftoff.workouttracker`
- For a release build, you'll need to sign the APK with a keystore
- To generate app icons from a single image: `npm install @capacitor/assets` then `npx capacitor-assets generate`
