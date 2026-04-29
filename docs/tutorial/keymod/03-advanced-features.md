# KeyMod Tutorial 03 — Advanced Features

**Audience:** Intermediate to Expert — power user features

---

## 1. Preferences

### Target Control

- **Mouse mode** — Absolute or Relative
- **Mouse event throttle** — 30–1000 events/second
- **Keyboard layout** — Physical layout mapping
- **Repeating keystroke interval** — Held key repeat speed

### Serial Communication

- **Baudrate** — 9600 (default, reliable) or 115200 (faster)
- **Serial output logging** — Log raw serial communication for debugging

### Logging

- **Log level** — Debug, Info, Warning, Error
- **Log to file** — `~/Documents/openterface.log` (macOS) or configured path (Qt)

---

## 2. Firmware Updates

### Update Process

1. Open the Firmware Update Tool (**Settings > Firmware Update Tool** on macOS, **Device > Update Firmware** on Qt)
2. The tool checks for the latest version from the network
3. Progress is tracked during the write operation
4. **Do not disconnect the device during update**

### Recovery

1. Keep the device powered
2. Close and reopen the Firmware Update Tool, retry
3. Use the Serial Reset Tool if the device is unresponsive

---

## 3. Serial Reset Tool

**Access:** Settings > Serial Reset Tool (macOS) or Device > Factory Reset HID Chip (Qt)

Use when:
- Device is in an unknown state after failed firmware update
- HID chip is not responding to commands
- Preparing the device for resale

---

## 4. Serial Console (Qt)

Open via **Device > Serial Port Debug** to see real-time serial protocol messages between the host application and the HID controller chip.

### Message Filters

- **Keyboard** — Keypress and release events
- **Mouse Absolute** — Absolute position commands
- **Mouse Relative** — Relative movement commands
- **Mouse** — Button events
- **HID** — General HID communication
- **Chip Info** — Configuration and status

### Message Direction

- `>>` — Message sent from host to device
- `<<` — Message received from device to host

---

## 5. Macro System (macOS)

Macros are saved keyboard action sequences triggered from the application.

### Key Sequence Format

**Modifier Tags:** `<CTRL>`, `<SHIFT>`, `<ALT>`, `<CMD>` (maps to Cmd/Win/Super based on target OS)

**Special Keys:** `<ESC>`, `<BACK>`, `<ENTER>`, `<TAB>`, `<SPACE>`, `<LEFT>`, `<RIGHT>`, `<UP>`, `<DOWN>`, `<HOME>`, `<END>`, `<DEL>`, `<PGUP>`, `<PGDN>`, `<F1>`–`<F12>`

**Delays:** `<DELAY05s>`, `<DELAY1S>`, `<DELAY2S>`, `<DELAY5S>`, `<DELAY10S>`

### Examples

```
<CMD>c</CMD>              # Copy on macOS
<CTRL>c</CTRL>            # Copy on Windows
<DELAY05s><ENTER>         # Wait, then press Enter
```

### AI-Assisted Generation

The macro editor's **Magic** button generates macros from natural language descriptions.

### Verification

Mark macros as **verified** after testing. Verified macros are available to the AI agent for autonomous execution.

---

## 6. Script Tool (Qt)

An AutoHotKey-inspired scripting language for automating keyboard and mouse actions.

**Access:** Device > Script Tool

### Commands

| Command | Example |
|---------|---------|
| `Sleep` | `Sleep 1000` |
| `Send` | `Send Hello World` |
| `Click` | `Click 100 200` |
| `SetCapsLockState` | `SetCapsLockState On` |

### Modifier Prefixes

`^` = Ctrl, `+` = Shift, `!` = Alt, `#` = Win

---

## 7. Diagnostics (Qt)

**Access:** Device > Device Diagnostics

Tests:
1. Serial connection test
2. Target USB status
3. Factory reset test
4. High/low baudrate test
5. Stress test
6. Plug & play test

---

## Next Steps

- **[Troubleshooting →](04-troubleshooting.md)** — Common problems and solutions
