# KeyMod Tutorial 02 — Keyboard & Mouse

**Audience:** Beginners to Intermediate — daily use features

---

## 1. Keyboard Input

### How It Works

When KeyMod is switched to **Target** mode, every keystroke from your connected keyboard is captured by the KeyMod's HID controller chip (CH9329 or CH32V208) and sent to the target computer as if a native USB keyboard were plugged in.

- **Standard keys** — All alphanumeric keys, function keys, modifiers
- **Special keys** — CapsLock, NumLock, ScrollLock state tracking
- **Media keys** — Play/pause, volume controls (if supported by the target)

### Keyboard Layouts

The KeyMod application supports different physical keyboard layouts to correctly map scancodes to the target:

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

### Target OS Mapping

Set the target OS to match the target computer's key conventions:

| Target | Key Mapping |
|--------|-------------|
| **Windows** | Alt, Ctrl, Win key behavior |
| **Mac** | Cmd, Option key behavior |
| **Linux** | Super, Meta key behavior |

---

## 2. Mouse Control

### Absolute Mode (Default)

Mouse position on the host maps directly to the target screen. Both cursors are visible.

- **Best for:** General use, desktop navigation, BIOS access

### Relative Mode

Mouse movements are sent as relative deltas to the target. The host cursor is hidden.

- **Best for:** Gaming, applications needing raw mouse input
- **Requirements:** Accessibility permission on macOS
- **Exit:** Use the configured keyboard shortcut or long-press Esc

### Performance Presets

| Preset | Throttle | Baudrate | Use Case |
|--------|----------|----------|----------|
| Low Performance | 30 Hz | 9600 | Slow target devices |
| Casual Use | 80 Hz | 9600 | Everyday use |
| Gaming | 250 Hz | 115200 | Responsive gaming |
| Max Performance | 1000 Hz | 115200 | Maximum responsiveness |

---

## 3. USB Switching

### Switching Between Host and Target

Toggle your keyboard/mouse between:

- **Host** — Peripherals control your host computer normally
- **Target** — Peripherals control the remote device via HID emulation

Switch via:
- **Hardware switch** on the KeyMod device (physical button)
- **Software toggle** in the application toolbar
- **Keyboard shortcut** — Configured in your OS's keyboard shortcuts settings

### Important Notes

- When switching, give the target a moment to detect the HID device
- Eject any storage devices before switching if using a switchable USB port
- The KeyMod supports hot-switching — no reboot needed on either machine

---

## 4. Paste to Target

Send clipboard text from the host to the target via emulated keystrokes. Useful for pasting commands, URLs, or configuration text.

> **Note:** Only ASCII characters are supported. Long text may lose formatting.

---

## 5. BIOS / Pre-Boot Access

KeyMod works at the hardware level, so you can control BIOS, UEFI, and bootloader screens on the target — just like a physically connected keyboard and mouse.

Common BIOS access keys:
- **F2:** Dell, Lenovo, ASUS
- **F10:** HP
- **Del:** ASUS, Gigabyte, MSI
- **Option:** Apple

---

## Next Steps

- **[Advanced Features →](03-advanced-features.md)** — Firmware, macros, serial debug
- **[Troubleshooting →](04-troubleshooting.md)** — Common problems and solutions
