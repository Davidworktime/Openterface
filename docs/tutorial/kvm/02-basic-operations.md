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

### Android Mouse Modes

The Android app offers three ways to control the target mouse, switchable in the settings panel:

| Mode | How It Works | Best For |
|---|---|---|
| **Absolute (Default)** | Tap anywhere and the cursor jumps there and left-clicks. Position maps proportionally. | Most tasks |
| **Relative** | Drag your finger; cursor moves relative to your drag, like a laptop trackpad. Lift your finger and cursor stays put. | Fine cursor positioning |
| **Absolute Drag** | Tap and hold; cursor jumps and follows your finger. A "Drag" label appears. Release to drop. | Dragging files, selecting text |

**Mouse buttons on Android:** single tap = left-click, long press = right-click, double tap = double-click.

### iPadOS Mouse Modes

The iPadOS app offers two mouse modes, toggleable via the mouse mode button on the toolbar:

| Mode | Icon | How It Works | Best For |
|---|---|---|---|
| **Pan Mode** (Relative) | Hand icon | Finger acts like a laptop trackpad — drag to move cursor, tap to click | General desktop use, flat surface |
| **iPencil Mode** (Absolute) | Pencil icon | Touch position maps directly to target screen coordinates, like a drawing tablet | Precise pointing, Apple Pencil use |

**Gestures in both modes:**

| Gesture | Pan Mode | iPencil Mode |
|---|---|---|
| **Single tap** | Left-click | Move cursor to point + left-click |
| **Tap & drag** | Move cursor (relative) | Drag with left button held |
| **Double-tap** | Double-click | Double-click at point |
| **Long press** | Right-click | Right-click at point |
| **Two-finger tap** | Right-click | Right-click |
| **Two-finger drag** | Scroll wheel | Scroll wheel |

**Quick Menu:** Long-press on the video preview to open a menu with Left Click, Right Click, and Drag options.

**Drag Mode:** Double-tap & hold or select Drag from the quick menu — the left button stays held, a "Dragging Mode Active" label appears.

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

### Android On-Screen Keyboard

The Android app provides a full on-screen keyboard accessible via the keyboard button (⌨) at the bottom-right of the main screen:

| Control | What It Does |
|---|---|
| **ShortCut** | Pre-built shortcuts: Ctrl+C/V, Win+L, Ctrl+Alt+Del, Alt+F4, etc. |
| **Function** | F1–F12, PrtSc, ScrLk, navigation keys (Ins, Home, PgUp, etc.), arrows |
| **System** | QWERTY layout with letters, numbers, punctuation, Backspace, Enter |
| **Modifier keys** | Ctrl, Shift, Alt, Win — toggle buttons that auto-reset after the next key |

To send a combination like **Ctrl+Alt+Del**: tap Ctrl (highlights), tap Alt (both highlight), tap Del. All modifiers reset automatically after the key is sent.

The keyboard also supports **different regional layouts** (US, Japanese JIS, German QWERTZ, etc.) selectable in the settings panel. Zoom in/out buttons let you adjust key sizes.

### iPadOS Keyboard Input

The iPadOS app supports two keyboard input methods:

**Floating On-Screen Keyboard:** Tap the **Keyboard** button in the toolbar to show a draggable floating keyboard with a Mac-style layout:

| Row | Keys |
|---|---|
| **Top** | Esc, F1–F12, Del |
| **Number** | `, 1–0, -, =, Backspace |
| **QWERTY** | Tab, q–p, [, ], \, Enter |
| **Home row** | Caps, a–l, ;, ', Enter |
| **Bottom** | Shift, z–m, ,, ., /, Shift |
| **Modifiers** | Ctrl, Alt, Cmd, Space, Cmd, Alt, Ctrl |

- **Toggle modifiers:** Tap Ctrl, Shift, Alt, Cmd, or Caps to toggle on/off (highlighted in blue)
- **Keyboard modes:** Normal (standard typing) and Game (optimized HID packet header for game input)
- **Dragging:** Grab the drag handle in the header to reposition the keyboard anywhere on screen

**External iPad Keyboard:** Physical keyboards connected to the iPad (Bluetooth, Smart Connector, USB) are passed through directly to the target PC. Modifier keys send as press/release events, so combinations like `Ctrl+C` or `Alt+Tab` work naturally.

**Composite Key Shortcuts:** The app includes a library of common shortcuts accessible from the toolbar, organized by category:

| Category | Examples |
|---|---|
| **Navigation** | Ctrl+C/V/X/A/F, Ctrl+Home/End, Page Up/Down |
| **Editing** | Ctrl+Z/Y, Ctrl+B/I/U, Ctrl+D |
| **System** | Ctrl+S/O/P/R, F11, Alt+F4 |
| **Application** | Alt+Tab, Cmd+M, Cmd+Shift+3/4 (macOS screenshots) |

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

### Android Video Controls

On the Android app, video settings are accessed via the settings panel (Menu button ☰):

- **Video Format** — Select resolution (1920×1080, 1280×720, 640×480) and frame rate (30fps, 60fps). Lower resolution/frame rate if video is choppy.
- **Controls** — Real-time sliders for **brightness**, **contrast**, and **hue**
- **Rotate/Flip** — Rotate 90° CW/CCW, flip horizontally/vertically. Useful when the KVM device is mounted upside-down or sideways

The settings persist between sessions — you only configure them once.

### iPadOS Video Controls

On iPadOS, video controls are accessible from the bottom toolbar:

- **Resolution Switching** — Tap the **Video** button (shows current resolution) to choose from: 2160p (4K), 1080p (default), 720p, or 480p. Lower resolution for better performance on slower connections.
- **Zoom Mode** — Tap **Zoom** to enter zoom mode, then pinch with two fingers to zoom in. A zoom indicator shows the current level (e.g., `2.5x`). When zoomed, single-finger drag pans the viewport. Tap Zoom again to exit.
- **Fullscreen** — Tap **Fullscreen** to hide the toolbar and extend video to fill the entire screen. Tap the arrow button in the top-left to exit.
- **Screen Rotation** — Tap **Rotate** to cycle through orientation correction modes (Normal, 90° CW, 180°, 90° CCW). Useful when the KVM-Go dongle is mounted sideways or upside-down. Rotation applies to both live preview and saved captures.

When the camera is starting, a "Starting Camera..." loading indicator appears. If no camera is connected but permissions are granted, a guide image is shown.

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

### iPadOS Audio Monitoring

The iPadOS app lets you listen to the target PC's audio through your iPad's speakers or headphones:

- Tap the **Audio** button (speaker icon) in the toolbar to toggle monitoring
- **Icon states:** gray slashed speaker = not authorized, red slashed speaker = off, green speaker with waves = on
- On first use, the app requests microphone permission
- Audio plays through iPad speakers or connected headphones/Bluetooth audio
- **During recording:** monitoring audio is temporarily muted to prevent feedback, but audio is still captured into the recording file

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

### Android Screen Capture & Recording

On Android, access via the settings panel:

- **Screen Capture** — Tap to save a snapshot of the current video frame to your device's default media folder. Requires **Storage permission**.
- **Record Video** — Tap to start/stop recording. A red recording indicator with timer appears at the top. Video saves to your device's default media folder.

**Use cases:** record the target's boot process, capture error messages, document configuration steps.

### iPadOS Screen Capture & Recording

**Screenshots:** Tap the **Screenshot** button (camera icon) in the toolbar. The app captures a high-resolution frame, corrects for orientation, and saves as JPEG.

**Video Recording:** Tap the **Record** button to start/stop. After stopping, the app displays the recording details (duration and file size).

| Setting | Value |
|---|---|
| **Video codec** | H.264 at 30 fps |
| **Resolution** | Matches capture device (typically 1920×1080) |
| **Audio codec** | AAC at 128 kbps, 48 kHz, stereo |
| **Container** | MOV |

**File locations:**
- **App Documents:** `Documents/Recordings/` — browse via Files app > On My iPad > Openterface KVM > Recordings
- **Photos App:** If Photo Library permission is granted and enabled in settings
- **File naming:** `Openterface_YYYY-MM-DD_HH-mm-ss.jpg` (screenshots) or `.mov` (recordings)

**Use cases:** record the target's boot process, capture error messages, document configuration steps.

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
