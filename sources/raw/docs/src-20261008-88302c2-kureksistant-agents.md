# AGENTS.md — Developer & AI Agent Guide for Kurek (Kureksistant)

> **Kurek** is an ultra-fast headless personal AI assistant for **Arch Linux / Omarchy Quattro (Hyprland)** and **macOS** (~333MB RAM with default faster-whisper STT; lower without Whisper). Features instant Middle Click mouse summon, native desktop launcher, DeepSeek-Flash reasoning, xAI Grok speech (**Sol** voice), Hermes bidirectional memory continuity, and 24 tool modules in `actions/`. Release: v0.1.0.

---

## 1. System Architecture

```
  ┌──────────────────────────────────────────────┐       ┌──────────────────────────────────────────────┐
  │     Arch Linux / Omarchy Quattro             │       │       macOS Menu Bar Item (Kurek.app)        │
  │  • Middle Click (mouse:274) / Super+Middle   │       │   Swift 6 / AppKit  •  Fn Key Global Monitor │
  │  • Super+Space Launcher (kurek.desktop)      │       │      10 Hz Reactive Polling / State Indicator│
  │  • CLI: kurek [toggle|prompt|status|stop]    │       │                                              │
  └──────────────────────┬───────────────────────┘       └──────────────────────┬───────────────────────┘
                         │                                                      │
                         └───────────────────────┬──────────────────────────────┘
                                                 │ HTTP (127.0.0.1:8790)
                                                 ▼
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                        KUREK PYTHON DAEMON (kurek_daemon.py)                           │
│                                                                                        │
│  ┌──────────────────────┐   ┌───────────────────────┐   ┌───────────────────────────┐  │
│  │   Audio Input (STT)  │   │      Brain (LLM)      │   │     Speech Output (TTS)   │  │
│  │  • Deepgram Nova-2   │   │  • DeepSeek-Flash     │   │  • xAI Grok TTS (Sol/sal) │  │
│  │  • faster-whisper    │   │    (api.deepseek.com) │   │    (api.x.ai/v1/tts)      │  │
│  │    (base.en local)   │   │  • Reasoning tokens   │   │  • Linux mpv (PipeWire)   │  │
│  │  • DC offset removal │   │  • 24 OpenAI Tools    │   │  • macOS afplay           │  │
│  │  • Peak normalization│   │  • Unrestricted Jarvis│   │  • In-place notifications │  │
│  └──────────────────────┘   └───────────┬───────────┘   └───────────────────────────┘  │
│                                         │                                              │
│                                         ▼                                              │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │                         24 Computer Control & Core Tools                         │  │
│  │  • open_app           • browser_control     • desktop_control   • reminder       │  │
│  │  • computer_control   • computer_settings   • manage_memory     • weather        │  │
│  │  • file_controller    • dev_agent           • web_search        • youtube_video  │  │
│  └──────────────────────────────────────┬───────────────────────────────────────────┘  │
│                                         │                                              │
│                                         ▼                                              │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │                             Persistent Memory System                             │  │
│  │  • Muse Memory: ~/memory/YYYY-MM-DD.md · ~/MEMORY.md · ~/ALIGNMENT_SYNTHESIS.md │  │
│  │  • Hermes Continuity Sync: HERMES_PROFILE / HERMES_MEMORIES_DIR / ~/.hermes/…  │  │
│  │    (reads full USER.md & MEMORY.md, syncs bidirectional remember calls)          │  │
│  │  • Conversation context: memory/kurek_history.json                              │  │
│  └──────────────────────────────────────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Key Components & File Locations

| Component | File Path | Description |
|-----------|-----------|-------------|
| **Python Daemon** | [`kurek_daemon.py`](kurek_daemon.py) | Headless background HTTP service on port `8790` (using `ThreadingHTTPServer`). Orchestrates audio capture, VAD auto-submitting, STT, DeepSeek LLM, tools, and TTS. |
| **Linux CLI & App Launcher** | [`bin/kurek`](bin/kurek) (`~/.local/bin/kurek`) | Single binary control: `kurek [toggle|prompt|status|start|stop]`. Auto-spawns daemon if offline. |
| **Desktop Entry** | [`desktop/kurek.desktop`](desktop/kurek.desktop) | Standard FreeDesktop `.desktop` entry. Appears in Omarchy launcher (`Super+Space`) under Apps with 1024x1024 retina icon. |
| **Hyprland Bindings** | `~/.config/hypr/bindings.lua` | Middle Click (`mouse:274`) and `SUPER + mouse:274` to summon Kurek. |
| **macOS Menu Bar UI** | [`menubar/KurekBar.swift`](menubar/KurekBar.swift) | Native Swift 6 status item for macOS. Polls `/status` at 10 Hz and monitors global `Fn` modifier flags. |
| **Launcher Script** | [`launch_kurek.sh`](launch_kurek.sh) | Cross-platform control script: `./launch_kurek.sh [start|stop|status]`. Uses `setsid` to detach permanently. |
| **Installer** | [`install_linux.sh`](install_linux.sh) | One-line installer for Arch Linux / Omarchy Quattro. |
| **LLM Client** | [`core/llm_client.py`](core/llm_client.py) | Direct `api.deepseek.com` client with OpenAI tool schemas (`deepseek-flash`). |
| **TTS Engine** | [`core/tts.py`](core/tts.py) | Implements `XAITTSEngine` (Grok Cloud TTS, voice: **Sol** / `sal`) playing via Linux `mpv` or macOS `afplay`. |
| **STT Engine** | [`core/stt.py`](core/stt.py) | Implements `DeepgramSTT` (Nova-2) and `WhisperSTT` (`faster-whisper`) with DC offset stripping and peak normalization. |
| **Memory Tool** | [`actions/memory_tool.py`](actions/memory_tool.py) | `manage_memory(action='remember'|'recall')`. Bidirectionally syncs with Hermes `USER.md` & `MEMORY.md`. |
| **Memory Files** | [`memory/kurek_history.json`](memory/kurek_history.json) | Saved multi-turn conversation history. Reloaded on daemon startup. |
| **External Memory** | `HERMES_PROFILE` / `HERMES_MEMORIES_DIR` / `~/.hermes/memories` | Optional Hermes `USER.md` + `MEMORY.md` continuity. |
| **Legacy GUI** | [`legacy/`](legacy/) | Unsupported PyQt6 JARVIS UI / dashboard / plugins (see `legacy/README.md`). |

---

## 3. Environment & Secrets

Environment variables are loaded from [`.env`](.env):

```bash
DEEPSEEK_API_KEY=sk-...   # Direct platform key for api.deepseek.com
XAI_API_KEY=xai-...        # Direct platform key for api.x.ai (Grok TTS)
DEEPGRAM_API_KEY=...      # Deepgram Nova-2 STT (falls back to local Whisper if omitted)
```

> [!IMPORTANT]
> Never use OpenRouter for Kurek. All DeepSeek calls route straight to `https://api.deepseek.com/chat/completions`.

---

## 4. State Machine & Visual Indicators

On Linux, real-time feedback is displayed through in-place desktop notifications:

| State | Notification Badge | Trigger / Meaning |
|-------|--------------------|-------------------|
| **IDLE** | `● Idle` | Ready and waiting for user input. |
| **LISTENING** | `🟢 Listening... (Speak now)` | Mic recording active. Auto-submits on 1.2s silence or max 12s. |
| **THINKING** | `🟡 Thinking...` | Transcribing audio, querying DeepSeek-Flash, or executing tools. |
| **SPEAKING** | `🔵 Speaking...` | Streaming speech audio via xAI Grok TTS (**Sol** voice). |

On macOS, the status is rendered by `KurekBar.swift` in the system menu bar.

---

## 5. Memory System & Hermes Continuity

Kurek uses the **Muse Memory** three-tier markdown memory plane, triaged by TypeSafe Jev:

1. **Daily logs:** `~/memory/YYYY-MM-DD.md`, the day's captured context.
2. **Durable core:** `~/MEMORY.md`, durable preferences and rules promoted by Jev.
3. **Standing alignment:** `~/ALIGNMENT_SYNTHESIS.md`, behavioural guidance distilled by the nightly dream cycle (`dream_tool`).

Supporting stores:
- `memory/kurek_history.json` keeps the rolling conversation context between turns.
- **Hermes continuity:** When configured, `manage_memory(action='remember')` also appends to Hermes `MEMORY.md`, and Kurek reads Hermes `USER.md` / `MEMORY.md` into its system prompt.

---

## 6. Available Tools & Capabilities

The daemon auto-discovers all tools in the [`actions/`](actions/) directory:

- **`open_app`**: Cross-platform launcher (`xdg-open` / binary on Linux, `open -a` on macOS).
- **`browser_control`**: Full Playwright browser automation (navigate, click, type, scrape).
- **`computer_settings`**: Volume (`pactl` / `osascript`), brightness (`brightnessctl`), Wi-Fi, Bluetooth.
- **`desktop_control`**: Window management (minimize, maximize, hide, tile).
- **`computer_control`**: Simulated keystrokes, mouse clicks, hotkeys, screenshots.
- **`reminder`**: Schedules system alarms and notifications.
- **`web_search`**: DuckDuckGo web search and real-time news retrieval.
- **`manage_memory`**: Stores and retrieves personal knowledge, synced with Hermes.
- **`weather_report`**, **`youtube_video`**, **`code_helper`**, **`file_controller`**, etc.

---

## 7. Developer Operations & Quick CLI Commands

### Start Daemon
```bash
kurek start
# Or via script:
./launch_kurek.sh
```

### Stop All Instances
```bash
kurek stop
```

### Check Daemon Status
```bash
kurek status
# Or curl:
curl -s http://127.0.0.1:8790/status
```

### Test Prompt Programmatically (Without Mic)
```bash
kurek prompt "Open browser and check latest Rust news"
```

### Toggle Listening via Mouse or Key
- **Middle Click**: Click mouse scroll wheel (`mouse:274`).
- **Super + Middle Click**: Secondary shortcut.
- **App Launcher**: Press `Super + Space`, type `Kurek`, hit `Enter`.

### View Live Daemon Logs
```bash
tail -f /tmp/kurek_daemon.log
```
