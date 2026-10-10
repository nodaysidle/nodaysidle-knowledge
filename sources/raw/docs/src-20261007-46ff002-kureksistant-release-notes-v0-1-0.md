# Kureksistant 0.1.0 — First Public Release

## Problem
Desktop AI assistants have become bloated 500MB+ Electron containers that hijack workstation memory, require manual window-switching to interact with, and lack direct keyboard and input hardware integration. When you need a quick answer or computer action, switching away from your editor and waiting for a browser-based UI breaks developer flow.

## What's Included
Kureksistant is a local-first, headless personal AI assistant daemon running natively on port `8790` with a ~55MB idle RAM footprint.

- **Hardware Summoning:** Wired directly to input events — middle-click on the mouse scroll wheel (`mouse:274`) or `Fn` key on macOS triggers instant listening without window switching.
- **Brain & Voice:** Direct API integration with `DeepSeek-Flash` for sub-second reasoning and tool dispatch, plus xAI Grok Cloud TTS (**Sol** voice) for conversational spoken feedback over PipeWire `mpv` (Linux) or `afplay` (macOS).
- **Native Workstation Tools:** 20 built-in actions including:
  - Wayland monitor perception (`grim` + Gemini Flash)
  - Parallel repository health scanner (`workstation_radar`)
  - Build and compile process watcher (`process_sentinel`)
  - Dictated conventional commits and PR copy to Wayland clipboard (`draft_to_clipboard`)
  - Full local file and application management
- **Muse Memory Architecture:** Three-tier memory plane (daily logs, core memory, and alignment synthesis) with TypeSafe Jev cognitive snap-judgment gating.

## Downloadable Assets & Verification
- `kureksistant-v0.1.0-linux-x86_64.tar.gz` (903 KB)
- `SHA256SUMS.txt`

### SHA-256 Checksums
```text
91c4cf1b682a4fe55f46e4fe9498ce8e11a5b07a7d4020c6ac07ef0d3e748911  kureksistant-v0.1.0-linux-x86_64.tar.gz
```

> **Code Signing / Notarization:** Unsigned / ad-hoc release. Binaries and scripts run locally with user workstation permissions. Always inspect scripts before executing.

---

## How to Install & Run (Linux / Arch / Hyprland)

```bash
# 1. Download release tarball and verify checksum
curl -LO https://github.com/nodaysidle/kureksistant/releases/download/v0.1.0/kureksistant-v0.1.0-linux-x86_64.tar.gz
sha256sum -c - <<< "91c4cf1b682a4fe55f46e4fe9498ce8e11a5b07a7d4020c6ac07ef0d3e748911  kureksistant-v0.1.0-linux-x86_64.tar.gz"

# 2. Extract archive
tar -xzf kureksistant-v0.1.0-linux-x86_64.tar.gz
cd kureksistant-0.1.0

# 3. Run automated installer
./install_linux.sh

# 4. Configure environment keys
cp .env.example .env
nano .env

# 5. Start assistant daemon
kurek start

# 6. Verify daemon status
kurek status
```

---

## Required Configuration (`.env`)

Kureksistant relies on cloud APIs for inference and voice synthesis (it is **not** a fully offline local model):

- `DEEPSEEK_API_KEY` (Required): Direct API key from `api.deepseek.com` for `deepseek-flash` reasoning.
- `XAI_API_KEY` (Required): xAI Grok Cloud API key from `api.x.ai` for Sol TTS voice generation.
- `GEMINI_API_KEY` (Optional): Google Gemini key for Wayland monitor vision (`screen_vision`).
- `DEEPGRAM_API_KEY` (Optional): Deepgram Nova-2 STT for sub-second voice transcription. If omitted, falls back to local `faster-whisper` (base.en).
- `TYPESAFE_API_KEY` (Optional): TypeSafe Jev System One engine for cognitive snap-judgment gating.

System dependencies:
- Linux: `mpv` (PipeWire audio), `notify-send`, `grim` (Wayland screen capture), `wl-clipboard` (`wl-copy`).
- macOS: macOS 14+ with Xcode command line tools (`swiftc`, `afplay`).

---

## Known Limits

- **Arch Linux & Hyprland first:** The mouse shortcut bindings (`mouse:274`) and `grim` screen vision are tuned for Arch Linux on Hyprland. Other Wayland compositors (Sway, River) require manual hotkey mapping in your window manager config.
- **Cloud API dependency:** While local Whisper STT is available as an offline fallback, DeepSeek-Flash reasoning and Grok Sol TTS require active network access and API credits.
- **macOS status:** The headless daemon and Swift menu bar app (`KurekBar.swift`) are functional, but Wayland-specific tools (`grim`, `wl-clipboard`) fall back to macOS system equivalents (`screencapture`, `pbcopy`).
- **File safety gate:** File creation is unrestricted; file deletion strictly requires verbal or interactive user confirmation (*"Yes or No?"*).
