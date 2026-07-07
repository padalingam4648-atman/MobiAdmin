# 📱 MOBIADMIN — Remote Device Security App

> **Control your Android device remotely via SMS — no internet required.**

MOBIADMIN is an Android security application that enables **remote device control using SMS commands**.  
Ring your phone, track its location, lock it, and monitor SIM changes — all through a simple SMS.

---

## 🚀 Key Features

| Feature | Description |
|--------|-------------|
| 🔊 **Phone Finder** | Rings device at max volume remotely |
| 📍 **GPS Location** | Returns live Google Maps link via SMS |
| 🔒 **Remote Lock** | Locks device instantly via SMS |
| 📱 **SIM Monitoring** | Detects SIM swap and sends alert SMS |
| � **Boot Persistence** | Restarts monitoring after device reboot |
| 📡 **Offline Ready** | Works fully without internet |

---

## 📨 SMS Commands

Send any of these commands via SMS to your device:

| Action | Command |
|--------|---------|
| 🔊 Ring phone | `MOBI RING` |
| 🔊 Ring (alias) | `MOBI BUZZ` · `MOBI ALARM` · `MOBI FINDME` |
| 📍 Get location | `MOBI LOCATION` |
| 📍 Location (alias) | `MOBI WHERE` · `MOBI GPS` · `MOBI TRACK` |
| 🔒 Lock device | `MOBI LOCK` |
| 🔒 Lock (alias) | `MOBI SECURE` · `MOBI PROTECT` · `MOBI EMERGENCY` |
| 📱 SIM status | `MOBI SIM` |
| 📱 SIM (alias) | `MOBI SIMSTATUS` · `MOBI SIMINFO` · `MOBI SIMCHECK` |
| ❓ Help | `MOBI HELP` · `MOBI COMMANDS` · `MOBI INFO` |

> Commands are **case-insensitive** — `mobi ring`, `MOBI RING`, `Mobi Ring` all work.

---

## ⚙️ Setup & Installation

### Prerequisites
- Android Studio (latest)
- Java JDK 17+
- Android SDK API 24+
- ADB (Android Debug Bridge)

### Build & Install

```bash
# Clone the repo
git clone https://github.com/padalingam4648-atman/MobiAdmin.git
cd MobiAdmin

# Build debug APK
./gradlew assembleDebug

# Install on connected device/emulator
adb install app/build/outputs/apk/debug/app-debug.apk

# Launch the app
adb shell am start -n com.example.mobiadmin/.MainActivity
```

### First-Time App Setup
1. Open the app
2. Tap **⚙️ PERMISSIONS** — grant all requested permissions
3. Tap **🔒 LOCK** — enable Device Admin for remote lock
4. Enter an **alternate phone number** for SIM change alerts
5. Tap **💾 SAVE & ACTIVATE**

---

## 🧠 How It Works

```
Incoming SMS
     ↓
SmsReceiver (highest priority broadcast)
     ↓
Command detected & validated
     ↓
Service triggered
     ↓
  ┌──────────────┬─────────────────┬───────────────┐
  ▼              ▼                 ▼               ▼
RING          LOCATION           LOCK           SIM INFO
  │              │                 │               │
PhoneFinderService    GPS fetch    DevicePolicyMgr  TelephonyManager
  │              │                 │               │
  └──────────────┴─────────────────┴───────────────┘
                 ↓
      Confirmation SMS sent back
```

---

## � Project Structure

```
MobiAdmin/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/mobiadmin/
│   │   │   │   ├── MainActivity.kt           ← UI & controls
│   │   │   │   ├── SmsReceiver.kt            ← Intercepts SMS commands
│   │   │   │   ├── PhoneFinderService.kt     ← Ring + location service
│   │   │   │   ├── SimTrackingService.kt     ← SIM change tracking
│   │   │   │   ├── SimChangeReceiver.kt      ← SIM swap detection
│   │   │   │   ├── MyDeviceAdminReceiver.kt  ← Device admin (lock)
│   │   │   │   └── SecurityUtils.kt          ← Hash & mask utilities
│   │   │   ├── res/
│   │   │   │   ├── layout/activity_main.xml  ← Main screen UI
│   │   │   │   ├── values/strings.xml        ← App strings
│   │   │   │   ├── xml/device_admin_receiver.xml
│   │   │   │   └── drawable/                 ← Cyber-themed UI assets
│   │   │   └── AndroidManifest.xml
│   │   ├── test/                             ← Unit tests
│   │   └── androidTest/                      ← Instrumented tests
│   └── build.gradle.kts
├── settings.gradle.kts
└── gradle.properties
```

---

## 🛠️ Tech Stack

| Technology | Usage |
|-----------|-------|
| **Kotlin** | Primary language |
| **Android SDK 34** | Target platform |
| **BroadcastReceiver** | SMS command interception |
| **ForegroundService** | Background ring & location |
| **DevicePolicyManager** | Remote device lock |
| **FusedLocationProvider** | GPS location retrieval |
| **SmsManager** | Send response SMS |
| **Firebase Realtime DB** | Optional location logging |
| **Coroutines** | Async location tracking |

---

## � Permissions Required

| Permission | Purpose |
|-----------|---------|
| `RECEIVE_SMS` | Intercept incoming SMS commands |
| `SEND_SMS` | Send confirmation/location replies |
| `ACCESS_FINE_LOCATION` | Get precise GPS coordinates |
| `READ_PHONE_STATE` | Read SIM card status |
| `READ_PHONE_NUMBERS` | Read device phone number |
| `RECEIVE_BOOT_COMPLETED` | Restart monitoring after reboot |
| `FOREGROUND_SERVICE` | Run background services |
| `BIND_DEVICE_ADMIN` | Enable remote device lock |
| `VIBRATE` | Vibration during ring |
| `POST_NOTIFICATIONS` | Show foreground notifications |

---

## 🔧 Useful ADB Commands

```bash
# Check emulator/device
adb devices

# Install APK
adb install -r app/build/outputs/apk/debug/app-debug.apk

# Launch app
adb shell am start -n com.example.mobiadmin/.MainActivity

# View live logs
adb logcat | grep -E "MobileFinderSMS|PhoneFinderService|SimTrack"

# Check app permissions
adb shell dumpsys package com.example.mobiadmin | grep permission

# Uninstall app
adb uninstall com.example.mobiadmin
```

---

## 🎯 Use Cases

- 📱 **Lost phone recovery** — ring it from another phone
- 🔐 **Anti-theft** — lock it remotely before it's accessed
- 🚨 **Emergency tracking** — get GPS location via SMS
- 👨‍👩‍👧 **Family safety** — monitor SIM changes on a family device

---

## ⚠️ Legal Notice

This app is intended for use **on your own device or with explicit permission** from the device owner.  
Unauthorized use may violate privacy laws.

---

## 📦 Package Info

| Property | Value |
|---------|-------|
| Package Name | `com.example.mobiadmin` |
| Min SDK | API 24 (Android 7.0) |
| Target SDK | API 34 (Android 14) |
| Version | 1.0 |
| Language | Kotlin |

---

## 📄 License

MIT License — © 2026 Padalingam S

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software.
