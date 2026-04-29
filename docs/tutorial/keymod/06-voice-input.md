---
title: "KeyMod Tutorial - Voice Input"
description: "Use voice-to-keyboard with KeyMod. Supports system speech recognition, on-device Whisper AI, and multiple languages."
keywords: "KeyMod voice input, speech to text, Whisper, voice typing, hands-free keyboard"
---

# 6. Voice Input

Convert your speech into keystrokes sent to the target computer — hands-free typing and accessibility.

## How It Works

1. Tap the **microphone** button
2. Speak what you want to type
3. Your speech is converted to text
4. The text is sent as keystrokes to the target computer

## STT Engines

| Engine | How it works | Setup |
|---|---|---|
| **System Recognizer** (Android) / **Apple Speech** (iOS) | Uses built-in speech recognition | Requires Google Voice Typing (Android) or network connectivity (iOS) |
| **Whisper** (both) | On-device or cloud AI transcription | Android: set API key in Settings. iOS: download on-device model files |

## Supported Languages (iOS)

15 languages including English (US/UK), Chinese (Simplified/Traditional), Cantonese, Japanese, Korean, French, German, Spanish, Italian, Portuguese, Russian, Arabic, and Hindi.

## Silence Detection & Auto-Pause

Both engines feature automatic silence detection that pauses recording when you stop speaking (2.0 second silence timeout by default). Toggle Auto-Pause on/off in the Voice Input view.

### Troubleshooting Silence Detection

| Symptom | Solution |
|---|---|
| **Recording continues when not speaking** | Check the Auto-Pause on Silence toggle. Reduce background noise. Speak clearly and close to the microphone. |
| **Recording stops immediately** | Speak more loudly or reduce the silence detection timeout. |

## Mini Toolbar (Android)

| Button | What it does |
|---|---|
| **Copy** | Copy transcribed text to clipboard |
| **Auto Send** | Automatically send text after transcription |
| **Auto Line Return** | Append an Enter keystroke after sending |
| **AI Refine** | Send transcribed text to AI for improvement |

## Whisper Model Management (iOS)

On-device Whisper models trade accuracy for file size:

| Model | Size | Accuracy | Speed |
|---|---|---|---|
| **tiny** | ~75 MB | Basic | Fastest |
| **base** | ~142 MB | Good | Fast |
| **small** | ~466 MB | Better | Moderate |
| **medium** | ~1.5 GB | Best | Slowest |

Start with `base` — it's a good balance of accuracy and speed.

If model downloads fail or stall, check network connectivity and available storage. Try a smaller model first (tiny or base).

## Permissions (iOS)

Voice Input requires **Microphone** and **Speech Recognition** permissions. If denied, enable them in Settings → Privacy & Security.

## Voice Text Not Sending (Android)

Check the connection status. The "Send" button is disabled when not connected.

## Next Steps

- **[← Macros](05-macros.md)** — Automated key sequences
- **[AI Integration →](07-ai.md)** — AI-assisted text refinement and command assistant
