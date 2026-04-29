---
title: "KeyMod Tutorial - Advanced Features"
description: "Explore KeyMod's advanced modes: gamepad, numpad, shortcuts, macros, voice input, presentation remote, settings, and AI integration."
keywords: "KeyMod gamepad, KeyMod macros, KeyMod shortcuts, voice input, presentation remote, KeyMod AI"
---

# 3. Advanced Features

KeyMod offers multiple input modes beyond keyboard and mouse, plus powerful settings and AI features.

## Gamepad — Virtual Game Controller

**Best for:** Gaming, retro game emulation, simple game testing.

### The Layout

```
+-----------------------------------+
| [L1]              [R1]           |
| [L2]              [R2]           |
|                                   |
|  [D-pad]          [A][B]         |
|  ▲                [X][Y]         |
| ◀ ▶                             |
|  ▼                              |
|             [Select] [Start]     |
|      [Left Stick]  [Right Stick] |
+-----------------------------------+
```

### Controls

| Control | How |
|---|---|
| D-pad | Tap the directional arrows |
| Action buttons (A, B, X, Y) | Tap them |
| Shoulder buttons | Tap L1, L2, R1, R2 at the top |
| Analog sticks | Touch and drag the stick circles |
| Start / Select | Tap the buttons |

### Customizing (iOS)

iOS supports three built-in controller layouts selectable from the top bar:

- **Xbox** — Standard Xbox-style with dual sticks, D-pad, A/B/X/Y, shoulder/trigger buttons
- **PlayStation** — PlayStation-style with Cross/Circle/Square/Triangle action buttons
- **NES** — Classic Nintendo Entertainment System (D-pad, A/B, Select/Start, no sticks)

### Customizing (Android)

- **Long-press any button or stick** to reconfigure it — assign any HID key to each component
- **Analog vs Key mode** — sticks can be configured as analog input or as key-mapped D-pad input
- **WASD mapping** — assign WASD keys to the left stick for PC gaming
- **Button/stick size scaling** — adjust sizes for your preferred touch area
- **Background image** — customize the gamepad background
- **Haptic feedback** — vibration on button press

### Analog Sticks (iOS)

- **Left stick → Keyboard keys:** Maps to arrow keys with diagonal support. Configurable to WASD in Edit Mode.
- **Right stick → Mouse movement:** Dynamic sensitivity (2.0–8.0), dead zone to prevent drift.
- **Hysteresis:** Activation (0.6) and deactivation (0.4) thresholds prevent key chatter at the boundary.

> **Note:** Gamepad HID protocol is under active development. Basic button support works; analog stick precision may vary.

---

## Numpad (iOS)

A full numeric keypad for data entry. Each key sends the corresponding HID numpad key code.

| Key | HID Usage Code |
|-----|---------------|
| 0-9 | 0x62, 0x59-0x61 |
| +, -, *, / | 0x57, 0x56, 0x55, 0x54 |
| Enter | 0x58 |
| . / = | 0x63 / 0x67 |
| NumLock | 0x53 |

Some shortcut profiles (Blender, Fusion 360, KiCad) include **custom numpad grids** tailored to their specific applications.

---

## Shortcut Hub — Profile-Based Shortcuts

**Best for:** One-tap access to common keyboard shortcuts, organized by application.

### Built-in Profiles

| Profile | What it covers |
|---|---|
| **Default** | Common shortcuts (Copy, Paste, Undo, Save, etc.) — cannot be deleted |
| **Blender 3D** | Transform, selection, view, mesh, mode, and shading shortcuts |
| **KiCAD** | PCB design: layers, drawing, components, properties |
| **Nomad Sculpt** | Sculpting tools, brush, transform, view, masking |
| **Fusion 360** | CAD: navigation, sketch, modeling, construction, assembly |
| **Photoshop** | Tools, edit, view shortcuts |
| **VS Code** | Navigation, editing, code, view shortcuts |

### Using Shortcuts

1. Open the **Shortcut Hub** (or "Shortcuts" mode from the sidebar on Android)
2. Tap any profile to open it
3. Inside a profile, browse **category tabs** and tap any shortcut card to execute it
4. The shortcut labels automatically adapt to the **target OS** (Ctrl+Z on Windows/Linux, Cmd+Z on macOS)

### Creating and Managing Profiles (Android)

| Action | How |
|---|---|
| Create a profile | Tap **"Create Profile"**, enter a name |
| Edit a shortcut | Long-press the shortcut → "Edit" |
| Delete a shortcut | Long-press the shortcut → "Delete" |
| Add to favorites | Long-press → "Add to My" |
| Duplicate a profile | Long-press a profile → "Duplicate" |
| Export a profile | Long-press → "Export" — saves a JSON file |
| Import a profile | Tap **"Import"** — paste JSON or browse for a file |

### Custom Profiles (iOS)

Import JSON files conforming to the profile format. The JSON includes profile name, icon, theme color, categories, and shortcuts. Custom profiles are stored in the app's `Documents/ShortcutProfiles/` directory.

### "My Shortcuts"

Each profile has a **My Shortcuts** section for personal shortcuts specific to your workflow.

---

## Macros — Automated Key Sequences

**Best for:** Power users who repeat the same key combinations, content creators who need to trigger complex actions quickly.

### What is a Macro?

A macro is a **recorded sequence of keystrokes** that you can replay with a single tap. For example:
- Type your email signature with one tap
- Send `Ctrl+Shift+Esc` followed by `Alt+D` in sequence
- Automate a multi-step command sequence with delays between steps

### Macro Token Syntax

| Token | Meaning |
|---|---|
| `<CTRL>` ... `</CTRL>` | Hold/release Control |
| `<SHIFT>` ... `</SHIFT>` | Hold/release Shift |
| `<ALT>` ... `</ALT>` | Hold/release Alt/Option |
| `<CMD>` ... `</CMD>` | Hold/release Command/Win/Super |
| `<ESC>`, `<BACK>`, `<ENTER>`, `<SPACE>` | Special keys |
| `<LEFT>`, `<RIGHT>`, `<UP>`, `<DOWN>` | Arrow keys |
| `<HOME>`, `<END>`, `<TAB>`, `<DEL>` | Navigation keys |
| `<F1>` through `<F12>` | Function keys |
| `<DELAY1S>`, `<DELAY2S>`, `<DELAY5S>`, `<DELAY10S>` | Pauses (iOS also supports `<DELAY500MS>`) |

**Example:**
```
<CTRL><ALT>t</ALT></CTRL><DELAY1S>ls -la<ENTER>
```
This opens a terminal (Ctrl+Alt+T), waits 1 second, then types `ls -la` and presses Enter.

### Creating a Macro

1. Go to **Macros** mode
2. Tap **"+"** to create a new macro
3. Enter a **macro name/label**
4. Build the macro command sequence using the text field and quick-insert token chips
5. Adjust the **Send Char Interval** (delay between keystrokes in milliseconds)
6. Tap **"Save"**

### Scheduling & Repeating (iOS)

Macros can be scheduled to run at a specific date/time with repeat count and interval. The app must be running for scheduled macros to fire.

### Sub-Macro References (iOS)

Invoke other macros by name using `<Macro>label</Macro>`. Macros can nest up to 10 levels deep.

---

## Voice Input — Voice-to-Keyboard

**Best for:** Hands-free typing, accessibility, quick text input.

### How It Works

1. Tap the **microphone** button
2. Speak what you want to type
3. Your speech is converted to text
4. The text is sent as keystrokes to the target computer

### STT Engines

| Engine | How it works | Setup |
|---|---|---|
| **System Recognizer** (Android) / **Apple Speech** (iOS) | Uses built-in speech recognition | Requires Google Voice Typing (Android) or network connectivity (iOS) |
| **Whisper** (both) | On-device or cloud AI transcription | Android: set API key in Settings. iOS: download on-device model files |

### Supported Languages (iOS)

15 languages including English (US/UK), Chinese (Simplified/Traditional), Cantonese, Japanese, Korean, French, German, Spanish, Italian, Portuguese, Russian, Arabic, and Hindi.

### Silence Detection & Auto-Pause

Both engines feature automatic silence detection that pauses recording when you stop speaking (2.0 second silence timeout by default). Toggle Auto-Pause on/off in the Voice Input view.

### Mini Toolbar (Android)

| Button | What it does |
|---|---|
| **Copy** | Copy transcribed text to clipboard |
| **Auto Send** | Automatically send text after transcription |
| **Auto Line Return** | Append an Enter keystroke after sending |
| **AI Refine** | Send transcribed text to AI for improvement |

### Whisper Model Management (iOS)

On-device Whisper models trade accuracy for file size:

| Model | Size | Accuracy | Speed |
|---|---|---|---|
| **tiny** | ~75 MB | Basic | Fastest |
| **base** | ~142 MB | Good | Fast |
| **small** | ~466 MB | Better | Moderate |
| **medium** | ~1.5 GB | Best | Slowest |

Start with `base` — it's a good balance of accuracy and speed.

---

## Presentation — Slide Remote Control (Android)

**Best for:** Speakers, teachers, anyone giving a slideshow presentation.

### Controls

| Button | Does |
|---|---|
| **Next** | Advances to next slide (Right Arrow). Long-press = go to last slide |
| **Previous** | Goes back one slide (Left Arrow). Long-press = go to first slide |
| **Play / Stop** | Starts/stops the presentation |
| **B (Blank Screen)** | Toggles black screen |
| **Pointer** | Opens a pop-out touchpad for mouse control |
| **App Switcher** | Opens the OS app switcher (Cmd+Tab / Alt+Tab) |

### Presentation Tool Picker

A carousel lets you select your presentation software (Keynote, PowerPoint, Google Slides, Word, Adobe Reader). Each tool has unique key combinations for play/stop.

### Slide Timer

The timer card supports countdown and countup modes, with a progress fill bar, vibration alert at target time, and persistent state across app lifecycle.

### Gestures

- **Swipe left** → Next slide
- **Swipe right** → Previous slide
- **Tap** → Next slide

---

## Settings

### General Settings

| Setting | Android | iOS |
|---|---|---|
| **Auto-connect** | Reconnect to last device on startup | — |
| **Keep screen on** | Prevent screen sleeping (immersive mode) | — |
| **Haptic feedback** | Vibration on button presses | Automatic (Taptic Engine) |
| **Orientation lock** | Lock screen orientation | Toggle button in top bar |
| **Language** | English, 中文, Español, Français | System language |
| **Theme** | 8 color families, Dark/Light, Follow system | — |
| **BLE Key Delay** | — | 10ms default, adjustable (affects all text input) |
| **Clipboard monitoring** | — | Toggle clipboard detection on/off |
| **Touchpad sensitivity** | Scroll sensitivity slider | Mouse movement sensitivity |

### Target OS

Available on both platforms. Affects shortcut labels, Unicode input methods, and AI behavior. See [Keyboard & Mouse](02-keyboard-mouse.md#target-os).

---

## AI Integration

AI features are **disabled by default**. Enable them in Settings to access:

- **Text Refinement** — Correct transcription errors and improve text quality
- **Command Assistant** — Convert natural language speech into keyboard commands

### AI Providers (iOS)

KeyMod supports multiple AI providers simultaneously:

| Field | Description |
|---|---|
| **Name** | Display name (e.g., "OpenAI", "My Local Server") |
| **API Base URL** | The API endpoint (e.g., `https://api.openai.com/v1`) |
| **Model Name** | The model to use (e.g., `gpt-4o`) |
| **API Key** | Stored securely in the iOS Keychain |

### AI Providers (Android)

| Provider | Options |
|---|---|
| **AI provider** | OpenAI, Anthropic, Google Gemini, Mistral AI, Groq, Alibaba (Qwen), DeepSeek, or Custom |
| **API endpoint** | Set the URL for the AI service |
| **Model** | Choose the AI model |
| **AI role** | "Command Assistant" (voice → keyboard actions) or "Text Refinement" (voice → improved text) |

### System Prompt Roles

- **Text Refinement:** Corrects speech-to-text errors, improves grammar and clarity
- **Command Assistant:** Converts natural language into keyboard commands. OS-specific prompts for Windows, macOS, and Linux.
- **Custom:** User-defined system prompt for specialized behavior

### Macro Context in AI

When AI is enabled, your defined macros are automatically included in the system prompt, allowing the AI to suggest or invoke them by name.

## Next Steps

- **[Troubleshooting →](04-troubleshooting.md)** — Common problems and solutions
