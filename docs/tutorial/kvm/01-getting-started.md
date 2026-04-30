# KVM Tutorial 01 — Getting Started

**Audience:** Beginners — first-time users of Openterface KVM devices

---

## 1. What Is a KVM-over-USB?

A KVM (Keyboard, Video, Mouse) device sits between your **host computer** (your workstation) and a **target computer** (server, mini PC, embedded device). It:

- **Captures** the target's HDMI video output (and audio, if available)
- **Relays** your keyboard and mouse input through HID emulation
- All over a single USB cable — no network required

This is what sets KVM devices apart from remote desktop software: you can control the target even in **BIOS/UEFI**, during boot, or when the OS has crashed.

### Openterface KVM Devices

| Device | Form Factor | Key Feature |
|--------|------------|-------------|
| **Mini-KVM** | Compact USB dongle | Desktop KVM-over-USB |
| **KVM-Go** | Toolkit-style portable | On-the-go KVM with built-in cables, **iPadOS support via BLE** |
| **uConsole KVM Extension** | Internal module | Built-in KVM for ClockworkPi uConsole |

> Looking for **KeyMod** (keyboard & mouse emulator only, no video)? See the [KeyMod Tutorial](../../keymod/index.md).

---

## 2. What You Need

### Hardware

- **Openterface KVM device** — Mini-KVM, KVM-Go, or uConsole KVM Extension
- **Host computer** — Running macOS, Windows, Linux, or Android
- **Target computer** — Any computer with HDMI output
- **HDMI cable** — From target's HDMI output to the KVM's HDMI input
- **USB cable** — From KVM to your host computer (provides both power and data)

### Optional

- **USB switch cable** — From KVM to the target device's USB port (for keyboard/mouse emulation)
- **Keyboard and mouse** — Plug into the KVM's USB switchable port to control either host or target

---

## 3. Installation

### Host Application

| Platform | Application | Download |
|----------|------------|----------|
| **macOS** | Openterface for macOS | [App Store](/appstore) or [DMG](app/mmacos/dmg-installation.md) |
| **Windows** | Openterface QT | [GitHub Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases) |
| **Linux** | Openterface QT | [Flatpak](https://flathub.org/apps/com.openterface.openterfaceQT), .deb, .rpm, AppImage |
| **Android** | Openterface for Android | [Google Play](https://play.google.com/store/apps/details?id=com.openterface.AOS) or [GitHub Releases](https://github.com/TechxArtisanStudio/Openterface_Android/releases) |
| **iPadOS** | Openterface for iPadOS | [App Store](/app/ipados/) — **KVM-Go only** |

### Android Requirements

The Android app requires:

- **Android 8.0 (API 26)** or later
- **USB OTG support** — most modern phones support it (Samsung, Google Pixel, OnePlus). Verify by connecting a USB flash drive with an OTG adapter
- **USB OTG cable or adapter** to connect the KVM device to your phone

### iPadOS Requirements

The iPadOS app requires:

- **iPadOS 17.0** or later
- **KVM-Go device** — iPadOS connects to the KVM-Go dongle via **Bluetooth Low Energy (BLE)** for keyboard/mouse input, and the USB capture card for video
- **Camera and Microphone permissions** — needed for video preview and audio monitoring from the capture card
- **Bluetooth permission** — required to discover and connect to the KVM-Go dongle for HID input
- **Photo Library permission** (optional) — to save screenshots and recordings to the Photos app

### macOS Permissions

On first launch, macOS will request:

| Permission | Why |
|-----------|-----|
| **Camera** | Captures video from the HDMI capture chip |
| **Microphone** | Captures audio from the target (if enabled) |
| **Accessibility** | Required for HID mouse control in Relative mode |

### Linux Permissions

- Add your user to the `dialout` and `video` groups: `sudo usermod -a -G dialout,video $USER`
- Install udev rules for device access
- **BrlTTY conflict:** Remove `brltty` or blacklist the serial chip — see [Troubleshooting](04-troubleshooting.md#brltty-conflict-linux)

### Windows

- The installer bundles the CH340 serial driver. For portable builds, install it separately.

---

## 4. Connecting the Hardware

```
┌─────────────┐                        ┌──────────────────┐
│   TARGET    │─── HDMI cable ────────▶│  Openterface     │
│  COMPUTER   │                        │  KVM Device      │
└─────────────┘                        │                  │
                                       │  ◄── USB cable ──│── USB switch cable ──▶ Target USB port
                                       └──────────────────┘
                                                │
                                                ▼
                                       ┌──────────────────┐
                                       │   HOST COMPUTER  │
                                       │  (this app)      │
                                       └──────────────────┘
```

1. Connect the target's **HDMI output** to the KVM's **HDMI input**
2. Connect the KVM's **USB** to a **USB port on your host computer**
3. (Optional) Connect the USB switch cable from the KVM to the target's USB port
4. (Optional) Plug your keyboard/mouse into the KVM's USB switchable port
5. **Power on** the target device

### Device Detection

The KVM enumerates as multiple USB devices:
- **Video capture** (MS2109/MS2109S/MS2130S) — appears as a webcam
- **Serial** (CH9329 or CH32V208) — `/dev/ttyUSB*` (Linux), `COM*` (Windows), `cu.usbserial-*` (macOS)
- **HID** — used for firmware operations

### Connecting via Android Phone

When using the Android app, the connection chain uses USB OTG:

```
┌──────────────┐     HDMI      ┌──────────────────┐
│              │ ────────────▶ │   Openterface     │
│  Target PC   │               │   KVM Device      │
│  (screen)    │ ◀─────────── │                   │
│              │     USB       │                   │
└──────────────┘               └────────┬─────────┘
                                        │
                                   USB OTG
                                        │
                               ┌────────▼─────────┐
                               │  Android Phone    │
                               │  (Openterface)    │
                               └──────────────────┘
```

Connection order for Android:

1. **HDMI:** Connect target's HDMI output to the KVM's HDMI **input**
2. **USB (target):** Connect target's USB port to the KVM's USB port — carries mouse/keyboard signals
3. **USB OTG (phone):** Connect the KVM to your Android phone via USB OTG cable/adapter
4. **Power:** Power on the KVM device (if separate power input) and the target computer

When connected successfully, the video preview switches from a placeholder to the target's live screen, and tapping the phone screen moves the cursor on the target.

### Connecting via iPadOS

The iPadOS app uses a different connection model: **BLE for input** and **USB capture for video**.

```
┌──────────────┐     HDMI      ┌──────────────────┐
│              │ ────────────▶ │   KVM-Go Dongle   │
│  Target PC   │               │                   │
│  (screen)    │ ◀─── USB ──── │                   │
└──────────────┘               └────────┬─────────┘
                                        │
                              ┌─────────┴─────────┐
                              │   USB Capture     │ (video)
                              │   BLE (FFF2)      │ (keyboard/mouse)
                              └─────────┬─────────┘
                                        │
                              ┌─────────▼─────────┐
                              │     iPad           │
                              │  (Openterface)     │
                              └───────────────────┘
```

Connection order for iPadOS:

1. **Hardware:** Plug the KVM-Go dongle into the target PC's USB port and connect the HDMI input
2. **Power on** the target computer
3. **Open the app** on your iPad and grant camera, microphone, and Bluetooth permissions
4. **Tap the BLE button** in the toolbar — the app scans for devices named `kvm*`
5. **Tap Connect** next to your KVM-Go device — the button turns green with RSSI signal strength
6. **Verify:** the video preview shows the target's screen, tapping sends clicks, typing sends keystrokes

> **Note:** The iPadOS app only works with **KVM-Go**. Mini-KVM and uConsole KVM Extension do not have BLE support.

---

## 5. First Launch

### The Main Window

```
┌─────────────────────────────────────────────────────────┐
│  Menu Bar / Toolbar                                     │
├─────────────────────────────────────────────────────────┤
│                                                         │
│              VIDEO DISPLAY AREA                          │
│         (shows target device screen)                     │
│                                                         │
├─────────────────────────────────────────────────────────┤
│  Status Bar │ Port │ Keys │ Mouse │ Resolution │        │
└─────────────────────────────────────────────────────────┘
```

### Android Permissions

On first launch, the Android app requests:

| Permission | Why | What Happens If Denied |
|---|---|---|
| **USB Host** | Communicate with the Openterface hardware | App can't detect your KVM device |
| **Camera** | Receive video from the HDMI capture chip | No video preview |
| **Storage** | Save screenshots and recordings | Can't save captures |

Grant all permissions for full functionality. A system USB permission dialog also appears when the KVM device is detected — tap **Allow**.

### iPadOS Permissions

On first launch, the iPadOS app requests:

| Permission | Why | What Happens If Denied |
|---|---|---|
| **Camera** | Receive video from the HDMI capture card | No video preview |
| **Microphone** | Monitor target PC audio through iPad speakers | No audio monitoring |
| **Bluetooth** | Discover and connect to KVM-Go for HID input | Can't send keyboard/mouse input |
| **Photo Library** | Save screenshots and recordings | Captures still save to app Documents folder |

If you accidentally denied a permission, go to **Settings > Privacy & Security** to re-enable it.

### Verifying Connection

- **HDMI indicator:** green = signal detected, orange = no signal, gray = unknown
- **Keyboard indicator:** green = connected, orange = not found, gray = unknown
- **Mouse indicator:** green = connected, orange = not found, gray = unknown
- **Serial port:** should show a port name and baud rate (9600 or 115200)

If indicators show orange or gray, see [Troubleshooting](04-troubleshooting.md).

---

## 6. Basic KVM Control

### Mouse Modes

| Mode | Description | Best For |
|------|-------------|----------|
| **Absolute** (default) | Host cursor maps directly to target screen | General use, GUI navigation |
| **Relative (HID)** | Mouse movements sent as deltas via HID | Gaming, fast-paced interaction |

Switch via the toolbar toggle or **Control > Mouse Mode**.

### Keyboard Input

All keystrokes are forwarded to the target whenever the app window is focused:
- Standard keys, function keys, modifiers
- Special keys: Ctrl+Alt+Del, Print Screen
- **Paste to Target:** Sends clipboard text as emulated keystrokes

### USB Switching

Toggle the USB switchable port between:
- **Host** — your keyboard/mouse controls the host computer
- **Target** — your keyboard/mouse controls the target computer

---

## 7. Next Steps

- **[Basic Operations →](02-basic-operations.md)** — Mouse, keyboard, video, audio, recording
- **[Advanced Features →](03-advanced-features.md)** — EDID, firmware, macros, scripts
- **[Troubleshooting →](04-troubleshooting.md)** — Common problems and solutions
