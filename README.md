# ⏰ MAD Practical 6 — Animations & Alarm Manager (Android)

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Kotlin-7F52FF?logo=kotlin&logoColor=white)
![UI](https://img.shields.io/badge/UI-XML%20Views-orange)
![Min SDK](https://img.shields.io/badge/minSdk-26-blue)
![Target SDK](https://img.shields.io/badge/targetSdk-37-blue)

**Subject:** Mobile Application Development (MAD)
**Enrollment No.:** 25172022054
**Practical No.:** 6

---

## 📖 Overview

This app demonstrates the main **animation techniques in Android** (frame-by-frame, tween, and a looping drawable animation) along with scheduling and cancelling an alarm using **`AlarmManager`** and a **`BroadcastReceiver`**.

It has two screens: an animated **Splash screen** followed by the **Main screen** where the alarm is created or cancelled.

## 🎯 Aim

To implement frame animation and tween animation in an Android application and to create/cancel an alarm using `AlarmManager` and `BroadcastReceiver`.

## ✨ Features

### 🌅 Splash Screen
- **Frame animation** (`AnimationDrawable`) that reveals the university logo piece by piece across 8 frames
- After about **7.5 seconds**, a **tween animation** (scale + alpha + translate + rotate) plays on the logo
- `AnimationListener` detects the end of the tween and automatically opens `MainActivity`
- Fade-in / fade-out activity transition
- Immersive full-screen mode (status & navigation bars hidden)

### ⏰ Main Screen
- **Alarm picture animation:** a 10-frame looping frame animation (100 ms per frame)
- **Heart fill animation:** a looping 5-step animation (0% → 100%) built from vector drawables
- **Create Alarm** button → schedules an alarm **10 seconds** from now using `AlarmManager.setExact()`
- **Cancel Alarm** button → cancels the pending alarm
- When the alarm fires, `AlarmBroadcastReceiver` shows an **"Alarm triggered!"** Toast
- Graceful fallback: if exact-alarm permission is not granted, it uses an inexact `set()` alarm instead of crashing

## 🧩 Animation Types Used

| Type | Where | File |
|---|---|---|
| Frame animation (`animation-list`) | Splash logo reveal | `drawable/logo_animation.xml` |
| Frame animation (`animation-list`) | Alarm clock images | `drawable/animation.xml` |
| Frame animation (`animation-list`) | Heart fill | `drawable/heart_fill_animation.xml` |
| Tween animation (`set`: scale, alpha, translate, rotate) | Splash exit | `anim/twinanimation.xml` |
| Extra tween resources | Reusable | `anim/fade_in_up.xml`, `anim/zoom_rotate_in.xml` |

## 🧭 App Flow

```
Splash (frame anim ~7.5s → tween anim) ──► MainActivity
                                              │
                      ┌───────────────────────┴──────────────────────┐
                Create Alarm (+10s)                          Cancel Alarm
                      │                                              │
        AlarmManager.setExact() ──► AlarmBroadcastReceiver ──► Toast "Alarm triggered!"
```

## 🛠️ Tech Stack

| Component | Details |
|---|---|
| Language | Kotlin |
| UI | XML layouts, ConstraintLayout, Material Components |
| Animation APIs | `AnimationDrawable`, `AnimationUtils`, `Animation.AnimationListener` |
| System APIs | `AlarmManager`, `PendingIntent`, `BroadcastReceiver` |
| Min SDK | 26 (Android 8.0) |
| Target SDK | 37 |
| Permission | `SCHEDULE_EXACT_ALARM` |

## 📂 Project Structure

```
25172022054_mad_practical6/
├── app/src/main/
│   ├── java/com/new_app/a25172022054_mad_practical6/
│   │   ├── SplashActivity.kt           # Frame + tween animation, launches MainActivity
│   │   ├── MainActivity.kt             # Alarm create / cancel + looping animations
│   │   └── AlarmBroadcastReceiver.kt   # Shows Toast when alarm triggers
│   ├── res/
│   │   ├── anim/                       # Tween animation XMLs
│   │   ├── drawable/                   # animation-lists, logo frames, alarm images, heart vectors
│   │   ├── layout/                     # activity_splash.xml, activity_main.xml
│   │   └── values/                     # strings, colors, themes
│   └── AndroidManifest.xml             # SplashActivity = launcher, receiver + permission
├── gradle/                             # Wrapper + libs.versions.toml
├── build.gradle.kts
└── settings.gradle.kts
```

## 🚀 Getting Started

### Prerequisites
- Android Studio (latest stable recommended)
- JDK 17 or above
- Emulator / device with Android 8.0 (API 26) or higher

### Run the project

```bash
# 1. Clone the repository
git clone https://github.com/Prince-Prajapati-Maheshbhai/25172022054_mad_practical6.git

# 2. Open in Android Studio and let Gradle sync

# 3. Select an emulator / device and click ▶ Run
```

### How to test the alarm
1. Wait for the splash animation to finish — the main screen opens automatically.
2. Tap **Create Alarm** → a toast confirms the alarm is set for 10 seconds.
3. Wait 10 seconds → the **"Alarm triggered!"** toast appears.
4. Tap **Cancel Alarm** before the time runs out to cancel it.

> ℹ️ On Android 12+ the exact-alarm permission may need to be allowed in system settings; otherwise the app falls back to an inexact alarm, which can fire slightly later.

## 📚 Concepts Covered

- Frame-by-frame animation with `animation-list` and `AnimationDrawable`
- Tween animation with `<scale>`, `<alpha>`, `<translate>`, `<rotate>`, `startOffset` and `duration`
- `AnimationListener` for chaining screens
- `onWindowFocusChanged()` for starting `AnimationDrawable`
- `Handler` with `postDelayed`
- `AlarmManager`, `PendingIntent` and `BroadcastReceiver`
- Edge-to-edge UI and immersive mode

## 👤 Author

**Prince Prajapati**

Enrollment No.: 25172022054
