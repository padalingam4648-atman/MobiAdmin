# 📱 MobiAdmin - Remote Device Security App

MobiAdmin is an Android security application that allows **remote device control using SMS commands**. It enables users to **find, lock, and track their phone** without internet connectivity.

---

## 🎯 Project Overview

This project is designed for **mobile security and anti-theft protection**.  
It uses Android system components like **Broadcast Receivers, Services, and Device Admin APIs** to perform actions remotely.

### 🔑 Core Idea
- Send an SMS command → Device receives it → Action is triggered → Response SMS is sent

---

## 🚀 Key Features

- 🔊 **Phone Finder** – Ring device at max volume via SMS  
- 📍 **Location Tracking** – Get GPS location with Google Maps link  
- 🔒 **Remote Lock** – Lock device instantly  
- 📱 **SIM Monitoring** – Detect SIM changes and send alerts  
- 📡 **Offline Working** – Works fully without internet  

---

## 📨 SMS Commands

| Feature | Command |
|--------|--------|
| Ring Phone | `MOBI RING` |
| Get Location | `MOBI LOCATION` |
| Lock Device | `MOBI LOCK` |
| SIM Info | `MOBI SIM` |
| Help | `MOBI HELP` |

---

## ⚙️ Setup

1. Install the app  
2. Grant permissions (SMS, Location, Phone)  
3. Enable **Device Admin**  
4. Set alternate number for SIM alerts  

---

## 🧠 How It Works

1. SMS received → `SmsReceiver`  
2. Command validated  
3. Service triggered (Ring / Lock / Location)  
4. Action executed  
5. Confirmation SMS sent  

---

## 📁 Project Structure
MobiAdmin/
├── app/
│ ├── src/main/
│ │ ├── java/com/example/mobiadmin/
│ │ │ ├── MainActivity.kt
│ │ │ ├── SmsReceiver.kt
│ │ │ ├── PhoneFinderService.kt
│ │ │ ├── SimTrackingService.kt
│ │ │ ├── SimChangeReceiver.kt
│ │ │ ├── MyDeviceAdminReceiver.kt
│ │ │ └── SecurityUtils.kt
│ │ ├── res/
│ │ └── AndroidManifest.xml
│ └── build.gradle.kts
---

## 📂 Folder Explanation

### 🔹 `app/`

Main module of the application (core app logic)

### 🔹 `app/src/main/java/com/example/mobiadmin/`

Contains all source code:

* **MainActivity.kt** → User interface and controls
* **SmsReceiver.kt** → Detects incoming SMS commands
* **PhoneFinderService.kt** → Handles alarm & location
* **SimTrackingService.kt** → Monitors SIM changes
* **SimChangeReceiver.kt** → Detects SIM replacement
* **MyDeviceAdminReceiver.kt** → Enables device admin (lock feature)
* **SecurityUtils.kt** → Utility functions for security

### 🔹 `app/src/main/res/`

UI resources:

* Layouts (XML files)
* Icons & images
* Strings, colors, styles

### 🔹 `app/src/main/AndroidManifest.xml`

Defines:

* Permissions (SMS, Location, Phone)
* Broadcast Receivers
* Services
* Device Admin

---

## 📦 APK & Build Output

### 🔹 `app/build/outputs/apk/`

Contains generated APK files after building the project:

* `debug/app-debug.apk` → Used for testing
* `release/app-release.apk` → Final production APK

👉 Install APK manually:

```bash
adb install app/build/outputs/apk/debug/app-debug.apk
```

---

## ⚙️ Build & Run Commands

```bash
# Build project
./gradlew build

# Install on device
./gradlew installDebug

# Uninstall app
adb uninstall com.example.mobiadmin

# View logs
adb logcat | grep MobiAdmin
```

---

## 🛠️ Tech Stack

* Kotlin
* Android SDK
* Broadcast Receivers
* Foreground Services
* DevicePolicyManager API

---

## 🔒 Security Features

* Works offline using SMS
* No data sharing
* Local processing only
* Device Admin protection
* Secure SIM monitoring

---

## 🎯 Use Cases

* 📱 Lost phone recovery
* 🔐 Anti-theft protection
* 🚨 Emergency tracking
* 👨‍👩‍👧 Family safety

---

## ⚠️ Note

Use only on your own device or with proper permission.

---

**Version:** 1.0
**License:** 
MIT License

Copyright (c) 2026 Padalingam S

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software... (rest continues)

---
