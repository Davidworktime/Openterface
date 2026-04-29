---
title: "KeyMod Tutorial - Numpad"
description: "Use the KeyMod numeric keypad for data entry, with HID numpad key codes and application-specific grids."
keywords: "KeyMod numpad, numeric keypad, HID numpad, data entry"
---

# 9. Numpad

A full numeric keypad for data entry. Each key sends the corresponding HID numpad key code.

## Key Mapping

| Key | HID Usage Code |
|-----|---------------|
| 0-9 | 0x62, 0x59-0x61 |
| +, -, *, / | 0x57, 0x56, 0x55, 0x54 |
| Enter | 0x58 |
| . / = | 0x63 / 0x67 |
| NumLock | 0x53 |

## Application-Specific Grids

Some shortcut profiles (Blender, Fusion 360, KiCad) include **custom numpad grids** tailored to their specific applications.

## Next Steps

- **[← Gamepad](08-gamepad.md)** — Virtual game controller
- **[Presentation →](10-presentation.md)** — Slide remote control
