---
type: wiki-note
note_kind: concept
topic_slug: kureksistant
status: draft
created: 2026-10-07
updated: 2026-10-10
tags:
  - wiki
  - kureksistant
---

# Kureksistant (Kurek) — overview

## Summary

Kureksistant is a headless Python voice-assistant daemon on `127.0.0.1:8790` for Arch Linux/Hyprland, with a secondary macOS menu-bar path. It is summoned by middle-click or the Fn key. Reasoning uses DeepSeek-Flash, voice uses xAI Grok TTS ("Sol"), and screen vision uses Gemini Flash. v0.1.0 ships as an unsigned Linux tarball. Local folder: `kurekizmo`.

## Current status (2026-10-08 03:32 UTC+2)

Newer facts here take precedence over the older figures in Details (~55MB, the `91c4cf1b…` checksum).

- **Repo:** public. `main` = `d863922`. Audit grade **C−**: [[artifacts/kureksistant/audit-2026-10-08]].
- **Lineage:** `kurekizmo` was made private on GitHub; `kureksistant` was created as the public repository specifically incorporating TypeSafe Jev cognitive memory triage and deep daemon optimizations (~333MB RAM, faster-whisper, 24 tools).
- **Done 2026-10-08 (Execution Operator / Grok Bot, Cursor cloud agent `bc-e01c8f24-b3e6-5c91-afb6-bee6dd7d455c`):**
  - **Key leak fixed in the release:** the public v0.1.0 tarball had shipped `config/api_keys.json` with likely-live Gemini and OpenRouter keys. The asset was re-cut on the same tag without secrets. New SHA-256: `a4085d73ae8764f6b9034e3caabd4c4278f345d074f7909dad171dea63861003`. `SHA256SUMS.txt` was replaced, and the new tarball contains 0 `api_keys.json` and 0 `.env`. The user's local `config/api_keys.json` was left untouched on purpose.
  - **[PR #2](https://github.com/nodaysidle/kureksistant/pull/2)** (squash, `31d7e56`):
    - The headless daemon is the only entrypoint. The legacy PyQt6 JARVIS GUI (`main.py`, `ui.py`, `dashboard/`, `plugins/`, `jarvis.ico`) moved to `legacy/`.
    - Added `SECURITY.md`, `NOTICE` and an SPDX `CC-BY-NC-4.0` `LICENSE`. GitHub may still show the licence as "Other".
    - Personal and machine-specific hardcodes became `.env` settings: `KUREK_USER_NAME`, `HERMES_PROFILE`, `HERMES_MEMORIES_DIR`, `INPUT_DEVICE`, `KUREK_PROJECT_DIR`.
    - Added `.github/workflows/ci.yml` (scoped ruff plus the daemon `/status` smoke test in `tests/test_daemon_smoke.py`).
    - Added a deny-list gate in `scripts/package_release.sh` that fails the build if a key file is packaged.
  - **[PR #3](https://github.com/nodaysidle/kureksistant/pull/3)** (squash, `52d009b`): the README, RAM badge, `AGENTS.md` and daemon docstring now say ~333MB RAM (with the default faster-whisper) and 24 tools. They said ~55MB and 28.
  - **Set by the user on GitHub:** description (~333MB) and topics `ai-assistant`, `deepseek`, `hyprland`, `linux`, `macos`, `personal-assistant`, `python`, `voice-assistant`. The Cursor GitHub app lacks admin permission (403).
- **Done 2026-10-10 (Antigravity — Arch Linux / Hyprland Performance & IPC Overhaul):**
  - **Unix Domain Socket & C Trigger Client:** Implemented `$XDG_RUNTIME_DIR/kurek.sock` asynchronous UDS server alongside HTTP `:8790`. Added compiled C binary (`bin/kurek-trigger.c` → `~/.local/bin/kurek-trigger`), cutting middle-click summon latency from ~50ms (bash/pgrep/curl) to **<2ms**, with auto-spawn fallback. Emits real-time state events over UDS for Waybar/AGS status synchronization.
  - **Sub-400ms Streaming Voice Pipeline:** Replaced full-response blocking with sentence-buffered streaming (`core/llm_client.py:stream_deepseek_sentences`). Chunks delimited by `[.!?\n]` immediately dispatch to xAI Grok Cloud TTS (**Sol** voice), dropping first-syllable speech latency from ~3.5s to **~350–500ms**.
  - **Persistent PipeWire mpv Sink (`core/mpv_sink.py`):** Pre-warms an idle `mpv` background process on PipeWire with IPC socket `$XDG_RUNTIME_DIR/kurek_mpv.sock`. Streams audio chunks out of `/dev/shm` (POSIX RAM tmpfs) with zero NVMe disk writes and enables instant barge-in interrupt (`{"command":["stop"]}`) on middle-click.
  - **Event-Driven Hyprland Watcher (`core/hyprland_watcher.py`):** Connects to `$XDG_RUNTIME_DIR/hypr/<inst>/.socket2.sock`. Caches active window class, title, workspace, and geometry in RAM (O(1) lookup), completely eliminating `hyprctl activewindow -j` CLI subprocess spawning.
  - **Zero-Disk Active Window Vision (`actions/screen_vision.py`):** Streams active window geometry via `grim -g "<coords>" -t jpeg -q 80 -` directly into `io.BytesIO` in RAM. Zero temporary file writes and sub-60ms capture speed.
  - **Native systemd User Service:** Created `~/.config/systemd/user/kurek.service` targeting `graphical-session.target` with journald logging and a strict resource envelope (`MemoryHigh=250M`, `MemoryMax=450M`).
  - **Hyprland Bindings Updated:** Updated `~/.config/hypr/bindings.lua` mouse:274 and SUPER+mouse:274 to call `/home/arch/.local/bin/kurek-trigger toggle` directly.
- **Waiting on the user:** revoke the old Gemini and OpenRouter keys in their dashboards, because the old tarball was public. Status: **unconfirmed**.
- **Open (deferred):**
  - The localhost control API has no authentication.
  - `actions/desktop.py` runs model-generated code with `exec`.
  - The legacy code in `legacy/` still has ruff errors (1,236 repo-wide at audit time) and mypy strict errors.

## Details

- **Runtime:** Python daemon (`kurek_daemon.py`), `kurek` CLI (`toggle|prompt|status|start|stop`), with IDLE / LISTENING / THINKING / SPEAKING states shown via desktop notifications.
- **Cloud dependence:**
  - DeepSeek and xAI keys are required; Gemini, Deepgram and TypeSafe keys are optional.
  - Speech-to-text falls back to local `faster-whisper`.
  - It is not usable offline.
- **Memory:** Muse Memory, in three tiers (`~/memory/YYYY-MM-DD.md`, `~/MEMORY.md`, `~/ALIGNMENT_SYNTHESIS.md`), with TypeSafe Jev triage and two-way Hermes sync (`~/.hermes/profiles/eldio/memories/`).
- **Tools:** auto-discovered from `actions/`. Examples: screen_vision, workstation_radar, process_sentinel, draft_to_clipboard, dream_tool, browser_control (Playwright), file_controller.
- **Safety posture:**
  - Tools run with the user's permissions.
  - File creation is unrestricted; deletion needs a spoken yes/no.
  - The release is unsigned.
- **History:**
  - 7 commits, 2026-10-03 → 2026-10-06 (UTC+2).
  - Renamed from kurekizmo (`old-origin` remote).
  - The README describes three phases: PyQt6 GUI (~500MB) → headless daemon (~55MB) → cognitive memory.
- **Release:** v0.1.0, published 2026-10-06 23:30 (UTC+2). The tarball's SHA-256 `91c4cf1b…8911` is verified against the published asset.

## Claims & citations

| Claim | Source |
|-------|--------|
| Daemon, port 8790, ~333MB, summon methods, 24 tools | [[sources/index/src-20261008-ae52ff2-kureksistant-readme]] |
| Architecture, Muse Memory, Hermes sync, agents guide | [[sources/index/src-20261008-88302c2-kureksistant-agents]] |
| Re-cut release checksum (`a4085d73…`) | [[sources/index/src-20261008-f95e626-kureksistant-sha256sums-v0-1-0]] |
| Historical ~55MB claim (superseded) | [[sources/index/src-20261007-c1c7fe9-kureksistant-readme]] |
| Historical JARVIS-era agent guide (superseded) | [[sources/index/src-20261007-459dbb7-kureksistant-agents]] |
| Historical leaked v0.1.0 checksum (superseded) | [[sources/index/src-20261007-e1be179-kureksistant-sha256sums-v0-1-0]] |
| Commit history, rename | [[sources/index/src-20261007-2aa023e-kureksistant-git-log]] |
| v0.1.0 key leak, re-cut, new SHA-256 `a4085d73…1003` | [[artifacts/kureksistant/audit-2026-10-08]]; agent verification 2026-10-08 |
| Legacy GUI in `legacy/`, CI, SECURITY.md, `.env` settings | PR #2 `31d7e56` (https://github.com/nodaysidle/kureksistant/pull/2) |
| Daemon error, dream cycle, F821s, dependency alignment | Commit `d863922` (https://github.com/nodaysidle/kureksistant/commit/d863922) |

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[wiki/concepts/kureksistant-source-discrepancies]]
- [[_system/templates/catalog/kurekizmo]]
- [[artifacts/kureksistant/audit-2026-10-08]]
- [[sessions/2026-10-08-kureksistant-session]]

## Open questions

- Is the licence MIT or CC BY-NC 4.0? See [[wiki/concepts/kureksistant-source-discrepancies]].
- The ~55MB RAM figure is a project claim and was not measured.
- **Update 2026-10-08:** the RAM question is answered. The audit measured ~333MB RSS with faster-whisper loaded, and the docs were corrected in PR #3. The licence question was resolved on 2026-10-07 (CC BY-NC 4.0).
- Has the user revoked the old Gemini and OpenRouter keys? Unconfirmed.
