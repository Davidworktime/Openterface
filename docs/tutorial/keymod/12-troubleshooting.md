---
title: "KeyMod Tutorial - Troubleshooting"
description: "Fix common KeyMod issues: connection problems, keys not registering, Bluetooth pairing failures, voice input errors, and more."
keywords: "KeyMod troubleshooting, KeyMod not connecting, KeyMod Bluetooth issues, KeyMod keys not working"
---

# 12. Troubleshooting

Common problems and solutions for the KeyMod app on Android and iOS.

## Connection Issues

### Not Connected

| Symptom | Solution |
|---|---|
| **"Not Connected"** indicator | Check cable connection; try re-plugging. For BLE, toggle Bluetooth off/on and re-pair. |
| **USB permission denied** (Android) | Go to Android Settings → Apps → KeyMod → Permissions → enable USB. Re-plug the cable. |
| **Bluetooth won't pair** | Toggle Bluetooth off/on. Forget the device in Bluetooth settings and re-pair. Make sure the KeyMod device is in pairing mode. |
| **Device not showing in scan** (iOS) | Check that Bluetooth is enabled. Verify the Openterface device is powered on and in BLE advertising mode. Ensure Bluetooth permission is granted to KeyMod in Settings → Privacy & Security → Bluetooth. |
| **Connection drops frequently** (iOS) | Check the RSSI value below the BLE button. Below -75 dBm indicates weak signal — move closer. Remove physical obstructions. Check for BLE interference. |
| **FFF2 characteristic not found** (iOS) | This indicates a firmware compatibility issue. Update the Openterface firmware to the latest version. |

### Connection State Indicators

| Indicator | Android | iOS |
|---|---|---|
| **Connected** | Green icon | Green icon with RSSI displayed |
| **Connecting** | Amber icon | Blue icon (scanning) |
| **Disconnected** | Gray icon | Gray/Disabled (permission denied or Bluetooth off) |
| **Signal bars** | BLE signal strength or USB active | RSSI in dBm below BLE button |

### Auto-Connect

- **Android:** Enable "Auto-connect on startup" in the connection dialog. KeyMod remembers your last connection type (USB or BLE) and last paired BLE device.
- **iOS:** The app automatically begins scanning for nearby Openterface devices after a brief delay on launch.

### USB Attach/Detach Detection (Android)

KeyMod monitors Android's USB attach/detach broadcast events. If you unplug the USB cable, the connection status updates immediately. Re-plugging triggers a reconnection attempt if auto-connect is enabled.

---

## Keyboard Issues

### Keys Not Registering

| Symptom | Solution |
|---|---|
| **Keys not sending** | Verify the connection shows "Connected" (green). Try switching modes and back. Check that the target computer recognizes the KeyMod device as a keyboard. |
| **Keys not registering** (iOS) | Verify BLE is connected (green icon). Check the target computer's keyboard is recognizing input. Increase **BLE Key Delay** in Settings → General (try 20ms or higher). |
| **Macro doesn't execute** | Verify you're connected. Check that the macro data contains valid tokens (no typos in token names). |
| **Wrong characters appearing** (iOS) | Check the **Target OS** setting — mismatched OS can cause key mapping issues. Verify the target computer's keyboard layout (QWERTY vs AZERTY). Check for stuck modifier keys in the sidebar. |

### Unicode Characters Not Working

Non-ASCII characters (Chinese, Japanese, emoji) require OS-specific input methods:

| OS | Method |
|---|---|
| **Windows** | Alt+NumPad hexadecimal Unicode input |
| **Linux** | Ctrl+Shift+U followed by hex code |
| **macOS** | Option+hex input |

If Unicode characters appear incorrectly, verify the **Target OS** is set correctly.

---

## TouchPad Issues

| Symptom | Solution |
|---|---|
| **Touchpad not responding** (Android) | Check that Haptic Feedback is enabled in Settings. Try the TouchPad Help overlay (?) to verify gesture support. |
| **Scroll not working** | Check touchpad scroll sensitivity in Settings → General. |

---

## Gamepad Issues (iOS)

### Analog Stick Not Responding

| Symptom | Solution |
|---|---|
| **Stick not producing action** | Check the key mapping in Edit Mode → Key Mapping. Verify the stick isn't stuck in the dead zone (center area, 0.15 threshold). Check hysteresis thresholds — the stick needs to move past 0.6 activation to trigger. |
| **Buttons sending wrong keys** | Open Edit Mode → Key Mapping and check the button's key assignment. Tap the button to open the configuration popup and correct the mapping. Reset positions to defaults using the reset button. |

---

## Voice Input Issues

### Speech Recognizer Unavailable (Android)

Install Google Voice Typing from Play Store. On Android 11+, KeyMod needs the queries permission (included in the APK).

### Whisper Model Not Downloading (iOS)

| Symptom | Solution |
|---|---|
| **Download fails or stalls** | Check network connectivity — model files are large and require a stable connection. Check available storage — the `base` model is ~142 MB, `small` is ~466 MB. Try a smaller model first (tiny or base). |

### Silence Detection Not Working

| Symptom | Solution |
|---|---|
| **Recording continues when not speaking** | Check the Auto-Pause on Silence toggle. Reduce background noise. Speak clearly and close to the microphone. |
| **Recording stops immediately** | Speak more loudly or reduce the silence detection timeout. |

### Voice Text Not Sending (Android)

Check the connection status. The "Send" button is disabled when not connected.

### Permissions (iOS)

Voice Input requires **Microphone** and **Speech Recognition** permissions. If denied, enable them in Settings → Privacy & Security.

---

## AI Issues

### API Key Not Working (iOS)

| Symptom | Solution |
|---|---|
| **"API key not configured"** | Verify the API key is correct — check for extra spaces or typos. Check the API Base URL — must include the full path (e.g., `https://api.openai.com/v1`). Verify the model name exists on the provider. For local providers (Ollama), ensure the API Key Optional flag is set. |

### Text Refinement Slow

Check your network connection. Try a faster model — smaller models (gpt-3.5-turbo, llama3-8b) respond faster. Use a local provider (Ollama) to eliminate network latency. Check the AI Request History for error messages.

---

## App Crashed or Frozen (iOS)

1. Force quit the app (swipe up from the app switcher) and relaunch
2. Restart your iOS device
3. Check iOS storage — low storage can cause app instability

---

## Settings Not Persisting (iOS)

Settings are stored in UserDefaults and should persist across app launches. If settings reset unexpectedly, check for iOS iCloud sync conflicts. Use Reset to Defaults and reconfigure if needed.

---

## Logs and Debugging (iOS)

KeyMod has a built-in LogManager that categorizes logs:

| Category | What It Logs |
|---|---|
| **BLE** | Device discovery, connection, disconnection, data transmission, RSSI |
| **Keyboard** | Key presses, releases, modifier state, mode changes |
| **VoiceInput** | Recording start/stop, transcription results, silence detection |
| **Clipboard** | Clipboard changes detected, content sent/dismissed |
| **Macro** | Macro execution, token processing, timing |

---

## Need More Help?

If you're still experiencing issues:

- **Bug reports:** [GitHub Issues (Android)](https://github.com/TechxArtisanStudio/Openterface_KeyMod_Android/issues) / [GitHub Issues (iOS)](https://github.com/TechxArtisanStudio/Openterface_KeyMod_iOS/issues)
- **Community:** [TechxArtisan Discord](https://discord.gg/techxartisan)
- **Openterface documentation:** [GitHub Repository](https://github.com/TechxArtusStudio/Openterface)
