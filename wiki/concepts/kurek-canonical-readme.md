---
type: wiki-note
note_kind: canonical-reference
topic_slug: kureksistant
title: "Kureksistant (Kurek) Canonical README"
status: active
canonical_source: "kurekizmo/README.md"
tags:
  - wiki
  - kureksistant
  - canonical-reference
---

> [!IMPORTANT]
> **CANONICAL GROUND TRUTH FOR ALL AGENTS (EO, SHIP, REACH, REEL, ATLAS):**
> Kurek is intentionally a **headless Python daemon (`kurek_daemon.py`) with NO GUI**, summoned by mouse middle-click (`mouse:274`), hotkey, or CLI. The old PyQt6 GUI in `legacy/` is completely obsolete and unsupported. All copy, releases, and promotion must lead with: *"A headless voice assistant daemon on Linux — no GUI on purpose."*

<p align="center">
  <img src="desktop/kurek.png" alt="Kureksistant icon" width="128" />
</p>

<h1 align="center">Kureksistant (Kurek)</h1>

<p align="center">
  <strong>A voice assistant daemon for an Omarchy / Hyprland Linux desktop, with an optional phone remote over Tailscale.</strong>
</p>

<p align="center">
  <a href="https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.1"><img src="https://img.shields.io/badge/Release-v0.2.1-blue.svg?style=flat-square" alt="Release v0.2.1"></a>
  <img src="https://img.shields.io/badge/Desktop-Arch%20%2F%20Omarchy%20%2F%20Hyprland-1793D1?style=flat-square&logo=arch-linux&logoColor=white" alt="Arch / Omarchy / Hyprland">
  <img src="https://img.shields.io/badge/Remote-Android%20app%20(debug%20APK%20in%20v0.2.1)-3DDC84?style=flat-square&logo=android&logoColor=white" alt="Android remote">
  <img src="https://img.shields.io/badge/License-CC%20BY--NC%204.0-lightgrey?style=flat-square" alt="License">
</p>

---

Kurek is a headless Python daemon (`kurek_daemon.py`) that runs as a systemd user service on your Linux desktop. You summon it with a mouse middle-click, a hotkey or the `kurek` CLI. It listens, thinks with DeepSeek-Flash, talks back with xAI Grok TTS (voice **Sol**), and can act on your desktop through about two dozen tool modules in [`actions/`](actions/), including windows, apps, the browser, files, the clipboard, screen vision and memory.

It is built and tested first on **Arch Linux with Omarchy / Hyprland**. A macOS menu-bar client exists ([`menubar/`](menubar/)) but is less exercised. The old PyQt6 GUI lives in [`legacy/`](legacy/) and is unsupported.

**Latest release: [v0.2.1, Omarchy Integration & Stability Refactor](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.1)** (see also [CHANGELOG.md](CHANGELOG.md)).

---

## ✨ Features (v0.2.1)

### Omarchy / Hyprland desktop integration
- **Terminals and shell:** Ghostty and Herdr are preferred, and there's a Fish shell alias. btop/htop open in a terminal.
- **Native `hyprctl dispatch` window control:**
  - cycle windows;
  - focus an already-open app (`workspace` + `focuswindow address:`);
  - full-screen toggle, which reads the current state and sets the opposite;
  - maximize (`fullscreen 1`);
  - snap the active window to the left or right half of the focused monitor;
  - display off (`dpms`).
- **Close:** "close this", "close it" and "close tab" close the current tab (Ctrl+W). Only an explicit "close window" closes the whole window (`killactive`).
- **Screen vision:** `grim` captures the active window and sends it to Gemini Flash. Hyprland context comes from the `.socket2.sock` event stream.
- **Summon:** a compiled C trigger (`bin/kurek-trigger`) over the Unix socket `$XDG_RUNTIME_DIR/kurek.sock`.

### Phone remote over Tailscale (opt-in)
- An Android app, **Kurek Remote**, is built from [`android/`](android/). It sends prompts to `POST /remote/prompt` and receives the reply as a Server-Sent Events stream (`sentence` / `tool` / `done`).
- Off by default. Enable it with `KUREK_REMOTE_BIND=tailscale` and a Bearer token of **32+ characters** (`KUREK_REMOTE_TOKEN`).
- **Silent on the PC by default:** remote prompts don't speak through the PC's speakers. Opt in per request with `"speak_local": true`, or globally with `KUREK_REMOTE_LOCAL_TTS=1`.
- A debug-signed APK (Kurek Remote) is attached to the [v0.2.1 release](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.1). Uninstall any older copy of the app first. You can also build it yourself (see below).

### Conversational yes/no confirmations
- Risky actions ask for confirmation, shown on the PC via `notify-send`.
- While one is pending, a reply that is **entirely** a yes/no word or phrase confirms or cancels it ("yes", "ok", "do it", "no", "cancel", "never mind" and so on).
- Anything longer, such as "notes for today" or "stop the music", is handled as a normal prompt.
- **By design**, an authenticated phone request may confirm or cancel a confirmation that was raised on the PC.

### Memory: SQLite (WAL + FTS5) with auto-migration
- Long-term memory lives in `memory/kurek_memory.db`, in SQLite WAL mode with an FTS5 full-text index. Recall falls back to plain word matching.
- On first start, the legacy `memory/long_term.json` is imported automatically.
  - If the import fails, it is rolled back, logged and retried on the next start.
  - The JSON file is never overwritten before migration has completed, and it is then kept up to date as a compatibility copy.
- Separately, the Muse memory layer keeps daily logs in `~/memory/`, a durable core in `~/MEMORY.md` and standing alignment in `~/ALIGNMENT_SYNTHESIS.md`. Optional TypeSafe Jev triage decides what gets promoted. Optional Hermes continuity is available via `HERMES_PROFILE` / `HERMES_MEMORIES_DIR`.

### Stability: the 600M systemd memory limit
- `kurek.service` runs with `MemoryHigh=512M` / `MemoryMax=600M` and `Restart=on-failure`.
- Heavy child jobs (dev-agent builds, pip installs, project runs) are started in their own `systemd-run --user --scope`, so their memory isn't counted against the service. Chromium is launched with low-memory flags.
- Tool calls time out after **120 s**. A timed-out tool is reported as **timed out, never as success, and never retried**. Calling the same tool again while the earlier call is still running is refused.

### Environment-first API keys
- Keys are read from the environment / `.env` first.
- For the Gemini key, `config/api_keys.json` is the legacy fallback. A missing key no longer crashes the actions that use it.

### Other tools (unchanged)
- `process_sentinel`: announces when long builds or tests finish.
- `draft_to_clipboard`: dictate commit messages and PR text into `wl-copy`.
- `workstation_radar`: git status across `~/Projects` and `~/dev`.
- `vault_knowledge`: queries the nodaysidle-knowledge Obsidian vault.
- `dream_tool`: nightly reflection journal.
- Also: Playwright browser control, web search, file management (deletion requires confirmation), volume/brightness, alarms, and the clipboard manager.

---

## ⚡ Install (Linux)

### Option: download the v0.2.1 bundle

Download [`kureksistant-v0.2.1-linux-x86_64.tar.gz`](https://github.com/nodaysidle/kureksistant/releases/download/v0.2.1/kureksistant-v0.2.1-linux-x86_64.tar.gz) and [`SHA256SUMS.txt`](https://github.com/nodaysidle/kureksistant/releases/download/v0.2.1/SHA256SUMS.txt), then:

```bash
grep ' kureksistant-v0.2.1-linux-x86_64.tar.gz$' SHA256SUMS.txt | sha256sum -c - && \
echo '8b3a7a6ec36795d6651a3b38d36b62f5dc1590a5a17abe1a3604ecf8c7a96b33  kureksistant-v0.2.1-linux-x86_64.tar.gz' | sha256sum -c - && \
tar -xzf kureksistant-v0.2.1-linux-x86_64.tar.gz && \
cd kureksistant-0.2.1 && \
./install_linux.sh
```

### 1. Clone and run the installer

```bash
git clone https://github.com/nodaysidle/kureksistant.git
cd kureksistant
./install_linux.sh
```

`install_linux.sh` does the following:
- creates `.venv` and installs `requirements.txt` plus the Playwright Chromium;
- compiles `kurek-trigger`;
- installs `~/.local/bin/kurek`, the icon and the desktop entry;
- renders the systemd user unit into `~/.config/systemd/user/kurek.service`. The unit loads your settings with `EnvironmentFile=-<install dir>/.env`;
- creates `.env` from `.env.example` only if it doesn't exist yet.

### 2. Configure `.env`

```bash
nano .env
```

| Variable | Required | Purpose |
|---|---|---|
| `DEEPSEEK_API_KEY` | **Yes** | Reasoning and tool dispatch (DeepSeek-Flash). |
| `XAI_API_KEY` | **Yes** | Speech (xAI Grok TTS, voice Sol). |
| `GEMINI_API_KEY` | Optional | Screen vision and Gemini-backed tools. |
| `DEEPGRAM_API_KEY` | Optional | Deepgram Nova-2 STT. Falls back to local `faster-whisper`. |
| `TYPESAFE_API_KEY` | Optional | TypeSafe Jev triage / screen-context fallback. |
| `OPENROUTER_API_KEY` | Optional | Decision-1 auto screen-context (prompt text is sent to OpenRouter when set). |
| `KUREK_AUTO_SCREEN` | Optional | `0` disables auto screen-context. |
| `KUREK_DECISION_TIMEOUT` | Optional | Decision-1 HTTP timeout in seconds. |
| `KUREK_USER_NAME` | Optional | How Kurek addresses you. |
| `HERMES_PROFILE` / `HERMES_MEMORIES_DIR` | Optional | Hermes memory continuity. |
| `INPUT_DEVICE` | Optional | Microphone name substring. |
| `KUREK_PROJECT_DIR` | Optional | Install path for the macOS menu-bar client. |
| `KUREK_TIMING` | Optional | `1` logs per-query timing deltas. |
| `KUREK_REMOTE_BIND` | For phone | `tailscale` enables the remote bind (see below). |
| `KUREK_REMOTE_TOKEN` | For phone | Bearer token, **at least 32 characters** (`openssl rand -hex 32`). |
| `KUREK_REMOTE_ALLOW_EXEC` | Optional | `1` lets remote prompts use exec-capable tools. Leave it empty unless you need that. |
| `KUREK_REMOTE_LOCAL_TTS` | Optional | `1` makes remote prompts also speak on the PC. |
| `KUREK_BIND` | Optional | Explicit bind host. Never use `0.0.0.0` unless you understand the risk. |

Phone-remote example:

```bash
# openssl rand -hex 32  → paste the output as the token
KUREK_REMOTE_TOKEN=<64-hex-char token>
KUREK_REMOTE_BIND=tailscale
```

### 3. Start the service

```bash
systemctl --user daemon-reload
systemctl --user enable --now kurek     # or: kurek start
systemctl --user status kurek
journalctl --user -u kurek -f           # the log shows the bind addresses
curl -s http://127.0.0.1:8790/status
```

With `KUREK_REMOTE_BIND=tailscale`, the log shows two listeners: `127.0.0.1:8790` and your Tailscale IPv4 (`100.x.y.z:8790`). If Tailscale isn't up yet at boot, the daemon stays on loopback and retries.

**System dependencies (Linux):**
- PipeWire with `mpv`;
- `notify-send`;
- `grim`;
- `wl-clipboard`;
- `hyprctl` (Hyprland);
- a C compiler for `kurek-trigger`;
- Tailscale for the phone remote.

### Hyprland bindings

```lua
-- ~/.config/hypr/bindings.lua
o.bind("mouse:274", "Summon Kurek Middle Click", "~/.local/bin/kurek-trigger toggle", { mouse = true })
o.bind("SUPER + mouse:274", "Summon Kurek Super+Middle Click", "~/.local/bin/kurek-trigger toggle", { mouse = true })
```

### CLI

```bash
kurek toggle           # start/stop listening
kurek status           # daemon state
kurek prompt "..."     # text prompt without the mic
kurek start | stop     # systemd user service
kurek-trigger toggle   # C trigger over the Unix socket
```

---

## 📱 Android remote (Kurek Remote)

A **debug-signed APK** (Kurek Remote) is attached to the [v0.2.1 release](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.1). It is signed with a throwaway debug key, so **uninstall any older copy of the app first**. Or build it from [`android/`](android/) (the Android SDK is required; the Gradle wrapper is included):

```bash
cd android
./gradlew :app:assembleDebug
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

In the app's settings, fill in:
- **Host:** the PC's Tailscale IPv4 (`tailscale ip -4`) or MagicDNS name.
- **Port:** `8790`.
- **Token:** the same `KUREK_REMOTE_TOKEN`.

The status should show **ONLINE**.

**Check it from another Tailscale device:**
- A prompt with the correct token returns `200` with `text/event-stream`.
- A wrong or missing token returns **`401`**.

Traffic is plain HTTP inside Tailscale/WireGuard. The daemon doesn't terminate TLS itself.

---

## 🔒 Security model (summary)

Full details and how to report issues: **[SECURITY.md](SECURITY.md)**.

- **Bind:** HTTP binds to `127.0.0.1:8790` by default. Remote access is opt-in with `KUREK_REMOTE_BIND=tailscale`, which adds only the Tailscale IPv4.
- **Token:** if the remote token is missing or shorter than 32 characters, the daemon **refuses** to bind remotely. Non-loopback requests need `Authorization: Bearer <token>`, compared in constant time (`hmac.compare_digest`).
- **Browser requests:** cross-origin/CSRF requests carrying an `Origin` header are rejected, and there is no `CORS *`.
- **Body limit:** request bodies are capped at 64 KB.
- **Exec tools:** remote prompts can't use exec-capable tools (`desktop_control`, `code_helper`, `dev_agent`) unless `KUREK_REMOTE_ALLOW_EXEC=1`.
- **Phone confirmations:** a remote client with the token can confirm pending confirmations, as described above. Treat the token like a password, and rotate it (`openssl rand -hex 32`) if it was ever shared or shipped in a build.
- **Local access:** the loopback API is unauthenticated by design. Any local process can call it.
- **Secrets:** `.env` and `config/api_keys.json` must never be committed or packaged.

---

## ⬆️ Upgrading from v0.2.0

1. **Back up your memory first:**
   ```bash
   cp memory/long_term.json memory/long_term.json.bak-$(date +%F)
   ```
2. Update the code (`git pull`) and re-run `./install_linux.sh`. This re-renders the unit with `EnvironmentFile` and keeps your `.env`.
3. Restart at a quiet time:
   ```bash
   systemctl --user daemon-reload && systemctl --user restart kurek
   ```
4. Check the log for `Migrated legacy long_term.json into kurek_memory.db`. If you see `Migration error (will retry next start)`, your JSON file is untouched. Fix the cause and restart.
5. If you use the phone remote, send a test prompt from the app, and check that a wrong token returns `401`.

---

## ⚠️ Known limits

- **Not offline:** reasoning (DeepSeek) and voice (xAI) need cloud API keys and internet. Only speech-to-text can fall back to local `faster-whisper`.
- **Desktop scope:** Hyprland/Omarchy comes first. Other Wayland compositors need their own keybinds, and the Hyprland-specific window actions won't apply there.
- **Timed-out tools keep running:** they can't be killed. After 120 s Kurek reports the timeout, but the tool may finish in the background.
- **Confirmation wording:** after a "yes", Kurek replies "Confirmed and executed." as soon as the action is started, before its result is known.
- **Memory headroom:** the service can run close to `MemoryHigh=512M` with faster-whisper and Chromium loaded. If it exceeds `MemoryMax=600M`, systemd restarts it, and an in-flight request is dropped.
- **Local tool permissions:** tools run with your user's permissions. Creating files is unrestricted, and deleting needs confirmation.
- **Lint:** older modules still have ruff warnings.

---

## 📄 License

[CC BY-NC 4.0](LICENSE) (`SPDX-License-Identifier: CC-BY-NC-4.0`) — derived from FatihMakes' JARVIS ("MARK 53 — JARVIS"). Kureksistant changes by [NODAYSIDLE](https://github.com/nodaysidle). See [NOTICE](NOTICE).

Security reports (including key leaks): see [SECURITY.md](SECURITY.md).
