---
title: "KeyMod Tutorial - Macros"
description: "Record and replay automated key sequences with KeyMod macros, including modifiers, delays, and scheduling."
keywords: "KeyMod macros, automated keystrokes, macro scheduler, macro tokens, key sequences"
---

# 5. Macros

Record and replay automated key sequences with a single tap.

## What is a Macro?

A macro is a **recorded sequence of keystrokes** that you can replay. For example:
- Type your email signature with one tap
- Send `Ctrl+Shift+Esc` followed by `Alt+D` in sequence
- Automate a multi-step command sequence with delays between steps

## Macro Token Syntax

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
| `<DELAY1S>`, `<DELAY2S>`, `<DELAY5S>`, `<DELAY10S>` | Pauses |

**Example:**
```
<CTRL><ALT>t</ALT></CTRL><DELAY1S>ls -la<ENTER>
```
This opens a terminal (Ctrl+Alt+T), waits 1 second, then types `ls -la` and presses Enter.

## Creating a Macro

1. Go to **Macros** mode
2. Tap **"+"** to create a new macro
3. Enter a **macro name/label**
4. Build the macro command sequence using the text field and quick-insert token chips
5. Adjust the **Send Char Interval** (delay between keystrokes in milliseconds)
6. Tap **"Save"**

## Next Steps

- **[← Shortcut Hub](04-shortcuts.md)** — Profile-based keyboard shortcuts
- **[Voice Input →](06-voice-input.md)** — Voice-to-keyboard transcription
