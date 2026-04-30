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

## Android-Specific Issues

### Device Not Detected

**Symptom:** Video preview shows a placeholder, not the target's screen.

1. **Check the USB OTG connection** — unplug and replug the cable
2. **Verify OTG support** — try connecting a USB flash drive to confirm your phone supports OTG
3. **Check the KVM device** — is it powered on? Are any indicator lights on?
4. **Try a different cable** — some OTG adapters are faulty
5. **Restart the app** — close it fully (swipe from recent apps) and reopen
6. **Check USB permission** — if a system dialog asked for USB access, make sure you tapped **Allow**

### No Video

**Symptom:** Device is detected but the screen is black or frozen.

1. **Check the HDMI cable** — is the target computer's HDMI firmly connected to the KVM HDMI input?
2. **Check the target's output** — is the target computer actually displaying something?
3. **Try a lower resolution** — open settings → **Video Format** → pick a lower resolution
4. **Check camera permission** — Android Settings → Apps → Openterface → Permissions → ensure Camera is allowed
5. **Restart the app**

### Mouse Not Responding

**Symptom:** Video works but tapping the screen does nothing on the target.

1. **Check USB connection for HID** — open settings → **Device** and confirm the device is active
2. **Try a different mouse mode** — switch from Absolute to Relative or vice versa
3. **Disconnect and reconnect** — use the red **Disconnect Device** button, then reconnect
4. **Check the target computer** — does it recognize a USB keyboard/mouse? Try unplugging and replugging the USB cable on the target side

### Keyboard Not Sending Keys

**Symptom:** Mouse works but typing does nothing.

1. **Make sure the keyboard is open** — tap the keyboard button
2. **Check the serial connection** — open settings → **Device** and confirm it's active
3. **Check the baudrate** — open settings → **Baudrate** and make sure it matches your device (115200 is the default)
4. **Check the keyboard layout** — make sure the correct layout (US, JP, DE) is selected

### App Crashes or Freezes

1. **Close and restart** the app
2. **Lower the video resolution and frame rate** — high settings can overwhelm devices with limited memory
3. **Check available storage** — low storage can cause instability
4. **Update the app** — check for a newer version on Google Play or GitHub Releases

### Screenshots or Recordings Not Saving

1. **Check Storage permission** — Android Settings → Apps → Openterface → Permissions → Storage
2. **Check available storage space** on your device
3. Recordings and screenshots are saved to your device's default media folder

### Collecting Logs (Android)

If standard troubleshooting doesn't help, collect logs to share with maintainers:

```bash
adb logcat | grep -i openterface > openterface.log
```

Include this file when opening a GitHub issue.

---

## iPadOS-Specific Issues

> **Note:** iPadOS is only supported on **KVM-Go**. If you're using Mini-KVM or uConsole KVM Extension, the iPadOS app will not work.

### Bluetooth Not Connecting

**Symptom:** BLE button doesn't turn green, or no devices appear in the scan list.

1. **Check Bluetooth is enabled** on your iPad — Settings > Bluetooth
2. **Ensure KVM-Go is powered on** — the dongle should be plugged into the target PC's USB port
3. **Bring the iPad closer** to the KVM-Go dongle — BLE range is typically up to 10 meters
4. **Check iPad Bluetooth permission** — Settings > Privacy & Security > Bluetooth > ensure Openterface is allowed
5. **Tap Refresh** in the BLE screen to restart the scan
6. **Check the Openterface app Bluetooth permission** — if denied on first launch, re-enable in Settings

### No Video Preview

**Symptom:** BLE is connected but the screen is black or shows a guide image.

1. **Check HDMI connection** — is the target PC's HDMI output firmly connected to the KVM-Go HDMI input?
2. **Check the target's output** — is the target computer actually displaying something?
3. **Try a lower resolution** — tap the Video button and select a lower resolution (720p or 480p)
4. **Check camera permission** — Settings > Privacy & Security > Camera > ensure Openterface is allowed
5. **Restart the app** — swipe up from recent apps and reopen

### Mouse/Touch Not Responding

**Symptom:** Video works but tapping the screen does nothing on the target.

1. **Check BLE connection** — the BLE button should be green with an RSSI value
2. **Try a different mouse mode** — toggle between Pan Mode and iPencil Mode
3. **Disconnect and reconnect** — open the BLE screen, tap Disconnect, then Connect again
4. **Check the target computer** — does it recognize the KVM-Go as a USB keyboard/mouse?

### Keyboard Not Sending Keys

**Symptom:** Mouse works but typing does nothing.

1. **Make sure the floating keyboard is open** — tap the Keyboard button
2. **Check BLE connection** — input goes through Bluetooth, not USB
3. **Check keyboard mode** — try switching between Normal and Game mode
4. **External keyboard:** if using a physical iPad keyboard, check that iPadOS is routing key events to the app

### Audio Not Playing

**Symptom:** Video works but you can't hear the target PC through the iPad.

1. **Check the Audio button** — it should show a green speaker icon
2. **Check microphone permission** — Settings > Privacy & Security > Microphone > ensure Openterface is allowed
3. **Check iPad volume** — make sure the iPad isn't muted or at minimum volume
4. **Check target audio output** — is the target PC configured to send audio over HDMI?

### App Crashes or Freezes

1. **Close and restart** the app
2. **Lower the video resolution** — high resolution can strain older iPads
3. **Check available storage** — low storage can cause instability
4. **Update the app** — check the App Store for a newer version

### Screenshots or Recordings Not Saving

1. **Check Photo Library permission** — Settings > Privacy & Security > Photos > ensure Openterface is allowed
2. **Check available storage** on your iPad
3. **Browse via Files app** — recordings save to `Documents/Recordings/` even without Photo Library access

---

## Factory Reset

1. Use the Serial Reset Tool from Settings (macOS) or Device menu (Qt)
2. This resets the HID chip to factory defaults
3. Reconnect the device after reset

## Connection Recovery

The applications handle automatic recovery for:
- Device disconnect/reconnect (hot-plug for USB, BLE reconnection for iPadOS)
- Communication timeouts
- Chipset fallbacks (MS2109 → MS2109S → MS2130S)
- Serial port recovery
- iPadOS BLE auto-reconnect (up to 3 attempts with 2-second delay)

## Submitting Defect Reports

1. Enable log file logging
2. Reproduce the issue
3. Submit via [GitHub Issues](https://github.com/TechxArtisanStudio/Openterface_QT/issues) or email to info@techxartisan.com
