# KVM Tutorial 02 — Basic Operations

**Audience:** Beginners to Intermediate — daily use features

---

## 1. Mouse Control

### Absolute Mode (Default)

The host mouse cursor maps directly to the target screen. Both cursors are visible.

- **Best for:** General use, server management, BIOS navigation
- **Cursor behavior:** Auto-hide or always show host cursor over the video area

### Relative (HID) Mode

Mouse movements are sent as relative deltas through the HID interface. The host cursor is hidden.

- **Best for:** Gaming, applications needing raw mouse input
- **Requirements:** Accessibility permission on macOS
- **Exit:** Global keyboard shortcut (macOS) or long-press Esc (Qt)

### Performance Presets (macOS)

Under **Control > Mouse Mode > Performance Presets**:

| Preset | Throttle | Baudrate | Use Case |
|--------|----------|----------|----------|
| Low Performance Target | 30 Hz | 9600 | Slow target devices |
| Casual Use | 80 Hz | 9600 | Everyday server management |
| Gaming | 250 Hz | 115200 | Responsive gaming |
| Max Performance | 1000 Hz | 115200 | Maximum responsiveness |

Higher throttle = more responsive. Higher baudrate = faster serial communication.

---

## 2. Keyboard Input

### Standard Input

All keystrokes typed while the app window is focused are forwarded to the target.

### Special Keys

Send key combinations via the toolbar keys panel or **Control > Special Keys**:

- **F1–F12:** Function keys
- **Ctrl+Alt+Del:** Windows three-finger salute
- **Print Screen:** Screenshot key
- **Ctrl+Alt+F2:** Linux VT switch

### Keyboard Layout

Set the target OS layout to match the target computer:

| Layout | Behavior |
|--------|----------|
| **Windows** | Maps host keys to Windows conventions |
| **Mac** | Maps host keys to Mac conventions |
| **Linux** | Maps host keys to Linux conventions |

Regional layouts (QWERTY UK, Danish, QWERTZ German, AZERTY French, Japanese, etc.) are also available in the Qt application.

### Paste to Target

The app sends clipboard text as emulated keystrokes to the target. Useful for usernames, commands, URLs.

> **Note:** Only ASCII characters are supported. Long text may lose formatting or drop characters on older/busy systems.

**Configuring paste behavior (macOS):**
- **Ask Every Time:** Prompts host or target each time
- **Host Paste:** Always sends to target
- **Local Paste:** Always pastes on host

---

## 3. Video Settings

### Resolution Display

The toolbar shows the current input resolution and FPS from the target. The resolution is determined by what the target outputs over HDMI.

### Supported Resolutions

| Resolution | Frame Rate Range |
|------------|-----------------|
| 640x480 | 5–60 Hz |
| 720x480 | 5–60 Hz |
| 800x600 | 5–60 Hz |
| 1024x768 | 10–60 Hz |
| 1280x720 | 10–60 Hz |
| 1280x1024 | 5–30 Hz |
| 1600x1200 | 5–30 Hz |
| 1920x1080 | 5–30 Hz |

### Changing Resolution

1. Configure the preferred resolution in video settings
2. Or use EDID settings to push custom resolution values to the target

### Aspect Ratio & Scaling

| Mode | Behavior |
|------|----------|
| **Active Resolution** | Auto-detects the active video area |
| **HID Resolution** | Uses resolution from capture card hardware |
| **Custom** | Manually set a ratio (16:9, 4:3, 21:9, etc.) |

**Scaling:** Stretch (fills window, may distort), Fit (letterboxing), Fill (may crop).

### Zoom

Zoom in/out, reset to fit, and scroll to pan when zoomed in.

### Video Backend (Qt)

| Backend | Platform | Notes |
|---------|----------|-------|
| **FFmpeg** | All | Recommended, hardware acceleration |
| **GStreamer** | Linux | Pipeline flexibility |
| **Qt Multimedia** | Windows | Simple fallback |

Switch via **Preferences > Video > Media Backend**. Restart after changing.

---

## 4. Audio from Target

The HDMI capture chip extracts audio from the HDMI signal and presents it as a USB audio input to the host.

### Enabling Audio

1. Click the audio icon or open audio settings
2. Enable audio capture
3. Select the correct input device (e.g., "OpenterfaceA")
4. Select your host's output device

Audio is disabled by default on most platforms.

### Volume Control

- **Target side:** Adjust on the target computer
- **Host side:** Use your host OS audio mixer for the capture device

---

## 5. Screen Capture & Recording

### Screenshot

Click the camera icon on the toolbar. Images are saved to your OS's default media folder:
- **Linux:** `~/Pictures`
- **Windows:** `C:\Users\<name>\Pictures`
- **macOS:** Camera captures folder (via Camera menu)

### Recording

Click the record button to start/stop recording the target's video and audio stream. A timer appears while recording is active.

**Recording settings:**
- Output format (MP4, AVI, MOV, MKV)
- Video bitrate, audio codec
- Output directory

---

## 6. Connection Indicators

| Indicator | Green | Orange | Gray |
|-----------|-------|--------|------|
| HDMI | Signal detected | No signal | Unknown |
| Keyboard | Connected | Not found | Unknown |
| Mouse | Connected | Not found | Unknown |

### USB Switch

The USB switch toggle shows whether the switchable port is routed to **Host** or **Target**.

---

## 7. Preventing Screen Saver

Enable **Prevent Screen Saver** (via Edit/Device menu or toolbar) to send periodic events that keep the target display awake.

---

## 8. Full Screen Mode

Use the standard full screen button to fill the display with the video area, hiding UI chrome.

---

## Next Steps

- **[Advanced Features →](03-advanced-features.md)** — EDID, firmware, macros, scripts, diagnostics
- **[Troubleshooting →](04-troubleshooting.md)** — Common problems and solutions
