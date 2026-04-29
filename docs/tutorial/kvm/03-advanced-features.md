# KVM Tutorial 03 — Advanced Features

**Audience:** Intermediate to Expert — power user features and configuration

---

## 1. Preferences System

### Video

- **Resolution & frame rate** — Preferred capture settings
- **Media backend** — FFmpeg, GStreamer (Linux), or Qt Multimedia (Windows)
- **Hardware acceleration** — VAAPI (Intel/AMD), V4L2-M2M (Raspberry Pi)
- **Aspect ratio & scaling** — Custom ratio, Stretch/Fit/Fill

### Audio

- **Enabled** — Toggle audio capture from target
- **Input/Output device** — Select source and playback device

### Target Control

- **Mouse mode** — Absolute, Relative (HID), Relative (Events)
- **Mouse event throttle** — 30–1000 events/second
- **Keyboard layout** — Target OS and regional layouts
- **Repeating keystroke interval** — Held key repeat speed
- **Auto-hide cursor** — Hide host cursor over video area

### Logging

- **Log level** — Debug, Info, Warning, Error
- **Log to file** — `~/Documents/openterface.log` (macOS) or configured path (Qt)
- **Serial logging** — Separate serial communication log

---

## 2. EDID Management

### What Is EDID?

EDID (Extended Display Identification Data) is what the KVM device sends to the target to describe its display capabilities — supported resolutions, refresh rates, vendor info. The KVM acts as a "fake monitor," so EDID determines what resolutions the target will output.

### Editing EDID

You can:
1. View the current EDID data
2. Edit supported resolutions
3. Add custom resolution entries
4. Flash the updated EDID to the device's firmware

**Access:** Settings > EDID Display Name Editor (macOS) or Device > Update Display Settings (Qt)

### Use Cases

- **Identifying the display** in target OS settings
- **Forcing specific resolution profiles** — some OSes use display name to select defaults
- **Custom naming** in multi-monitor setups

---

## 3. Macro System (macOS)

Macros are saved keyboard action sequences triggered from the toolbar macro panel.

### Key Sequence Format

**Modifier Tags:** `<CTRL>`, `<SHIFT>`, `<ALT>`, `<CMD>` (maps to Cmd/Win/Super depending on target OS)

**Special Keys:** `<ESC>`, `<BACK>`, `<ENTER>`, `<TAB>`, `<SPACE>`, `<LEFT>`, `<RIGHT>`, `<UP>`, `<DOWN>`, `<HOME>`, `<END>`, `<DEL>`, `<PGUP>`, `<PGDN>`, `<F1>`–`<F12>`

**Delays:** `<DELAY05s>`, `<DELAY1S>`, `<DELAY2S>`, `<DELAY5S>`, `<DELAY10S>`

### Examples

```
<CMD>c</CMD>              # Copy on macOS
<CTRL>c</CTRL>            # Copy on Windows
<DELAY05s><ENTER>         # Wait, then press Enter
```

### AI-Assisted Generation

The macro editor's **Magic** button generates macros from natural language. Describe what you want and the AI produces the key sequence.

### Verification

Mark macros as **verified** after testing. Only verified macros are available to the AI agent for autonomous execution.

---

## 4. Script Tool (Qt)

An AutoHotKey-inspired scripting language for automating keyboard and mouse actions on the target.

### Opening

Menu: **Device > Script Tool**

### Commands

| Command | Description | Example |
|---------|-------------|---------|
| `Sleep` | Pause execution | `Sleep 1000` |
| `Send` | Send keystrokes | `Send Hello World` |
| `Click` | Mouse click | `Click 100 200` |
| `SetCapsLockState` | Toggle CapsLock | `SetCapsLockState On` |
| `FullScreenCapture` | Screenshot | `FullScreenCapture "/tmp/shot.png"` |

### Modifier Prefixes

`^` = Ctrl, `+` = Shift, `!` = Alt, `#` = Win

---

## 5. Firmware Updates

### When to Update

- New hardware features
- Bug fixes
- Compatibility improvements

### Update Process

1. Open Firmware Update Tool (**Settings > Firmware Update Tool** on macOS, **Device > Update Firmware** on Qt)
2. The tool checks for the latest version from the network
3. Progress is tracked during the write operation
4. **Do not disconnect the device during update**

### Recovery

1. Keep the device powered
2. Close and reopen the Firmware Update Tool, retry
3. Use the Serial Reset Tool if the device is unresponsive

---

## 6. Serial Reset Tool

**Access:** Settings > Serial Reset Tool (macOS) or Device > Factory Reset HID Chip (Qt)

Use when:
- Device is in an unknown state after failed firmware update
- HID chip is not responding
- Preparing the device for resale

---

## 7. Diagnostics (Qt)

Menu: **Device > Device Diagnostics**

Runs hardware tests sequentially:
1. Serial connection test
2. Target USB status
3. Factory reset test
4. High/low baudrate test
5. Stress test (rapid commands, measure success rate)
6. Plug & play test (USB disconnect/reconnect detection)

After running, export results via the **Support Email Dialog**.

---

## 8. AI Chat System (macOS)

Built-in AI assistant that can analyze the target screen, suggest actions, and execute keyboard/mouse operations.

### Chat Modes

| Mode | Description |
|------|-------------|
| **Interactive** | Ask questions, get guidance |
| **Agentic** | AI autonomously plans and executes multi-step tasks |
| **Guide** | One instruction at a time, step by step |
| **Planner** | Complex requests broken into structured plans |

### Configuration

Settings > AI Chat: API endpoint, key (stored in Keychain), model, target system (macOS/Windows/Linux/etc.)

---

## 9. Remote Control (VNC/RDP — macOS)

Switch between **Hardware KVM**, **VNC**, and **RDP** modes via **Control > Connection Protocol**.

| Scenario | Mode |
|----------|------|
| Target in BIOS/UEFI, no network, booting, crashed | Hardware KVM |
| High-bandwidth desktop use, Windows server | VNC or RDP |

---

## 10. TCP Server (Qt)

Built-in TCP server for remote control on port 12345.

### Commands

`CHECK_STATUS`, `GET_LAST_IMAGE`, `GET_TARGET_SCREEN`, `SCRIPT_COMMAND`

### Python Example

```python
import socket
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect(("localhost", 12345))
sock.send(b"CHECK_STATUS\n")
print(sock.recv(4096).decode())
sock.close()
```

> **Security:** No authentication, encryption, or rate limiting. Only enable on trusted networks.

---

## Next Steps

- **[Troubleshooting →](04-troubleshooting.md)** — Common problems and solutions
