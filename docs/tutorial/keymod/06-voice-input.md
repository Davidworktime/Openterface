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
| **System Recognizer** | Uses Android's built-in speech recognition | Requires Google Voice Typing |
| **Whisper** | On-device or cloud AI transcription | Set API key in Settings > Voice Input |

<div align="center">
  <img src="https://assets2.openterface.com/images/keymod/andorid/demo-voice-input.webp" alt="Voice input screen" width="300" />
  <p><em>Voice input — transcript area, targets, history, and mic. Configure API key in Settings > Voice Input.</em></p>
</div>

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

## Voice Text Not Sending

Check the connection status. The "Send" button is disabled when not connected.

## Next Steps

- **[← Macros](05-macros.md)** — Automated key sequences
- **[AI Integration →](07-ai.md)** — AI-assisted text refinement and command assistant
