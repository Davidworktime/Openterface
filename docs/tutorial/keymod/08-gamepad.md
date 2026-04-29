---
title: "KeyMod Tutorial - Gamepad"
description: "Use KeyMod as a virtual game controller with customizable layouts for Xbox, PlayStation, and NES-style gamepads."
keywords: "KeyMod gamepad, virtual controller, game controller, WASD mapping, analog stick"
---

# 8. Gamepad

Transform your phone into a virtual game controller for gaming, retro emulation, and game testing.

## The Layout

```
+-----------------------------------+
| [L1]              [R1]           |
| [L2]              [R2]           |
|                                   |
|  [D-pad]          [A][B]         |
|  ▲                [X][Y]         |
| ◀ ▶                             |
|  ▼                              |
|             [Select] [Start]     |
|      [Left Stick]  [Right Stick] |
+-----------------------------------+
```

## Controls

| Control | How |
|---|---|
| D-pad | Tap the directional arrows |
| Action buttons (A, B, X, Y) | Tap them |
| Shoulder buttons | Tap L1, L2, R1, R2 at the top |
| Analog sticks | Touch and drag the stick circles |
| Start / Select | Tap the buttons |

## Customizing (iOS)

iOS supports three built-in controller layouts selectable from the top bar:

- **Xbox** — Standard Xbox-style with dual sticks, D-pad, A/B/X/Y, shoulder/trigger buttons
- **PlayStation** — PlayStation-style with Cross/Circle/Square/Triangle action buttons
- **NES** — Classic Nintendo Entertainment System (D-pad, A/B, Select/Start, no sticks)

### Analog Sticks (iOS)

- **Left stick → Keyboard keys:** Maps to arrow keys with diagonal support. Configurable to WASD in Edit Mode.
- **Right stick → Mouse movement:** Dynamic sensitivity (2.0–8.0), dead zone to prevent drift.
- **Hysteresis:** Activation (0.6) and deactivation (0.4) thresholds prevent key chatter at the boundary.

> **Note:** Gamepad HID protocol is under active development. Basic button support works; analog stick precision may vary.

## Customizing (Android)

- **Long-press any button or stick** to reconfigure it — assign any HID key to each component
- **Analog vs Key mode** — sticks can be configured as analog input or as key-mapped D-pad input
- **WASD mapping** — assign WASD keys to the left stick for PC gaming
- **Button/stick size scaling** — adjust sizes for your preferred touch area
- **Background image** — customize the gamepad background
- **Haptic feedback** — vibration on button press

## Troubleshooting

### Analog Stick Not Responding

| Symptom | Solution |
|---|---|
| **Stick not producing action** | Check the key mapping in Edit Mode → Key Mapping. Verify the stick isn't stuck in the dead zone (center area, 0.15 threshold). Check hysteresis thresholds — the stick needs to move past 0.6 activation to trigger. |
| **Buttons sending wrong keys** | Open Edit Mode → Key Mapping and check the button's key assignment. Tap the button to open the configuration popup and correct the mapping. Reset positions to defaults using the reset button. |

## Next Steps

- **[← AI Integration](07-ai.md)** — AI-assisted text refinement and command assistant
- **[Numpad →](09-numpad.md)** — Numeric keypad for data entry
