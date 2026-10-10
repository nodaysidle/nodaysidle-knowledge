---
type: wiki-note
note_kind: concept
topic_slug: nodaysidle-voice-anywhere
status: active
created: 2026-10-10
updated: 2026-10-10
tags:
  - wiki
  - android
  - speech-to-text
  - accessibility
  - superwhisper
---

# Voice Anywhere (Android) — Architecture & Superwhisper Interaction

## Overview

**Voice Anywhere** (`com.nodaysidle.voiceanywhere.debug`) is an Android accessibility service and companion application providing seamless, universal dictation across any application on Android (WhatsApp, Notes, Browsers, Telegram, etc.) with local & cloud speech-to-text (STT) and LLM post-processing polish.

The app is modeled after **Superwhisper Pro**'s tactile interaction model:
- Hold-to-Talk (press and hold down anywhere on the badge to record, release to transcribe & paste)
- Seamless overlay that automatically appears when typing in any editable field and hides when returning to the home screen or non-editable views
- Floating black rounded triangle badge with bright white outline and matching inner Delta (`▲`) glyph
- Double-tap gesture for instant access to the transcription history drawer
- Local / Cloud STT engine switching: Deepgram Nova-2/3, OpenRouter Whisper, xAI Grok STT, and on-device FUTO engine

---

## 2026-10-10 Architectural Changes & Fixes

### 1. Tactile Superwhisper Triangle Badge
- **Idle Appearance**: Designed a custom Canvas-rendered `SuperwhisperDeltaIcon`:
  - Outer geometry: Solid black (`#0A0B10`) rounded triangle badge with a bright white (`#FFFFFF` / `#F1F5F9`) stroke outline.
  - Inner geometry: Crisp, bright white Delta (`▲`) triangle glyph drawn with rounded stroke corners.
  - Container padding in `IDLE` state is set to zero with a transparent background, ensuring no circular or pill container borders remain visible.
- **Dynamic Recording & Feedback Expansion**:
  - Upon holding the triangle, the container smoothly transitions into an active recording capsule displaying a 4-bar live audio waveform (`MiniWaveformView`).
  - Outline pulses with a subtle glow animation during recording and processing.
  - Success (`✓ Inserted`, green), copy (`✓ Copied`, blue), and error states smoothly display descriptive feedback before fading back to idle.

### 2. Auto-Show / Auto-Hide Lifecycle (Typing Detection)
- **Problem**: The overlay previously lingered for 2.5 seconds on non-editable screens or failed to hide on launcher home screens.
- **Fixes Applied**:
  - `accessibility_service_config.xml`: Added `typeWindowsChanged` and `typeViewTextChanged` event types.
  - `VoiceAccessibilityService.kt`:
    - Tuned `bubbleHideRunnable` delay to `200ms` when focus is lost.
    - Enhanced `hasEditableFocus` to perform multi-stage verification: checks current event source, input focus via `findFocus(AccessibilityNodeInfo.FOCUS_INPUT)`, and `rootInActiveWindow.findFocus()`.
    - Automatically hides when the home launcher is active or when leaving input fields.
    - Immediately pops up whenever the user taps into any text input across any app.

### 3. Audio Recording & STT Error Resilience
- **MediaRecorder Stop Error `-1007` Resolution**:
  - Android's native `MediaRecorder` raises error `-1007` if `stop()` is called before audio frame encoding completes (< 350ms duration).
  - Enforced a minimum buffer safety threshold in `DictationAudioRecorder.kt` (`elapsed < 450L`) with frame finalization, preventing encoder crashes on fast taps.
- **Short Audio & Quota Rejection Protection**:
  - Sub-300ms touches or files < 300 bytes are discarded cleanly without triggering false "Error" flashes.
  - Granular error reporting on real API/network failures: displays descriptive labels (`No speech`, `STT Error`, `No API Key`) on the floating status label.

---

## Code References

- **Overlay UI & Canvas Rendering**: `app/src/main/java/com/nodaysidle/voiceanywhere/service/FloatingMicOverlay.kt`
- **Accessibility Engine & State Management**: `app/src/main/java/com/nodaysidle/voiceanywhere/service/VoiceAccessibilityService.kt`
- **Hardware Audio Capture**: `app/src/main/java/com/nodaysidle/voiceanywhere/stt/DictationAudioRecorder.kt`
- **Cloud STT Transcriber**: `app/src/main/java/com/nodaysidle/voiceanywhere/stt/DeepgramSttClient.kt`
- **Accessibility XML Configuration**: `app/src/main/res/xml/accessibility_service_config.xml`
- **Local Workspace**: `/home/arch/Projects/_github-migrations/nodaysidle-voice-anywhere-v2`
