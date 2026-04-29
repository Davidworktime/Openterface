---
title: "KeyMod Tutorial - Settings"
description: "Configure KeyMod settings including auto-connect, themes, language, BLE key delay, touchpad sensitivity, and target OS."
keywords: "KeyMod settings, auto-connect, theme, language, BLE delay, touchpad sensitivity"
---

# 11. Settings

Configure KeyMod's behavior and appearance.

## General Settings

| Setting | Android | iOS |
|---|---|---|
| **Auto-connect** | Reconnect to last device on startup | — |
| **Keep screen on** | Prevent screen sleeping (immersive mode) | — |
| **Haptic feedback** | Vibration on button presses | Automatic (Taptic Engine) |
| **Orientation lock** | Lock screen orientation | Toggle button in top bar |
| **Language** | English, 中文, Español, Français | System language |
| **Theme** | 8 color families, Dark/Light, Follow system | — |
| **BLE Key Delay** | — | 10ms default, adjustable (affects all text input) |
| **Clipboard monitoring** | — | Toggle clipboard detection on/off |
| **Touchpad sensitivity** | Scroll sensitivity slider | Mouse movement sensitivity |

## Target OS

Set the target OS to match the target computer's key conventions. This affects shortcut labels, Unicode input methods, and modifier key mapping.

| Target | Key Mapping |
|--------|-------------|
| **Windows** | Alt, Ctrl, Win key behavior |
| **Mac** | Cmd, Option key behavior |
| **Linux** | Super, Meta key behavior |

Change the target OS by tapping the **OS icon** in the header bar (Android) or using the segmented picker in the sidebar (iOS).

See [Target-Specific Keyboard](03-target-keyboard.md) for keyboard layout and Unicode input details.

## Settings Not Persisting (iOS)

Settings are stored in UserDefaults and should persist across app launches. If settings reset unexpectedly, check for iOS iCloud sync conflicts. Use Reset to Defaults and reconfigure if needed.

## Next Steps

- **[← Presentation](10-presentation.md)** — Slide remote control
- **[Troubleshooting →](12-troubleshooting.md)** — Common problems and solutions
