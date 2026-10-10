# AGENTS.md — Developer & AI Agent Guide for Kurek (JARVIS)

> **Kurek** is an ultra-fast, low-RAM (~60MB total), headless personal AI assistant for **Arch Linux / Omarchy Quattro (Hyprland)** and **macOS**. Features instant Middle Click mouse summon, native desktop launcher, DeepSeek-Flash reasoning, xAI Grok speech (**Sol** voice), Hermes bidirectional memory continuity, and 17 direct computer-control tools.

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
│  │  • DC offset removal │   │  • 17 OpenAI Tools    │   │  • macOS afplay           │  │
│  │  • Peak normalization│   │  • Unrestricted Jarvis│   │  • In-place notifications │  │
│  └──────────────────────┘   └───────────┬───────────┘   └───────────────────────────┘  │
│                                         │                                              │
│                                         ▼                                              │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │                         17 Computer Control & Core Tools                         │  │
│  │  • open_app           • browser_control     • desktop_control   • reminder       │  │
│  │  • computer_control   • computer_settings   • manage_memory     • weather        │  │
│  │  • file_controller    • dev_agent           • web_search        • youtube_video  │  │
│  └──────────────────────────────────────┬───────────────────────────────────────────┘  │
│                                         │                                              │
│                                         ▼                                              │
│  ┌──────────────────────────────────────────────────────────────────────────────────┐  │
│  │                             Persistent Memory System                             │  │
│  │  • Rolling Context: memory/kurek_history.json (multi-turn persistence)           │  │
│  │  • Hermes Continuity Sync: ~/.hermes/profiles/eldio/memories/                   │  │
│  │    (reads full USER.md & MEMORY.md, syncs bidirectional remember calls)          │  │
│  │  • Local Store: memory/long_term.json                                            │  │
│  └──────────────────────────────────────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Key Components & File Locations

| Component | File Path | Description |
|-----------|-----------|-------------|
| **Python Daemon** | [`kurek_daemon.py`](file:///home/arch/Projects/JARVIS/kurek_daemon.py) | Headless background HTTP service on port `8790` (using `ThreadingHTTPServer`). Orchestrates audio capture, VAD auto-submitting, STT, DeepSeek LLM, tools, and TTS. |
| **Linux CLI & App Launcher** | [`bin/kurek`](file:///home/arch/Projects/JARVIS/bin/kurek) (`~/.local/bin/kurek`) | Single binary control: `kurek [toggle|prompt|status|start|stop]`. Auto-spawns daemon if offline. |
| **Desktop Entry** | [`desktop/kurek.desktop`](file:///home/arch/Projects/JARVIS/desktop/kurek.desktop) | Standard FreeDesktop `.desktop` entry. Appears in Omarchy launcher (`Super+Space`) under Apps with 1024x1024 retina icon. |
| **Hyprland Bindings** | `~/.config/hypr/bindings.lua` | Middle Click (`mouse:274`) and `SUPER + mouse:274` to summon Kurek. |
| **macOS Menu Bar UI** | [`menubar/KurekBar.swift`](file:///home/arch/Projects/JARVIS/menubar/KurekBar.swift) | Native Swift 6 status item for macOS. Polls `/status` at 10 Hz and monitors global `Fn` modifier flags. |
| **Launcher Script** | [`launch_kurek.sh`](file:///home/arch/Projects/JARVIS/launch_kurek.sh) | Cross-platform control script: `./launch_kurek.sh [start|stop|status]`. Uses `setsid` to detach permanently. |
| **Installer** | [`install_linux.sh`](file:///home/arch/Projects/JARVIS/install_linux.sh) | One-line installer for Arch Linux / Omarchy Quattro. |
| **LLM Client** | [`core/llm_client.py`](file:///home/arch/Projects/JARVIS/core/llm_client.py) | Direct `api.deepseek.com` client with OpenAI tool schemas (`deepseek-flash`). |
| **TTS Engine** | [`core/tts.py`](file:///home/arch/Projects/JARVIS/core/tts.py) | Implements `XAITTSEngine` (Grok Cloud TTS, voice: **Sol** / `sal`) playing via Linux `mpv` or macOS `afplay`. |
| **STT Engine** | [`core/stt.py`](file:///home/arch/Projects/JARVIS/core/stt.py) | Implements `DeepgramSTT` (Nova-2) and `WhisperSTT` (`faster-whisper`) with DC offset stripping and peak normalization. |
| **Memory Tool** | [`actions/memory_tool.py`](file:///home/arch/Projects/JARVIS/actions/memory_tool.py) | `manage_memory(action='remember'|'recall')`. Bidirectionally syncs with Hermes `USER.md` & `MEMORY.md`. |
| **Memory Files** | [`memory/kurek_history.json`](file:///home/arch/Projects/JARVIS/memory/kurek_history.json) | Saved multi-turn conversation history. Reloaded on daemon startup. |
| **External Memory** | `~/.hermes/profiles/eldio/memories/` | Contains `USER.md` (profile of NDI) and `MEMORY.md` (knowledge base). |

---

## 3. Environment & Secrets

Environment variables are loaded from [`.env`](file:///home/arch/Projects/JARVIS/.env):

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

Kurek features a **three-tier memory architecture**:

1. **Short-Term Conversational Memory:**
   - In-flight messages within the current session.
   - Automatically saved to `memory/kurek_history.json` after every turn.
   - Last 10 turns are re-injected as context on every new user query.
2. **Long-Term Structured Memory:**
   - Stored in `memory/long_term.json`.
   - Managed via `actions/memory_tool.py` using `manage_memory(action='remember', category=..., key=..., value=...)`.
3. **Hermes Continuity Sync:**
   - On every request, Kurek dynamically resolves `~/.hermes/profiles/eldio/memories/USER.md` and `MEMORY.md`.
   - Injects the user's complete profile (NDI, Slovenia, Omarchy Quattro / Arch Linux, brand values, active projects) into the system prompt.
   - When Kurek executes `manage_memory(action='remember')`, it automatically appends the fact to Hermes `MEMORY.md` (`§ [CATEGORY] Key: Value`) so both assistants share knowledge in real time.

---

## 6. Available Tools & Capabilities

The daemon auto-discovers all tools in the [`actions/`](file:///home/arch/Projects/JARVIS/actions/) directory:

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
