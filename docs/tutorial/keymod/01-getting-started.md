---
title: "KeyMod Tutorial - Getting Started"
description: "Install the KeyMod app, connect to your KeyMod device, and send your first keystroke in under 5 minutes."
keywords: "KeyMod getting started, KeyMod setup, KeyMod installation, connect KeyMod"
---

# 1. Getting Started

Install the KeyMod app, connect to your KeyMod hardware, and send your first keystroke in under 5 minutes.

## What You Need

- **Openterface KeyMod hardware** — powered on and within range
- **Phone or tablet** — Android or iOS/iPadOS with the KeyMod app installed
- **USB cable** (for initial setup) — USB-C to connect your phone to the KeyMod device
- **Bluetooth** (optional) — for wireless connection after initial setup

## Step 1: Install the KeyMod App

**Android:**

1. Open your phone's browser and go to the [KeyMod GitHub Releases page](https://github.com/TechxArtisanStudio/Openterface_KeyMod_Android/releases)
2. Download the latest `.apk` file
3. Tap the downloaded file to install
4. If Android asks, allow **"Install unknown apps"** for your browser

Alternatively, build from source — see [Build from Source](#build-from-source) below.

**iOS / iPadOS:**

KeyMod is available on the App Store for iPhone and iPad running iOS 16 or later.

## Step 2: Connect to Your KeyMod Device

KeyMod connects to the Openterface KeyMod hardware in two ways:

### USB Connection (recommended for first-time setup)

1. Plug your phone into the KeyMod device using a USB-C cable
2. Open the KeyMod app
3. Tap the connection icon (top-right corner of the main screen)
4. Tap **"USB Connection"**
5. Accept the USB permission prompt (Android) or confirm the connection (iOS)
6. You should see a green **"Connected"** status indicator

### Bluetooth Connection (wireless)

1. Make sure Bluetooth is enabled on your phone
2. Open KeyMod and tap the connection icon
3. Tap **"Bluetooth Connection"**
4. Wait for your KeyMod device to appear in the scan list
5. Tap it to pair
6. You should see a green **"Connected"** status indicator

> **Tip:** Enable **"Auto-connect on startup"** in the connection dialog so KeyMod reconnects automatically every time you open it. The app remembers your last connection type (USB or BLE).

## Step 3: Pick Your Mode — Welcome & Guide

After launching, you'll see the **Welcome & Guide** screen with mode cards:

```
Portrait mode (phone held upright):     Landscape mode (phone held sideways):

+-------------------+                   +-------------------------------+
|  KeyMod           |                   | KeyMod      | KB  | GP  | MC |
| Choose mode       |                   |             |     |     |    |
|                   |                   |             | SC  | VC  | PR |
| [Keyboard] [Game] |
| [Macros ] [Short] |                   Tap any card to enter that mode
| [Voice  ] [Present]                   or use the sidebar (hamburger)
+-------------------+                   menu to navigate.

"Remember my choice" checkbox: skips this screen next time.
"Skip" button: goes directly to last-used mode.
```

**"Remember my choice"** — check this box to skip the Welcome screen on future launches and go directly to your last-used mode.

**"Skip" button** — bypass the Welcome screen and enter your previously-used mode immediately.

## Step 4: Send Your First Keystroke

1. Select **Keyboard & Mouse** mode
2. Tap any key on the on-screen keyboard
3. The corresponding keystroke is sent to the target computer

That's it! You're now controlling your target computer remotely.

## Connection State Indicators

| Indicator | Meaning |
|---|---|
| **Green** (connected icon) | Active connection, ready to send input |
| **Amber/Blue** (connecting icon) | Connection in progress |
| **Gray** (disconnected icon) | No active connection |
| **Signal bars** | BLE signal strength or USB active status |

## Build from Source (Android, for Developers)

```bash
# Clone the repository
git clone https://github.com/TechxArtisanStudio/Openterface_KeyMod_Android.git
cd Openterface_KeyMod_Android

# Build (requires Java 21 and Android SDK 35)
./gradlew assembleDebug

# The APK will be at:
ls app/build/outputs/apk/debug/KeyMod-debug.apk

# Install on a connected device
adb install -r app/build/outputs/apk/debug/KeyMod-debug.apk
```

## Next Steps

- **[Keyboard & Mouse →](02-keyboard-mouse.md)** — Typing, modifiers, touchpad, and text input
