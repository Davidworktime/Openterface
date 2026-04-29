# KeyMod Tutorial 01 — Getting Started

**Audience:** Beginners — first-time KeyMod users

---

## 1. What Is KeyMod?

KeyMod is a **keyboard and mouse emulator** — a compact USB device that lets you share a single keyboard and mouse between your host computer and a target device.

Unlike KVM devices, KeyMod does **not** capture video. It focuses on reliable HID (Human Interface Device) emulation: your keyboard and mouse signals are translated and routed to whichever machine you select.

This makes KeyMod ideal for:
- Using your favorite mechanical keyboard with a headless server or Raspberry Pi
- Switching peripherals between a desktop PC and a laptop without unplugging
- Managing devices where video is handled by a separate monitor or KVM

## 2. What You Need

### Hardware

- **KeyMod device** — Openterface KeyMod
- **Host computer** — Running macOS, Windows, or Linux
- **Target device** — Any computer with a USB port (server, Raspberry Pi, SBC, etc.)
- **USB cable** — From KeyMod to your host computer (power + data)
- **USB cable** — From KeyMod to the target device (HID emulation)

### Peripherals

- **Keyboard** — Plug into the KeyMod's peripheral port
- **Mouse** — Plug into the KeyMod's peripheral port (or use a combo keyboard+mouse dongle)

---

## 3. Installation

### Host Application

| Platform | Application | Download |
|----------|------------|----------|
| **macOS** | Openterface for macOS | [App Store](/appstore) or [DMG](macos/dmg-installation.md) |
| **Windows** | Openterface QT | [GitHub Releases](https://github.com/TechxArtisanStudio/Openterface_QT/releases) |
| **Linux** | Openterface QT | [Flatpak](https://flathub.org/apps/com.openterface.openterfaceQT), .deb, .rpm, AppImage |

### macOS Permissions

On first launch, macOS may request:

| Permission | Why |
|-----------|-----|
| **Accessibility** | Required for HID mouse control in Relative mode |
| **Camera** | Not required for KeyMod (no video) |

### Linux Permissions

- Add your user to the `dialout` group: `sudo usermod -a -G dialout $USER`
- Install udev rules for device access
- **BrlTTY conflict:** The `brltty` service may claim the serial chip — see [Troubleshooting](04-troubleshooting.md)

### Windows

- The installer bundles the CH340 serial driver. For portable builds, install separately.

---

## 4. Connecting KeyMod

```
┌─────────────┐     USB cable      ┌─────────────┐
│  KEYBOARD   │───────────────────▶│             │
└─────────────┘                    │   KeyMod    │       USB cable       ┌─────────────┐
                                   │   Device    │──────────────────────▶│   TARGET    │
┌─────────────┐                    │             │                       │  COMPUTER   │
│   MOUSE     │───────────────────▶│             │                       └─────────────┘
└─────────────┘                    └──────┬──────┘
                                          │
                               USB cable  │
                                          ▼
                                 ┌─────────────┐
                                 │    HOST     │
                                 │  COMPUTER   │
                                 │  (this app) │
                                 └─────────────┘
```

1. Plug your **keyboard and mouse** into the KeyMod's peripheral USB port(s)
2. Connect the KeyMod's **host USB cable** to your host computer
3. Connect the KeyMod's **target USB cable** to the target device
4. Launch the Openterface application on your host

---

## 5. First Use

### USB Switch

The KeyMod routes your keyboard and mouse to one of two destinations:

- **Switch to Host** — Your peripherals control the host computer (normal use)
- **Switch to Target** — Your peripherals control the target device (HID emulation)

Toggle the USB switch via:
- The hardware switch on the KeyMod device
- The software toggle in the application toolbar
- A configured keyboard shortcut

### Verifying Connection

In the application:
- **Keyboard indicator:** green = connected, orange = not found
- **Mouse indicator:** green = connected, orange = not found
- **Serial port:** should show a port name (e.g., `/dev/ttyUSB*`, `COM*`, or `cu.usbserial-*`) and baud rate

If indicators show orange, see [Troubleshooting](04-troubleshooting.md).

---

## 6. Next Steps

- **[Keyboard & Mouse →](02-keyboard-mouse.md)** — Input modes, layouts, performance
- **[Advanced Features →](03-advanced-features.md)** — Firmware, macros, serial debug
- **[Troubleshooting →](04-troubleshooting.md)** — Common problems and solutions
