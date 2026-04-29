---
title: "KeyMod Tutorial"
description: "Complete guide to using the KeyMod app. Learn how to connect, control your computer from your phone, and use keyboard, mouse, gamepad, macros, and voice input modes."
keywords: "KeyMod tutorial, how to use KeyMod, phone keyboard guide, KeyMod app tutorial"
---

# KeyMod Tutorial

{% include "partials/keymod-slideshow.html" %}

This tutorial covers both the **Android** and **iOS/iPadOS** versions of the KeyMod app. Where features differ between platforms, we note it clearly.

## What is KeyMod?

KeyMod transforms your phone or tablet into a **universal input device** for any computer. It connects to the **Openterface KeyMod** hardware (a KVM — Keyboard, Video, Mouse switcher), which then sends your phone's keystrokes, mouse movements, and gamepad inputs to a target computer as if they came from a real USB keyboard and mouse.

### How the connection works

```
[ Your Phone ] ──USB/BLE──> [ KeyMod Hardware ] ──USB HID──> [ Target Computer ]
   (KeyMod app)                (CH9329 protocol)              (Windows/macOS/Linux)
```

The app communicates with the KeyMod hardware using the **CH9329 protocol** over a serial connection (USB-C at 115200 baud, 8N1, or Bluetooth BLE). The KeyMod device appears to the target computer as a standard USB keyboard and mouse — no drivers needed.

### Who is this for?

| You are... | KeyMod helps you... |
|---|---|
| **System Administrator** | Manage servers from your phone without carrying a spare keyboard and monitor |
| **Presenter / Speaker** | Control slides from anywhere in the room, no clicker needed |
| **Gamer** | Use your phone as a gamepad for retro gaming or as an extra controller |
| **Content Creator** | Trigger shortcuts, macros, and voice input while recording on another machine |
| **Power User** | Send complex keyboard shortcuts, text snippets, or automation sequences from your phone |
| **Anyone** | Type on your computer from your couch, bed, or across the room |

## Tutorial Sections

| Guide | Description |
|---|---|
| [1. Getting Started](01-getting-started.md) | Install, connect, and pick your first mode (5 minutes) |
| [2. Keyboard & Mouse](02-keyboard-mouse.md) | Typing, modifiers, touchpad, and text input |
| [3. Advanced Features](03-advanced-features.md) | Gamepad, Numpad, Shortcuts, Macros, Voice Input, Presentation, Settings, and AI |
| [4. Troubleshooting](04-troubleshooting.md) | Common problems and solutions |

## Getting Help

- **Bug reports:** [GitHub Issues (Android)](https://github.com/TechxArtisanStudio/Openterface_KeyMod_Android/issues) / [GitHub Issues (iOS)](https://github.com/TechxArtisanStudio/Openterface_KeyMod_iOS/issues)
- **Community:** [TechxArtisan Discord](https://discord.gg/techxartisan)
- **Source code:** [Android](https://github.com/TechxArtisanStudio/Openterface_KeyMod_Android) / [iOS](https://github.com/TechxArtisanStudio/Openterface_KeyMod_iOS)
