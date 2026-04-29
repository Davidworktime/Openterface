# KVM Tutorial 04 — Troubleshooting

Common problems and solutions for Openterface KVM devices.

---

## Device Not Detected

### Symptoms
- "No devices found" in device menu
- Keyboard and mouse indicators show orange or gray
- Serial port shows "N/A"

### Diagnosis

**Linux:**
```bash
lsusb | grep -E "534d|1a86"
dmesg | tail -20
ls /dev/hidraw*   # HID video chip
ls /dev/ttyUSB*   # serial chip
```

Expected: `534d:2109` (HDMI capture) and `1a86:7523` or `1a86:fe0c` (serial).

**macOS:** Apple Menu > About This Mac > System Report > Hardware > USB — look for Openterface.

**Windows:** Device Manager > "Universal Serial Bus devices" and "Ports (COM & LPT)" — CH340 should appear as "USB-SERIAL CH340 (COMx)".

### Solutions

| Problem | Fix |
|---------|-----|
| Device not in lsusb/System Report | Try different USB cable/port. Needs USB 2.0+ |
| Device appears but no nodes | Check udev rules (Linux) or reinstall drivers (Windows) |
| Permission denied | Add user to `dialout` and `video` groups (Linux) |
| Detected then disappears | `brltty` claiming the serial port (Linux) — see below |

---

## BrlTTY Conflict (Linux)

**The most common cause of keyboard/mouse failure on Linux.**

The `brltty` (Braille terminal) service claims USB serial devices, including the CH9329/CH32V208 chip.

### Fix
```bash
# Option 1: Remove brltty (if you don't need Braille support)
sudo apt remove brltty          # Debian/Ubuntu
sudo dnf remove brltty          # Fedora

# Option 2: Blacklist the device (preferred)
echo 'ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7523", ENV{BRLTTY_BRAILLE_DRIVER}=""' | sudo tee /etc/udev/rules.d/99-brltty-openterface.rules
sudo udevadm control --reload-rules
```

---

## No Video / Black Screen

### Steps

1. **Verify HDMI cable** securely connected at both ends
2. **Check target device** is outputting HDMI (test with a regular monitor)
3. **Try a different HDMI cable**
4. **Reconnect the device** — the app handles hot-plug events
5. **Check video chipset detection:** Supported: MS2109, MS2109S, MS2130S

### Backend Selection (Qt)

If one backend shows a black screen, try another via **Preferences > Video > Media Backend**:
- **FFmpeg** — Most reliable (recommended)
- **GStreamer** — Linux only
- **Qt Multimedia** — Windows fallback

### GStreamer Issues (Linux)

```bash
GST_DEBUG=3 ./openterfaceQT 2>&1 | grep -i error
```

Try a different sink:
```bash
OPENTERFACE_GST_SINK=xvimagesink ./openterfaceQT
```

### EDID Mismatch

If the target doesn't recognize the EDID, it may not output a compatible resolution. Try changing the target's output resolution or edit the EDID via the app's display settings.

---

## Keyboard/Mouse Not Responding

### Steps

1. **Check USB switch toggle** — make sure it's set to **Target**, not Host
2. **Verify serial port status** — should show a port name, not "N/A"
3. **Try switching baud rate** — 9600 or 115200
4. **Check control chipset** — Supported: CH9329, CH32V208
5. **Verify CTS monitoring** — The app monitors Clear-To-Send lines for HID events

### Mouse-Specific Issues

- **Relative mode on macOS:** Requires Accessibility permission. Check **System Settings > Privacy & Security > Accessibility**
- **Absolute mode:** Verify aspect ratio matches target display
- **Mouse lag:** Try higher performance preset or increase baudrate
- **Serial port conflicts (Linux):** Close other apps using the port: `sudo lsof /dev/ttyUSB0`

---

## Audio Not Playing

### Steps

1. **Enable audio** via the audio icon > Enable Audio
2. **Check microphone permission** — System Settings > Privacy & Security > Microphone (macOS)
3. **Select correct input device** — "OpenterfaceA" or capture device name
4. **Select correct output device** — your speakers or headphones
5. **Check target's HDMI audio output** — is the target configured to send audio over HDMI?

---

## USB Serial Driver Issues

### macOS

```bash
kextstat | grep com.apple.driver.usb.cdc
```

If needed, install WCH CH34x driver from [WCH CH34xDriver GitHub](https://github.com/WCHSoftGroup/ch34xser_macos). Enable in **System Settings > General > Login Items & Extensions > Driver Extensions**.

### Windows

If serial chip doesn't appear in Device Manager, install the CH340/CH341 driver. The installer typically bundles it; for portable builds, download separately.

### Linux

The CH340 driver (`ch341` module) is built into the kernel:
```bash
lsmod | grep ch341
dmesg | grep ch341
```

---

## Firmware Update Fails

### USB Stability

- Do not unplug during flashing
- Do not suspend the host computer
- Use a direct USB port (avoid hubs)

### Recovery

1. Power cycle: unplug USB, wait 10 seconds, reconnect
2. Re-enter ISP mode (some devices: hold button during power-on)
3. Use Serial Reset Tool to re-flash bootloader
4. Contact support if bricked

---

## Performance Problems

### High CPU Usage

1. **Enable hardware acceleration** — Preferences > Video > Hardware Acceleration (VAAPI, V4L2-M2M)
2. **Lower resolution** — 720p uses significantly less CPU than 1080p
3. **Lower frame rate** — 15fps halves decode workload
4. **Switch backend** — FFmpeg with HW acceleration typically uses less CPU than GStreamer

### Frame Drops

Check the FPS counter in the status bar. If actual FPS is below target, the pipeline is bottlenecked. Enable frame dropping in the FFmpeg frame processor to prioritize smooth playback.

---

## Logging and Diagnostics

### Enable Logging

- **macOS:** Settings > Logging Setting > Log to file (`~/Documents/openterface.log`)
- **Qt:** Preferences > Log > set log level and file path

### Serial Console (Qt)

Open via **Device > Serial Port Debug** — shows real-time serial protocol messages with filters for Keyboard, Mouse, HID, Chip Info.

---

## Platform-Specific Issues

### Linux: Qt Platform Plugin

`This application failed to start because no Qt platform plugin could be initialized.`

```bash
export QT_QPA_PLATFORM=xcb
```

### Linux: Wayland Video Issues

```bash
QT_QPA_PLATFORM=xcb ./openterfaceQT
```

### Windows: CH340 Driver

If the driver fails to install: disable Driver Signature Enforcement temporarily, then install manually via Device Manager.

### Raspberry Pi: Video Stuttering

On Pi 3 or low-memory Pi 4:
1. Lower resolution to 720p
2. Use FFmpeg backend (not GStreamer)
3. Use 9600 baud for serial stability

---

## Factory Reset

1. Use the Serial Reset Tool from Settings (macOS) or Device menu (Qt)
2. This resets the HID chip to factory defaults
3. Reconnect the device after reset

## Connection Recovery

The applications handle automatic recovery for:
- Device disconnect/reconnect (hot-plug)
- Communication timeouts
- Chipset fallbacks (MS2109 → MS2109S → MS2130S)
- Serial port recovery

## Submitting Defect Reports

1. Enable log file logging
2. Reproduce the issue
3. Submit via [GitHub Issues](https://github.com/TechxArtisanStudio/Openterface_QT/issues) or email to info@techxartisan.com
