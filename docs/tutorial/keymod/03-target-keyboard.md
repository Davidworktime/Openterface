---
title: "KeyMod Tutorial - Target-Specific Keyboard"
description: "Configure keyboard layouts and target OS mapping so KeyMod sends the correct keys to Windows, macOS, or Linux computers."
keywords: "KeyMod keyboard layout, target OS, QWERTY, AZERTY, keyboard mapping, modifier keys"
---

# 3. Target-Specific Keyboard

KeyMod sends keystrokes that adapt to the target computer's operating system and keyboard layout. Configuring these settings correctly ensures the right keys arrive on the target.

## Keyboard Layouts

KeyMod supports different physical keyboard layouts to correctly map scancodes to the target:

| Layout | Notes |
|--------|-------|
| **QWERTY US** | Default |
| **QWERTY UK** | British layout |
| **QWERTZ German** | German layout |
| **AZERTY French** | French layout |
| **AZERTY Belgian** | Belgian layout |
| **QWERTY Danish** | Danish layout |
| **QWERTY Spanish** | Spanish layout |
| **QWERTY Swedish** | Swedish layout |
| **Japanese** | JIS layout |

Set your layout via **Settings > Keyboard Layout** to ensure keys are sent correctly to the target.

### Wrong Keyboard Layout Symptoms

| Symptom | Likely Cause |
|---------|-------------|
| `@` and `"` swapped | UK vs US layout mismatch |
| `Y` and `Z` swapped | QWERTY vs QWERTZ mismatch |
| `A` and `Q` swapped | QWERTY vs AZERTY mismatch |
| `¥` key not working | Japanese layout not selected |

## Target OS Mapping

Set the target OS to match the target computer's key conventions. This affects shortcut labels, Unicode input methods, and modifier key mapping.

| Target | Key Mapping |
|--------|-------------|
| **Windows** | Alt, Ctrl, Win key behavior |
| **Mac** | Cmd, Option key behavior |
| **Linux** | Super, Meta key behavior |

Change the target OS by tapping the **OS icon** in the header bar (Android) or using the segmented picker in the sidebar (iOS).

### Unicode Characters

Non-ASCII characters (Chinese, Japanese, emoji) require OS-specific input methods:

| OS | Method |
|---|---|
| **Windows** | Alt+NumPad hexadecimal Unicode input |
| **Linux** | Ctrl+Shift+U followed by hex code |
| **macOS** | Option+hex input |

If Unicode characters appear incorrectly, verify the **Target OS** is set correctly.

## Next Steps

- **[← Keyboard & Mouse](02-keyboard-mouse.md)** — Typing, modifiers, touchpad, and text input
- **[Shortcut Hub →](04-shortcuts.md)** — Profile-based keyboard shortcuts
