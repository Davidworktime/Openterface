# KeyMod Tutorial 04 — Troubleshooting

Common problems and solutions for Openterface KeyMod.

---

## Device Not Detected

### Symptoms
- Keyboard and mouse indicators show orange or gray
- Serial port shows "N/A"
- USB switch toggle has no effect

### Diagnosis

**Linux:**
```bash
lsusb | grep "1a86"
dmesg | tail -20
ls /dev/ttyUSB*   # serial chip
```

Expected: `1a86:7523` or `1a86:fe0c` (CH9329 or CH32V208 serial chip).

**macOS:** Apple Menu > About This Mac > System Report > Hardware > USB — look for KeyMod/serial device.

**Windows:** Device Manager > "Ports (COM & LPT)" — should show "USB-SERIAL CH340 (COMx)".

### Solutions

| Problem | Fix |
|---------|-----|
| Device not in lsusb/System Report | Try different USB cable/port |
| Permission denied | Add user to `dialout` group (Linux) |
| Detected then disappears | `brltty` claiming the serial port — see below |

---

## BrlTTY Conflict (Linux)

**The most common cause of KeyMod failure on Linux.**

The `brltty` (Braille terminal) service claims USB serial devices including the CH9329/CH32V208 chip.

### Symptoms
- Device is detected in `lsusb`
- Serial port appears briefly then disappears
- `/dev/ttyUSB*` returns "Device or resource busy"

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

## Keyboard/Mouse Not Working on Target

### Symptoms
- Typing on the keyboard has no effect on the target
- Mouse movements don't register on the target

### Steps

1. **Check USB switch** — make sure KeyMod is switched to **Target**, not Host
2. **Verify serial port** — should show a port name, not "N/A"
3. **Try switching baud rate** — 9600 or 115200
4. **Check target device** — is it powered on and accepting input?
5. **Try the other USB cable** — ensure both host and target cables are connected

### Mouse-Specific Issues

- **Relative mode on macOS:** Requires Accessibility permission. Check **System Settings > Privacy & Security > Accessibility**
- **Mouse lag:** Try a higher performance preset or increase the baudrate
- **Serial port conflicts (Linux):** Close other apps using the port: `sudo lsof /dev/ttyUSB0`

---

## Keys Mapped Incorrectly

### Wrong Keyboard Layout

Ensure the correct layout is selected in **Settings > Keyboard Layout**:

| Symptom | Likely Cause |
|---------|-------------|
| `@` and `"` swapped | UK vs US layout mismatch |
| `Y` and `Z` swapped | QWERTY vs QWERTZ mismatch |
| `A` and `Q` swapped | QWERTY vs AZERTY mismatch |
| `¥` key not working | Japanese layout not selected |

### Wrong Target OS

Ensure the target OS is set correctly in the toolbar or settings. Key conventions (Cmd vs Win vs Super) differ across OSes.

---

## USB Serial Driver Issues

### macOS

```bash
kextstat | grep com.apple.driver.usb.cdc
```

If needed, install WCH CH34x driver from [WCH CH34xDriver GitHub](https://github.com/WCHSoftGroup/ch34xser_macos).

### Windows

If the serial chip doesn't appear in Device Manager, install the CH340/CH341 driver. The installer bundles it; for portable builds, download separately.

### Linux

The CH340 driver (`ch341` module) is built into the kernel:
```bash
lsmod | grep ch341
dmesg | grep ch341
```

---

## Firmware Update Fails

### Recovery

1. Keep the device powered
2. Close and reopen the Firmware Update Tool, retry
3. Use the Serial Reset Tool if unresponsive
4. Contact support if bricked

---

## Logging and Diagnostics

### Enable Logging

- **macOS:** Settings > Logging Setting > Log to file (`~/Documents/openterface.log`)
- **Qt:** Preferences > Log > set log level and file path

### Serial Console (Qt)

Open via **Device > Serial Port Debug** — shows real-time serial protocol messages with filters for Keyboard, Mouse, HID events.

---

## Platform-Specific Issues

### Linux: Qt Platform Plugin

`This application failed to start because no Qt platform plugin could be initialized.`

```bash
export QT_QPA_PLATFORM=xcb
```

### Windows: CH340 Driver

If the driver fails to install: disable Driver Signature Enforcement temporarily, install manually via Device Manager.

---

## Factory Reset

1. Use the Serial Reset Tool from Settings (macOS) or Device menu (Qt)
2. Reconnect the device after reset

## Connection Recovery

The applications handle automatic recovery for:
- Device disconnect/reconnect (hot-plug)
- Communication timeouts
- Serial port recovery

## Submitting Defect Reports

1. Enable log file logging
2. Reproduce the issue
3. Submit via [GitHub Issues](https://github.com/TechxArtisanStudio/Openterface_QT/issues) or email to info@techxartisan.com
