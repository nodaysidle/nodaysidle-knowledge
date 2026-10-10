---
type: wiki-note
note_kind: concept
topic_slug: kureksistant
status: active
created: 2026-10-07
updated: 2026-10-10
verified: 2026-10-10T07:35:00+02:00
verified_previous_v020: 2026-10-10T06:11:00+02:00
verified_previous_pr5: 2026-10-10T06:10:00+02:00
verified_previous_pr5: 2026-10-10T05:51:00+02:00
verified_previous_pr4: 2026-10-10T05:40:00+02:00
verified_previous: 2026-10-10T05:11:00+02:00
tags:
  - wiki
  - kureksistant
---

# Kureksistant (Kurek) — overview

## Summary

Kureksistant is a headless Python voice-assistant daemon on `127.0.0.1:8790` for Arch Linux/Hyprland, with a secondary macOS menu-bar path. It is summoned by middle-click or the Fn key. Reasoning uses DeepSeek-Flash, voice uses xAI Grok TTS ("Sol"), and screen vision uses Gemini Flash. v0.2.0 (2026-10-10) ships as an unsigned Linux tarball; v0.1.0 is superseded. Local folder: `kurekizmo`.

## Status as of 2026-10-08 03:32 UTC+2 (superseded; see "Current status (2026-10-10 06:10 UTC+2)" below)

Newer facts here take precedence over the older figures in Details (~55MB, the `91c4cf1b…` checksum).

- **Repo:** public. `main` = `d863922` at the time. *(Stale: `main` = `e91a14c` since 2026-10-10 06:05:56, tagged v0.2.0.)* Audit grade **C−**: [[artifacts/kureksistant/audit-2026-10-08]].
- **Lineage:** `kurekizmo` was made private on GitHub; `kureksistant` was created as the public repository specifically incorporating TypeSafe Jev cognitive memory triage and deep daemon optimizations (~333MB RAM, faster-whisper, 24 tools). ⚠️ *(2026-10-10 05:11) 24 tools is **stale/unverified**: `main` has 27 `actions/*.py` modules. ✅ *Corrected 2026-10-10 06:11: 24 is right (journal "Loaded 24 actions").* ~333MB is the 2026-10-08 measurement, now capped at 250M.* ✅ *Resolved 2026-10-10 06:10: **24 tools verified** (24 unique module-level `TOOL` dicts; 4 of the 28 `actions/*.py` files are helpers). RAM is now documented as **~450MB peak observed** with faster-whisper; the unit is `MemoryHigh=512M` / `MemoryMax=600M` (PR #6 `f1d7920`).*
- **Done 2026-10-08 (Execution Operator / Grok Bot, Cursor cloud agent `bc-e01c8f24-b3e6-5c91-afb6-bee6dd7d455c`):**
  - **Key leak fixed in the release:** the public v0.1.0 tarball had shipped `config/api_keys.json` with likely-live Gemini and OpenRouter keys. The asset was re-cut on the same tag without secrets. New SHA-256: `a4085d73ae8764f6b9034e3caabd4c4278f345d074f7909dad171dea63861003`. `SHA256SUMS.txt` was replaced, and the new tarball contains 0 `api_keys.json` and 0 `.env`. The user's local `config/api_keys.json` was left untouched on purpose.
  - **[PR #2](https://github.com/nodaysidle/kureksistant/pull/2)** (squash, `31d7e56`):
    - The headless daemon is the only entrypoint. The legacy PyQt6 JARVIS GUI (`main.py`, `ui.py`, `dashboard/`, `plugins/`, `jarvis.ico`) moved to `legacy/`.
    - Added `SECURITY.md`, `NOTICE` and an SPDX `CC-BY-NC-4.0` `LICENSE`. GitHub may still show the licence as "Other".
    - Personal and machine-specific hardcodes became `.env` settings: `KUREK_USER_NAME`, `HERMES_PROFILE`, `HERMES_MEMORIES_DIR`, `INPUT_DEVICE`, `KUREK_PROJECT_DIR`.
    - Added `.github/workflows/ci.yml` (scoped ruff plus the daemon `/status` smoke test in `tests/test_daemon_smoke.py`).
    - Added a deny-list gate in `scripts/package_release.sh` that fails the build if a key file is packaged.
  - **[PR #3](https://github.com/nodaysidle/kureksistant/pull/3)** (squash, `52d009b`): the README, RAM badge, `AGENTS.md` and daemon docstring now say ~333MB RAM (with the default faster-whisper) and 24 tools. They said ~55MB and 28.
  - **Set by the user on GitHub:** description (~333MB) and topics `ai-assistant`, `deepseek`, `hyprland`, `linux`, `macos`, `personal-assistant`, `python`, `voice-assistant`. The Cursor GitHub app lacks admin permission (403). ⚠️ *(2026-10-10 05:11) The live topic is misspelled `ai-assitant`. ✅ *Fixed 2026-10-10 06:11.** ✅ *Resolved 2026-10-10 06:10: live topic is `ai-assistant`.*
- **Done 2026-10-10 (Antigravity — Arch Linux / Hyprland Performance & IPC Overhaul):**
  - **Unix Domain Socket & C Trigger Client:** Implemented `$XDG_RUNTIME_DIR/kurek.sock` asynchronous UDS server alongside HTTP `:8790`. Added compiled C binary (`bin/kurek-trigger.c` → `~/.local/bin/kurek-trigger`), cutting middle-click summon latency from ~50ms (bash/pgrep/curl) to **<2ms**, with auto-spawn fallback. Emits real-time state events over UDS for Waybar/AGS status synchronization. ⚠️ *(2026-10-10 05:11) UDS and C trigger **verified** (`kurek_daemon.py:816-842`, `bin/kurek-trigger.c`). The **<2ms** figure is **unbacked** (no benchmark) and conflicts with the repo's own **<1ms**. See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].* ✅ *Resolved 2026-10-10 06:10: measured **~0.8ms median** (`scripts/bench_trigger.py`, mock daemon; CI on `e91a14c`: 0.840ms median, 1.061ms p95, 200 runs). Docs now say ~0.8ms; the <1ms/<2ms wording is gone. "Asynchronous" is loose: the server is one thread per connection.*
  - **Sub-400ms Streaming Voice Pipeline:** Replaced full-response blocking with sentence-buffered streaming (`core/llm_client.py:stream_deepseek_sentences`). Chunks delimited by `[.!?\n]` immediately dispatch to xAI Grok Cloud TTS (**Sol** voice), dropping first-syllable speech latency from ~3.5s to **~350–500ms**. ⚠️ *(2026-10-10 05:11) Sentence streaming **verified** (`core/llm_client.py:869`, daemon `:506-557`; the split rule is `(?<=[.!?])\s+`, not `[.!?\n]`). xAI TTS is one blocking request per sentence. **~350–500ms / sub-400ms is unbacked** (no timing data), and the range contradicts the title.* ✅ *Resolved 2026-10-10 06:10: "sub-400ms" removed from docs and the v0.2.0 notes; PR #6 `f1d7920` adds opt-in timing logs (`KUREK_TIMING`) and a safer sentence splitter. First-audio latency is still unmeasured, so no figure is claimed.*
  - **Persistent PipeWire mpv Sink (`core/mpv_sink.py`):** Pre-warms an idle `mpv` background process on PipeWire with IPC socket `$XDG_RUNTIME_DIR/kurek_mpv.sock`. Streams audio chunks out of `/dev/shm` (POSIX RAM tmpfs) with zero NVMe disk writes and enables instant barge-in interrupt (`{"command":["stop"]}`) on middle-click. ✅ *(2026-10-10 05:11) Verified in code and live socket; barge-in not exercised. Falls back from `/dev/shm` to the runtime dir.*
  - **Event-Driven Hyprland Watcher (`core/hyprland_watcher.py`):** Connects to `$XDG_RUNTIME_DIR/hypr/<inst>/.socket2.sock`. Caches active window class, title, workspace, and geometry in RAM (O(1) lookup), completely eliminating `hyprctl activewindow -j` CLI subprocess spawning. ⚠️ *(2026-10-10 05:11) Event-driven watcher **verified**, but "completely eliminating" `hyprctl` is **unbacked**: it still seeds state with `hyprctl` (`core/hyprland_watcher.py:85-108`), and `actions/screen_vision.py:63-65` falls back to it.* ✅ *Resolved 2026-10-10 06:10: PR #6 `f1d7920` parses events and fetches geometry lazily (one seed plus one `hyprctl` call per vision request, no longer one per focus change). "Eliminates hyprctl" removed from docs and notes.*
  - **Zero-Disk Active Window Vision (`actions/screen_vision.py`):** Streams active window geometry via `grim -g "<coords>" -t jpeg -q 80 -` directly into `io.BytesIO` in RAM. Zero temporary file writes and sub-60ms capture speed. ⚠️ *(2026-10-10 05:11) The Linux in-memory path is **verified** (`actions/screen_vision.py:80-99`); **sub-60ms is unbacked**. The macOS fallback writes `/tmp`.* *(2026-10-10 06:10: the sub-60ms figure is no longer claimed in docs or the v0.2.0 notes.)*
  - **Native systemd User Service:** Created `~/.config/systemd/user/kurek.service` targeting `graphical-session.target` with journald logging and a strict resource envelope (`MemoryHigh=250M`, `MemoryMax=450M`). ⚠️ **Conflict (2026-10-10 05:11):** the unit is verified and active, but `MemoryHigh=250M` sits below the documented ~333MB. Live: 237 MiB current, 251 MiB peak, swapping (journal "239.7M memory swap peak"). ✅ *Resolved 2026-10-10 05:40: [PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f` set 400M/600M; live 345 MiB, swap ~0.* *Then 450M/600M in PR #5 `e1d3575`, and **512M/600M** in PR #6 `f1d7920` (current at v0.2.0).*
  - **Hyprland Bindings Updated:** Updated `~/.config/hypr/bindings.lua` mouse:274 and SUPER+mouse:274 to call `/home/arch/.local/bin/kurek-trigger toggle` directly. ✅ *Verified locally (`bindings.lua:39-40`).*
  - **Knowledge Vault Integration (`actions/vault_knowledge.py`):** Added tool #25 connecting Kurek directly to the `nodaysidle-knowledge` Obsidian vault. Supports `list_projects` (portfolio overview from MOC), `read` (concept notes, PRDs, roadmaps, X promo strategy), `search` (ripgrep/regex with YAML frontmatter stripping), and `add_inbox` (voice idea capture to `inbox/YYYY-MM-DD-<slug>.md`). Grounded via compact ~150-token portfolio anchor in `kurek_daemon.py` without prompt bloat.
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
  - 7 commits, 2026-10-03 → 2026-10-06 (UTC+2). *(Stale: `main` = `e91a14c` as of 2026-10-10 06:05, after PRs #4–#7.)*
  - Renamed from kurekizmo (`old-origin` remote).
  - The README describes three phases: PyQt6 GUI (~500MB) → headless daemon (~55MB) → cognitive memory.
- **Release:** v0.1.0, published 2026-10-06 23:30 (UTC+2).*(Superseded 2026-10-10 06:11: [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0) is Latest, SHA-256 `6b856030…19da`.)*  The tarball's SHA-256 `91c4cf1b…8911` is verified against the published asset. *(Superseded: re-cut `a4085d73…1003` on 2026-10-08; **v0.2.0** published 2026-10-10 06:07, SHA-256 `6b856030…19da`, now Latest.)*

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
| UDS subscribers, memory envelope, dream cycle, stream errors | PR #4 `c83f46f` (https://github.com/nodaysidle/kureksistant/pull/4) |
| Portable paths, UDS peer auth, hardened C trigger | PR #5 `e1d3575` (https://github.com/nodaysidle/kureksistant/pull/5) |
| Lazy Hyprland geometry, timing logs, bench, splitter, docs, 512M | PR #6 `f1d7920` (https://github.com/nodaysidle/kureksistant/pull/6) |
| v0.2.0 bump, CHANGELOG | PR #7 `e91a14c` (https://github.com/nodaysidle/kureksistant/pull/7) |
| v0.2.0 release, SHA-256 `6b856030…19da`, ~0.8ms trigger, ~450MB peak | https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0; agent verification 2026-10-10 06:10 |

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

## Current status (2026-10-10 05:11 UTC+2): code check of the 10-10 overhaul

Checked by Grok Bot (ATLAS) against `main` @ `02382f2` and the running service. Full table: [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].

- **Verified:** UDS server + state events; the C trigger (built by `install_linux.sh`); sentence-buffered streaming to xAI TTS; the persistent mpv sink on `/dev/shm`; the socket2 Hyprland watcher; in-memory `grim` capture; the systemd unit (active since 03:33:30); local bindings.
- **Unbacked:**
  - `<2ms` trigger: the repo says `<1ms`, and nobody has measured it.
  - `~350–500ms` / "sub-400ms" first audio.
  - `sub-60ms` capture.
  - "completely eliminating `hyprctl`" (it is still used to seed state and as a fallback).
  - There are no benchmarks; CI runs only the daemon smoke test (`lint-and-smoke` passed).
- **Stale:**
  - 24 tools (27 modules on `main`);
  - the v0.1.0 release notes (~55MB, 20 actions);
  - the commit history count;
  - the topic typo `ai-assitant`.
- **Conflict:** `MemoryHigh=250M` versus ~333MB with Whisper. The live daemon sits at the cap and swaps.
- **Unchanged and verified:** v0.1.0 is the only release (SHA-256 `a4085d73…1003`); the licence is CC BY-NC 4.0 (FatihMakes JARVIS + NODAYSIDLE, GitHub shows "Other"); paid DeepSeek + xAI keys are required; 0 open issues.
- **Links:** `8e80480` committed only this note. 10 of its 12 wikilinks point at untracked files, so they are broken on GitHub. There was no audit entry or session note for 10-10; both were added now, uncommitted.

## Current status (2026-10-10 05:40 UTC+2): PR #4 fixes merged

- ✅ **Fixed in [PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f`** (squash-merged 05:38:17 CEST; CI `lint-and-smoke` green; CI now runs `pytest -q tests/`). Each fix has a test:
  1. **UDS subscribers stay open** and receive broadcasts. The finally block no longer closes them (`kurek_daemon.py`; `tests/test_uds_subscribe.py`). **State events are working:** a live read-only subscribe at 05:40 got `{"event": "state", "state": "idle"}` and the socket stayed open.
  2. **Memory envelope:** `MemoryHigh=400M` / `MemoryMax=600M` (`desktop/kurek.service`; `tests/test_systemd_memory_envelope.py`). ✅ **The MemoryHigh/swap conflict is resolved.** The installed unit has the new limits, and the service has been active since 05:38:49. **Live 05:40: 345 MiB current (matching Execution Operator's ~345MiB), 402 MiB peak, 12 KiB swap.** Before this, 251.7M peak / 95.3M swap peak under the 250M cap. The peak slightly exceeds MemoryHigh, so it is worth watching.
  3. **Dream cycle:** responses are normalised via `text_from_llm_response` for str, dict and None (`core/dream_cycle.py`; `tests/test_dream_cycle_response.py`).
  4. **No more stuck THINKING:** stream errors and uncaught errors now end in IDLE (`core/llm_client.py` yields `error` events; `kurek_daemon.py` finally → IDLE; `tests/test_stream_errors.py`).
  8. **Honest failure speech:** "I couldn't reach DeepSeek right now." / "I didn't get a response from DeepSeek." replace the fake "All set." (the tests assert no "All set."). "All set." remains only for successful tool runs with no spoken output.
- Local clone `kurekizmo` = `c83f46f`, clean.
- **Still open (owner decision):**
  - **PR B (not yet approved):** hardcoded paths; installer system dependencies; socket authentication and the `/tmp` socket fallback; JSON escaping and the timeout in the C trigger. ✅ **Closed 2026-10-10 05:51 by [PR #5](https://github.com/nodaysidle/kureksistant/pull/5) `e1d3575`.**
  - **PR C (optional):** `hyprctl` is spawned on every focus change; the latency claims (<1/<2ms, sub-400ms, 60ms) are still unmeasured; cleanups. ✅ **Closed 2026-10-10 06:11 by [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920`** (merged by [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c`).
  - **v0.2.0** has not been cut (v0.1.0 is still the only release). ✅ **Done 2026-10-10 06:11:** [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0) released (`e91a14c`).
- See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].

## Current status (2026-10-10 05:51 UTC+2): PR #5 fixes merged

- ✅ **Fixed in [PR #5](https://github.com/nodaysidle/kureksistant/pull/5) `e1d3575`** (squash-merged 05:49:30 CEST; CI `lint-and-smoke` green. CI now also compiles the trigger with `-Werror` and runs shellcheck on the installer). New tests: `tests/test_installer_templating.py`, `tests/test_uds_security.py`, `tests/test_trigger_json_escape.py`.
  - **5. Hardcoded paths:** the installer templates `@KUREK_DIR@` into the unit (`install_linux.sh:19`) and writes `~/.config/kurek/install_path` (`:78-79`). The C trigger reads that file (`bin/kurek-trigger.c:89-102`) and polls the socket (`:174-182`, 100ms steps).
  - **6. Installer:** checks the pacman packages `mpv grim wl-clipboard libnotify gcc` (`:24-35`), with a binary check on non-Arch systems. It exits without gcc (`:46-51`), always runs pip (`:67-69`) and installs Playwright Chromium (`:73`). It is idempotent (`mkdir -p`, overwrite); that is asserted by the test and was not re-run on the machine.
  - **9. Socket auth:** the UDS socket is 0600 (`umask 0o177` + `chmod`, `kurek_daemon.py:948-955`), with an `SO_PEERCRED` same-UID check (`:912-931`). The `/tmp` fallback is gone (`:891`; a private 0700 dir is used if XDG is unset).
  - **10. Trigger:** `json_escape` (`:26`); 500ms send/receive timeouts (`IO_TIMEOUT_USEC 500000`, `SO_RCVTIMEO/SO_SNDTIMEO`). Note: the total connect poll is `CONNECT_TIMEOUT_MS 5000`, not 500ms.
  - **Memory:** `MemoryHigh=450M` / `MemoryMax=600M` (was 400M/600M in PR #4).
- **Machine, read-only 05:51 (trigger not toggled):**
  - local repo `e1d3575`, clean;
  - installed unit templated (no `@KUREK_DIR@` left, paths are `/home/arch/dev/nodaysidle/kurekizmo`), 450M/600M;
  - service active since 05:50:18;
  - **RAM: 280 MiB current, 452 MiB peak, 24 KiB swap** (Execution Operator reported ~373MiB, presumably at another moment; the peak is slightly above MemoryHigh);
  - `kurek.sock` mode 600 (journal: "Listening … (0600)");
  - a read-only subscribe got `{"event": "state", "state": "idle"}` and stayed open;
  - `~/.config/kurek/install_path` = `/home/arch/dev/nodaysidle/kurekizmo`;
  - `config/api_keys.json` exists (mtime 2026-09-10 21:22, contents not read).
- **Still open, neither approved:**
  - **PR C:** `hyprctl` spawned on every focus change; unmeasured latency claims (<1/<2ms, sub-400ms, 60ms); cleanups. ✅ **Closed 2026-10-10 06:11 by [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920`** (merged by [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c`). ✅ *Closed 2026-10-10 06:02 by PR #6 `f1d7920`.*
  - **v0.2.0:** not cut. ✅ **Done 2026-10-10 06:11:** [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0) released (`e91a14c`). ✅ *Published 2026-10-10 06:07; see below.*
- See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].

## Current status (2026-10-10 06:10 UTC+2): v0.2.0 released

- **Repo:** `main` = `e91a14c` (PR #7, squash-merged 06:05:56 CEST). CI `lint-and-smoke` green on `e91a14c` (run 38022871050).
- **Merged today:** [PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f` (05:38) · [PR #5](https://github.com/nodaysidle/kureksistant/pull/5) `e1d3575` (05:49) · [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920` (06:02) · [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c` (06:05).
- **Release [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0)** (published 06:07:28 CEST, Latest; tag at `e91a14c`; v0.1.0 untouched):
  - `kureksistant-v0.2.0-linux-x86_64.tar.gz`: 942,506 bytes, SHA-256 `6b85603070959836f1fecd51bd3b2450d8bc9cbefb6ed0af240f1847e6e619da`.
  - `SHA256SUMS.txt`: 106 bytes.
  - Built by Grok Bot with `VERSION=0.2.0 scripts/package_release.sh` from a shallow checkout of `e91a14c` (deny-list OK). Re-downloaded and `sha256sum -c` OK. 105 files; only `.env.example` and `config/api_keys.json.example`; no memories or dream journals; gitleaks, trufflehog and pattern scans clean.
  - The cloud agent's earlier local build was 940,761 bytes / `d38a3e15…db89`. The difference is expected, since the tar.gz is not reproducible byte-for-byte.
- **Corrected claims (docs and release notes):** no "sub-400ms"; no "eliminates hyprctl"; trigger **~0.8ms median** measured; **~450MB peak** RAM observed with faster-whisper; **24 tools**; `MemoryHigh=512M` / `MemoryMax=600M`; topic `ai-assistant` fixed; licence CC BY-NC 4.0 (derived from FatihMakes' JARVIS).
- **Still open:** first-audio and capture latency not measured (no figure claimed); the HTTP `:8790` control API has no auth (the UDS socket is now 0600 + peer UID); `exec` in `actions/desktop.py`; legacy ruff/mypy debt; key revocation unconfirmed.

## Current status (2026-10-10 06:11 UTC+2): v0.2.0 released

- ✅ **Released [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0)** (Latest, published 06:07:28 CEST, target `e91a14c`).
  - **Asset:** `kureksistant-v0.2.0-linux-x86_64.tar.gz`, 942,506 bytes, SHA-256 `6b85603070959836f1fecd51bd3b2450d8bc9cbefb6ed0af240f1847e6e619da` (GitHub digest; it matches the release notes). There is also a `SHA256SUMS.txt` (106 bytes).
  - **Release notes:** they summarise #4–#6 and the Oct 8 fixes; DeepSeek + xAI keys are required (not usable offline); ~450MB peak RAM observed; 24 tools; trigger ~0.8ms median (`scripts/bench_trigger.py`, mock daemon; CI 0.84ms median / 1.06ms p95, 200 runs); CC BY-NC 4.0 (FatihMakes JARVIS).
- ✅ **[PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920`** (merged 06:02:40 CEST, CI green) closes PR C:
  - **Hyprland watcher:** event-parsed with lazy geometry. Focus/move events only mark geometry as stale and no longer spawn `hyprctl`. It now runs one seed fetch plus one fetch per vision request (`core/hyprland_watcher.py:7-10, 92-113`; `tests/test_hyprland_watcher.py`).
  - **Latency wording:** opt-in `KUREK_TIMING=1` logs (`core/timing.py`) and `scripts/bench_trigger.py`. README/AGENTS now give only "~0.8ms median (mock daemon)"; the <1/<2ms, sub-400ms and 60ms claims are gone.
  - **Cleanups:** safer sentence splitter (`tests/test_sentence_splitter.py`); `MemoryHigh=512M` / `MemoryMax=600M`.
- ✅ **[PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c`** (merged 06:05:56 CEST, CI green): `CHANGELOG.md`, version bumps, AGENTS "Release: v0.2.0".
- ✅ **Stale facts fixed:**
  - **Topic:** `ai-assistant` is now correct on GitHub (repo settings; no commit).
  - **v0.1.0-era figures (~55MB / ~333MB):** replaced in README/AGENTS by "~450MB peak observed" (`f1d7920`).
  - **Tool count:** **24 is correct** and **corrects my earlier "stale" flag**. The live journal says "Loaded 24 actions" (06:09:29, 06:10:39); the 27 `actions/*.py` files include non-tool helper modules.
  - **Release notes:** the v0.2.0 notes are accurate. ⚠️ The **v0.1.0** notes still say "~55MB" and "20 built-in actions"; that release is superseded but not edited.
- **Machine, read-only 06:10 (trigger not toggled):**
  - local repo `e91a14c` (`git describe` = `v0.2.0`), clean;
  - unit 512M/600M;
  - service active, **restarted at 06:10:39**, just before the check;
  - **313 MiB current, 396 MiB peak, 0 swap**. This is right after a restart, so it is not comparable with Execution Operator's ~436MiB or the ~450MB peak in the release notes;
  - socket mode 600; a read-only subscribe got `{"event": "state", "state": "idle"}` and stayed open.
- **Still open (owner not yet decided):**
  - ⚠️ **Security risk:** the HTTP API on `127.0.0.1:8790` has no authentication (`kurek_daemon.py:1066`; only the UDS path checks peers). Any local process can drive it.
  - ⚠️ **Security risk:** `actions/desktop.py:97` runs `exec(compile(code, …))` on model-generated code.
  - **Not measured:** end-to-end first-audio and screen-capture latency (`KUREK_TIMING=1` logs exist, but no published figures).
- See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].

## Current status (2026-10-10 07:35 UTC+2): showcase card 06, real demo GIF, launch date

- **Showcase:** card 06 on [[_system/templates/catalog/nodaysidle-apps]] (https://nodaysidle-apps.vercel.app/#kurek), [nodaysidle-apps PR #3](https://github.com/nodaysidle/nodaysidle-apps/pull/3) `46251cb`. It has the voiced clip, the CC BY-NC 4.0 FatihMakes JARVIS credit and a note that keys are required; 14/14 links return 302.
- **Real demo GIF:** [kureksistant PR #8](https://github.com/nodaysidle/kureksistant/pull/8) `022d4be` (merged 06:30:45 CEST, not ~07:33) replaces the mock-up `docs/demo.gif` (it showed ~55MB / 20 tools / <100ms) with REEL's v0.2.0 GIF (800×800, ~2.7MB). It is byte-identical to `/workspace/clips/kurek/kurek.gif`; the hashes match. `main` = `022d4be`.
- **Launch on X: Wed 21 Oct 2026, 15:15 Europe/Ljubljana**, as reported by Execution Operator. ⚠️ **Conflict:** REACH's plan file on the box (`/workspace/reach/x-promo-strategy-2026-10-12.md`, mtime 2026-10-09 17:30) has Wed 21 Oct 15:15 as "Browser build thread (or the poll winner)". In that file Kurek appears only as a no-link recap on Wed 14 Oct 20:30 and a re-feature on Thu 29 Oct citing stale v0.1.0 figures (~333MB, `docs/demo.gif`). REACH needs to confirm or update the plan.
- Still open: ⚠️ unauthenticated HTTP :8790; ⚠️ `actions/desktop.py` exec(); end-to-end latency not measured.
