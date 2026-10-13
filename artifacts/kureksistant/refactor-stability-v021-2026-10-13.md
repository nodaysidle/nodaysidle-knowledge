---
type: artifact
artifact_kind: refactor
topic_slug: kureksistant
generated: 2026-10-13
generator_agent: Antigravity
repo_ref: main @ f0a7cdf
version: v0.2.1
verified_at: 2026-10-13T23:51:52+02:00
tags:
  - artifact
  - refactor
  - kureksistant
  - omarchy
  - hyprland
---

# Kureksistant v0.2.1 Architectural & Stability Refactor

**Execution Date:** 2026-10-13 23:51 (UTC+2)  
**Agent:** Antigravity  
**Commit:** `f0a7cdf` (`feat(arch): Omarchy Hyprland integration, SQLite FTS5 memory & stability hardening (v0.2.1)`)  
**Target Environment:** Arch Linux / Omarchy Quattro (Hyprland, Ghostty, Herdr, Fish shell) & Android Remote Client over Tailscale.

---

## 1. Executive Summary

This release resolves systemic crash paths on `.env`-only installations, replaces legacy X11 abstractions with native Omarchy Hyprland mechanics, shields the systemd 600M memory envelope from heavy subprocesses, optimizes the Android remote client experience over Tailscale, aligns LLM system prompts with active runtime tool schemas, and modernizes memory management from full-file JSON rewrites to SQLite WAL mode with FTS5 full-text indexing.

---

## 2. Before vs. Now Matrix

| Area | Before (v0.2.0) | Now (v0.2.1 Refactor) |
|---|---|---|
| **API Keys & Config** | `actions/` modules (`dev_agent`, `code_helper`, `computer_settings`, etc.) directly read `config/api_keys.json`, throwing `FileNotFoundError` on `.env`-only Arch installations. | All actions route through `memory.config_manager.get_gemini_key()`, prioritizing `os.environ["GEMINI_API_KEY"]` before safely falling back without crashing. |
| **Omarchy & Hyprland** | Ignored Omarchy terminal emulators; mapped shells to bash; used X11 `pyautogui` hotkeys (`alt+tab`, `ctrl+w`, `f11`) that fail under Wayland; ran CLI `htop` headlessly without a terminal. | Prioritizes `ghostty` and `herdr` emulators at the top of `open_app.py` fallbacks and aliases; supports `fish`; `computer_settings.py` uses native `hyprctl dispatch` (`cyclenext`, `killactive`, `fullscreen 0`, `movewindow l/r`, `dpms off`), `grim` screenshots, and spawns `btop`/`htop` inside Ghostty/Herdr. |
| **Remote Android Client** | Prompts from Android over Tailscale (`/remote/prompt`) fired local workstation PipeWire speakers into an empty room and burnt xAI TTS credits; unconfirmed destructive actions had no conversational gate. | Local TTS is muted on remote turns unless `speak_local=True` or `KUREK_REMOTE_LOCAL_TTS=1`; bound headless `notify-send` confirmation gate and conversational affirmative/negative ("yes"/"no") turn resolution in `kurek_daemon.py`. |
| **System Prompt Alignment** | `core/prompt.txt` referenced outdated PyQt6 GUI HUD buttons, click targets, and hallucinated tool names (`screen_process`, `save_memory`, `shutdown_jarvis`). | Synchronized `core/prompt.txt` with discovered tool schemas (`screen_vision`, `manage_memory`, `system_monitor`, `vault_knowledge`, `workstation_radar`, `process_sentinel`) and Omarchy workstation context. |
| **Systemd 600M Envelope** | Running Playwright Chromium or project builds inside `kurek.service` breached `MemoryMax=600M`, causing systemd OOM-kills; tool errors could hang the daemon in `THINKING`. | Low-memory Chromium flags passed in `actions/browser_control.py`; child build processes wrapped via `systemd-run --user --scope` in `actions/dev_agent.py`; 120s timeout guard added to `core/action_loader.py`. |
| **Memory Architecture** | `memory/long_term.json` was read and rewritten entirely on every store, performing linear regex scans; `actions/background_monitor.py` tightly coupled to private `_lock`. | Migrated `memory/memory_manager.py` to SQLite (`memory/kurek_memory.db`) with `WAL` journal mode and `FTS5` full-text search indexing; automatic zero-loss migration of legacy JSON data; decoupled background monitor state with public thread-safe helpers. |

---

## 3. Tasks Executed & Technical Implementation

### Task 1: Eliminate Direct `config/api_keys.json` Reads in `actions/`
- **Root Cause:** Raw `open(API_CONFIG_PATH)` calls crashed whenever `config/api_keys.json` was absent (which is explicitly ignored in `.gitignore` and omitted in `.env` installs).
- **Fix:** Ensured `memory/config_manager.py:get_gemini_key()` checks `os.environ.get("GEMINI_API_KEY")` first, safely returning `""` if neither exists. Replaced all raw JSON opens in:
  - `actions/dev_agent.py`
  - `actions/code_helper.py`
  - `actions/flight_finder.py`
  - `actions/desktop.py`
  - `actions/file_processor.py`
  - `actions/computer_settings.py`
  - `actions/computer_control.py`
  - `actions/youtube_video.py`
- **Test:** Added `tests/test_api_key_env_fallback.py` asserting key resolution with and without `config/api_keys.json`.

### Task 2: First-Class Support for Ghostty, Herdr, Fish, and Hyprland
- **Terminal Priorities:** Placed `ghostty` and `herdr` as the top priority entries in `_LINUX_TERMINAL_FALLBACKS` and added aliases for `fish`, `ghostty`, and `herdr` in `actions/open_app.py`. Terminal launches now resolve installed binaries cleanly without shell wrapper errors.
- **Hyprland Dispatches:** In `actions/computer_settings.py`:
  - `_is_hyprland()` checks `HYPRLAND_INSTANCE_SIGNATURE` and `hyprctl`.
  - Dispatches native window actions: `cyclenext`, `killactive`, `fullscreen 0`, `movewindow l/r`, `dpms off`.
  - Screenshots use native Wayland `grim` directly to `~/Pictures` or `~/Desktop`.
  - Screen locking checks `hyprlock` and `swaylock` before `loginctl`.
  - Task manager launches `btop` or `htop` inside a detected `ghostty` or `herdr` window instead of headless CLI failure.
- **Test:** Added `tests/test_omarchy_terminal_hyprland.py` verifying fallback ordering, aliases, and Hyprland command dispatching.

### Task 3: Optimize `/remote/prompt` SSE for Android over Tailscale
- **Audio Output:** In `kurek_daemon.py`, `/remote/prompt` turns (`remote=True`) now stream JSON SSE events (`tool`, `sentence`, `done`) without dispatching local PipeWire `mpv_sink` audio playback unless `speak_local` is explicitly set or `KUREK_REMOTE_LOCAL_TTS=1`.
- **Conversational Affirmations:** Wired `core/confirm.py` with `notify-send`. When an irreversible action is pending confirmation, the daemon checks incoming prompts for affirmative (`yes`, `confirm`, `do it`, `sure`, `ja`) or negative (`no`, `cancel`, `stop`, `abort`) intent, resolving the action immediately without unnecessary LLM invocation.
- **Android App:** Verified Android client `MainActivity.java` defaults to `""` for token and host, prompting the user for configuration instead of relying on insecure hardcoded literals.

### Task 4: Align `core/prompt.txt` with Active Runtime Tool Schemas
- Rewrote `core/prompt.txt` to eliminate legacy PyQt6 HUD references and removed nonexistent tool names (`screen_process`, `save_memory`, `shutdown_jarvis`, `agent_task`).
- Fully documented active Omarchy tools: `screen_vision`, `manage_memory`, `system_monitor`, `vault_knowledge`, `workstation_radar`, `process_sentinel`, `draft_to_clipboard`, `manage_clipboard`.

### Task 5: Protect `kurek.service` `MemoryMax=600M` Envelope
- **Playwright Low-Memory:** In `actions/browser_control.py`, launched Chromium instances receive `--disable-dev-shm-usage` and `--js-flags=--max-old-space-size=256`.
- **Systemd Scope Isolation:** External builds and commands run by `actions/dev_agent.py` under Linux systemd are wrapped with `systemd-run --user --scope --quiet --`, placing child memory into a transient scope outside `kurek.service`'s 600M cgroup.
- **Action Timeout:** Added 120s timeout guard in `core/action_loader.py:ActionRegistry.run` so tool execution timeouts never leave the daemon stuck in `THINKING`.

### Task 6: SQLite WAL + FTS5 Memory Engine & Private Lock Decoupling
- **Database Engine:** Replaced `memory/long_term.json` in `memory/memory_manager.py` with `memory/kurek_memory.db` backed by SQLite.
- **WAL & FTS5:** Enabled `PRAGMA journal_mode=WAL` and created `entries_fts` virtual table using SQLite FTS5 with synchronized insert/update/delete triggers.
- **Zero-Loss Migration:** Automatically migrates preexisting `memory/long_term.json` records on startup.
- **Lock Decoupling:** Decoupled `actions/background_monitor.py` from `memory.memory_manager._lock`, providing public `load_monitors()` and `save_monitors()` helpers.
- **Test:** Added `tests/test_sqlite_memory_manager.py` verifying SQLite transactions, FTS5 search scoring, migration, and monitor lock separation.

---

## 4. Verification and Validation Results

1. **Unit Test Suite:**
   - Command: `.venv/bin/pytest -v tests/`
   - Results: **90 passed, 1 skipped** (shellcheck on install script) in 5.49s.
2. **Static Analysis & Linters:**
   - Command: `.venv/bin/ruff check kurek_daemon.py core actions memory bin scripts tests setup.py --select E9,F63,F7,F821 --exclude legacy`
   - Results: **All checks passed (0 errors)**.
3. **Trigger Client Compilation:**
   - Command: `gcc -O2 -Wall -Wextra -Werror bin/kurek-trigger.c -o bin/kurek-trigger`
   - Results: **Clean build, zero warnings or errors**.
4. **Shell Script Validation:**
   - Command: `bash -n install_linux.sh`
   - Results: **Syntax OK**.

---

## 5. Artifact & Repository References

- **Git Commit:** `f0a7cdf` on `main`
- **Release Version:** `v0.2.1` documented in `CHANGELOG.md`
- **Canonical Concept Note:** [[wiki/concepts/kureksistant-overview]]
- **Catalog Entry:** [[_system/templates/catalog/kurekizmo]]
- **Session Record:** [[sessions/2026-10-08-kureksistant-session]]
