---
type: wiki-note
note_kind: concept
topic_slug: kureksistant
status: active
created: 2026-10-07
updated: 2026-10-13
verified: 2026-10-13T23:51:52+02:00
verified_previous_v021: 2026-10-13T23:51:52+02:00
verified_previous_v020_atlas: 2026-10-10T16:28:00+02:00
verified_previous_v020: 2026-10-10T06:11:00+02:00
verified_previous_v020_check: 2026-10-10T06:10:00+02:00
verified_previous_pr5: 2026-10-10T05:51:00+02:00
verified_previous_pr4: 2026-10-10T05:40:00+02:00
verified_previous: 2026-10-10T05:11:00+02:00
tags:
  - wiki
  - kureksistant
---

# Kureksistant (Kurek) — overview

## Summary

Kureksistant is a headless Python voice-assistant daemon on `127.0.0.1:8790` for Arch Linux/Hyprland, with a secondary macOS menu-bar path. It is summoned by middle-click or the Fn key. Reasoning uses DeepSeek-Flash, voice uses xAI Grok TTS ("Sol"), and screen vision uses Gemini Flash. v0.2.0 (2026-10-10) ships as an unsigned Linux tarball; v0.1.0 is superseded. *(Update 2026-10-14: **v0.2.1** is Latest, target `3761c78`; v0.2.0 superseded.)* Local folder: `kurekizmo`.

**Positioning (2026-10-12 05:48):** Kurek has evolved from a desktop voice assistant into **voice control of the PC**, including **remotely from an Android app over Tailscale**. Verified 2026-10-12 (per Execution Operator): phone over Tailscale got HTTP 200 SSE with a spoken reply; a wrong token gets 401; the daemon binds 127.0.0.1 plus the Tailscale interface only (remote is opt-in via KUREK_REMOTE_BIND=tailscale); hardening in PR #11 `822966c`. The Android APK is **not published** as a release yet. *(ATLAS 2026-10-15 13:55 UTC: **that sentence is superseded — the APK IS published, as a debug build.** [v0.2.1](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.1) (2026-10-14, target `3761c78`) attaches a **debug-signed** Kurek Remote APK to its release assets; first-hand at the local checkout `09e3c7d` the README says so and tells you to uninstall any older copy first (`kurekizmo` `README.md:47`, `:188`; badge `:14`). There is still **no direct APK link** anywhere — not in the README, not on the apps card (the live `#kurek` card carries no `.apk` link) — so "don't link the APK" stands. State it as "a debug APK attached to the v0.2.1 release", never as a store or production release.)*

## Status as of 2026-10-08 03:32 UTC+2 (superseded; see "Current status (2026-10-10 06:10 UTC+2)" below)

Newer facts here take precedence over the older figures in Details (~55MB, the `91c4cf1b…` checksum).

- **Repo:** public. `main` = `d863922` at the time. *(Stale: `main` = `e91a14c` since 2026-10-10 06:05:56, tagged v0.2.0.)* Audit grade **C−**: [[artifacts/kureksistant/audit-2026-10-08]].
- **Lineage:** `kurekizmo` was made private on GitHub; `kureksistant` was created as the public repository specifically incorporating TypeSafe Jev cognitive memory triage and deep daemon optimizations (~333MB RAM, faster-whisper, 24 tools). ⚠️ *(2026-10-10 05:11) 24 tools is **stale/unverified**: `main` has 27 `actions/*.py` modules. ✅ *Corrected 2026-10-10 06:11: 24 is right (journal "Loaded 24 actions").* ~333MB is the 2026-10-08 measurement, now capped at 250M.* ✅ *Resolved 2026-10-10 06:10: **24 tools verified** (24 unique module-level `TOOL` dicts; 4 of the 28 `actions/*.py` files are helpers). ✅ *Updated 2026-10-10 16:28: **25 tools** since `6137128` (vault_knowledge); journal "Loaded 25 actions".* RAM is now documented as **~450MB peak observed** with faster-whisper; the unit is `MemoryHigh=512M` / `MemoryMax=600M` (PR #6 `f1d7920`).*
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
  - **Knowledge Vault Integration (`actions/vault_knowledge.py`):** Added tool #25 connecting Kurek directly to the `nodaysidle-knowledge` Obsidian vault. Supports `list_projects` (portfolio overview from MOC), `read` (concept notes, PRDs, roadmaps, X promo strategy), `search` (ripgrep/regex with YAML frontmatter stripping), and `add_inbox` (voice idea capture to `inbox/YYYY-MM-DD-<slug>.md`). Grounded via compact ~150-token portfolio anchor in `kurek_daemon.py` without prompt bloat. ⚠️ *(2026-10-10 16:28) The ~150-token / no-bloat claim is **unmeasured**. Tool count is now **25** (`6137128` adds `actions/vault_knowledge.py`; README/AGENTS say 25; journal 16:27 "Loaded 25 actions").*
  - **Sub-100ms Screen Context Trigger via Microsoft-Decision-1 (2026-10-10 20:55):** Updated `_check_auto_screen_context` in `kurek_daemon.py` to route `needs_screen` snap judgments through Microsoft-Decision-1 via OpenRouter `/api/alpha/decisions` (`sk-or-v1-...`). Cuts synchronous blocking trigger latency from ~240ms (Jev) down to **~85ms P50**, saving ~155ms of lag on every spoken summon before voice synthesis begins. Retains TypeSafe Jev as fallback for screen vision, and keeps Jev permanently for asynchronous Muse memory consolidation and safety boundary hoisting to `~/ALIGNMENT_SYNTHESIS.md`. See [[wiki/concepts/decision-models-microsoft-vs-jev]]. *(ATLAS 2026-10-15 13:38 UTC: the **latency figures in this line are unqualified — do not quote them.** 85 ms and 240 ms are the two models' quoted P50 figures, as recorded in the 2026-10-10 audit note (`_audit/log.md` line 504), and the "~155ms saved" is that note's own assertion (line 509, "live verified in daemon venv"); **no bench script, CI run or artifact backs a Kurek-level number.** Same class as the "~0.8ms trigger" and "<0.1s" caveats — no latency claims.)*
- **Done 2026-10-15 (Antigravity — Operative Code Access: `codebase` & `run` Tools, commit `ab1420a`):**
  - **Tool #26: `actions/codebase.py`:** Ground-truth source tree inspection across allowed project roots (`~/.config/kurek/codebase_roots`, defaulting to `~/Projects` and `~/dev`). Supports `search` (live ripgrep with context lines — ⚠️ the "<0.1s latency" figure that stood here until 2026-10-15 13:32 UTC has been **removed**: it is **unmeasured and unqualified** — no bench script, CI run or artifact backs a `codebase`-tool latency — and must not be quoted (no-latency-claims rule; same class as the "~0.8ms trigger" and "~85 ms" figures)), `tree` (filtered ASCII directory tree), `read` (line-range bounded reader), `find` (fast glob/extension locator), `outline` (AST symbol maps for Rust, TypeScript, Python, Go, Swift), `index` (per-repo snapshot index), and `status` (branch, dirty status, commit, and index freshness). Strictly read-only; skips binary files; safely caps unbounded output.
  - **Tool #27: `actions/run.py`:** Sandboxed, auditable command runner with strict allowlist. Supports `exec`, `read`, `list`, `cancel`. Permits read-oriented inspection (`git status/diff/log/show`, `rg`, `ls`, `cat`, `head`, `tail`, `wc`, `find`, `stat`, `--version`) and declared project build/test targets (`cargo check/test/build/clippy`, `pytest`, `npm test`, `make`). Permanently blocks destructive operations (`rm`, `git push`, `git reset --hard`, `curl|sh`, package installs) and shell chaining (`&&`, `|`, `;`). Enforces non-interactive execution (`GIT_PAGER=cat`, `CI=1`), timeouts, output truncation, secret/token redaction, and append-only audit logging to `~/.local/state/kurek/run_audit.log`.
  - **Daemon & Remote Protection:** Auto-discovery now loads **27 active tools**. `run` is added to `REMOTE_BLOCKED_EXEC_TOOLS` in `kurek_daemon.py`, protected unless `KUREK_REMOTE_ALLOW_EXEC=1`.
  - **Verified live over Tailscale:** Tested via owner's Android phone (`mi-10t`, phone's Tailscale IP); verified prompt correctly inspected working tree state and cited the new tools. Unit test suites added in `tests/test_codebase.py` (12 tests) and `tests/test_run.py` (10 tests); full test suite passes (168 passed, 1 skipped).
- **State corrected 2026-10-15 12:45 UTC (ATLAS):** `ab1420a` reached `main` via [kureksistant PR #24](https://github.com/nodaysidle/kureksistant/pull/24), **merged** 2026-10-15T04:33:03Z (squash `fc94620`); `origin/main` = local main = `09e3c7d`, and v0.2.1 is still the Latest release (27 tools on `main`). `KUREK_REMOTE_ALLOW_EXEC=1` stays ON by the owner's 02:33 decision. The local tree now also carries **uncommitted** `actions/run.py`, `core/prompt.txt` and `kurek_daemon.py` plus untracked `.commandcode/` — unreviewed, not described anywhere here.
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
  - The README describes four phases: PyQt6 GUI (~500MB) → headless daemon (~55MB) → cognitive memory → Android Remote Pocket Jarvis.
- **Android Remote Companion:** Native Android APK (`android/`) with voice dictation, live Server-Sent Events (SSE) streaming on `/remote/prompt`, and Bearer token security (`KUREK_REMOTE_TOKEN`). Enables untethered workstation control over home Wi-Fi and Tailscale.
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
| v0.2.0 release, SHA-256 `6b856030…19da`, ~0.8ms trigger, ~450MB peak | https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0; agent verification 2026-10-10 06:10. *(ATLAS 2026-10-15 13:55 UTC: this is the v0.2.0-era row. Its "~0.8ms trigger" is the **mock-daemon bench** figure — `scripts/bench_trigger.py` times `bin/kurek-trigger` against a mock UDS daemon — and CI **does** print its median/p95 as an **informational, non-gating** step (`--runs 200`, soft-fail ignored: `.github/workflows/ci.yml:60-64`; `CHANGELOG.md:64`). Machine-dependent, **not** end-to-end latency, never for public copy. "~450MB peak" stands only as observed.)* |

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
  - *(Historical at 2026-10-10 05:11 UTC+2, commit `02382f2`; superseded 51 minutes later by PR #6 `f1d7920`.)* There are no benchmarks; CI runs only the daemon smoke test (`lint-and-smoke` passed). Current CI also runs `bench_trigger.py` as an informational, non-gating mock-daemon benchmark and runs the test suite; it is not end-to-end latency, and its figures are not public-copy claims.
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
- **Corrected claims (docs and release notes):** no "sub-400ms"; no "eliminates hyprctl"; trigger **~0.8ms median** measured; **~450MB peak** RAM observed with faster-whisper; **24 tools**; `MemoryHigh=512M` / `MemoryMax=600M`; topic `ai-assistant` fixed; licence CC BY-NC 4.0 (derived from FatihMakes' JARVIS). *(ATLAS 2026-10-15 13:55 UTC: **qualify the two figures and the count.** "~0.8ms median" is the **mock-daemon** bench (`scripts/bench_trigger.py` against a mock UDS daemon); CI prints it as an **informational, non-gating** step (`--runs 200`, soft-fail ignored: `.github/workflows/ci.yml:60-64`). It is machine-dependent, **not** end-to-end latency, must not be quoted in public copy — and it is *not* "never recorded by CI". "~450MB peak" is observed only. "24 tools" is superseded: the v0.2.1 release and the live card say **25** (27 on `main`).)*
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
- **Launch on X: Wed 21 Oct 2026, 15:15 Europe/Ljubljana**, as reported by Execution Operator. ⚠️ **Conflict:** REACH's plan file on the box (`/workspace/reach/x-promo-strategy-2026-10-12.md`, mtime 2026-10-09 17:30) has Wed 21 Oct 15:15 as "Browser build thread (or the poll winner)". In that file Kurek appears only as a no-link recap on Wed 14 Oct 20:30 and a re-feature on Thu 29 Oct citing stale v0.1.0 figures (~333MB, `docs/demo.gif`). REACH needs to confirm or update the plan. ✅ *Resolved 2026-10-10 16:28: REACH updated [[wiki/concepts/x-promo-strategy-2026-10-12]]: Wed 21 Oct = Kurek v0.2.0 launch, Thu 29 = poll-winner thread, v0.2.0 facts, six-app roundup.*
- Still open: ⚠️ unauthenticated HTTP :8790; ⚠️ `actions/desktop.py` exec(); end-to-end latency not measured.

## Current status (2026-10-10 16:28 UTC+2): vault_knowledge tool, PR #9

- **Vault note commit `5477ef5`** (owner, 12:36) added the Knowledge Vault Integration bullet (tool #25). Audit and session entries were added afterwards (2026-10-10 16:28).
- **Tools: 25** (`6137128` adds `actions/vault_knowledge.py`; README/AGENTS say 25).
- **[PR #9](https://github.com/nodaysidle/kureksistant/pull/9) `9f82d28`** (squash, ~16:20, per Execution Operator): hardens `vault_knowledge` reads against path traversal, adds an env var for the vault path (no longer hardcoded), and fixes short queries. Installed on the owner's machine 16:27: journal "Loaded 25 actions", service active, `api_keys.json` unchanged (per Execution Operator, not re-checked by ATLAS).
- **Still open:** ⚠️ unauthenticated HTTP :8790; ⚠️ `actions/desktop.py` exec(); end-to-end latency and the ~150-token anchor are unmeasured.

## ## Update 2026-10-11 20:10 (UTC+2) — weekly reconcile (ATLAS)

- ✅ On portfolio-nine as card **07 / 09** (Portfolio PR #1 `9b9a0d8`). Apps card 06 and v0.2.0 release unchanged.
- [[artifacts/vault-operations/repo-status-reconcile-2026-10-11]]

- 2026-10-12 03:50 (ATLAS): kureksistant PR #10 squash 395d7bf (2026-10-12 03:49, per Execution Operator): optional Microsoft-Decision-1 auto-screen decision via OpenRouter with TypeSafe fallback, 1.5s timeout, KUREK_AUTO_SCREEN=0 opt-out, validated null. ⚠️ Privacy risk: prompt text is sent to OpenRouter when the key is set. No latency claims.

- 2026-10-12 05:12 (ATLAS): 🏁 Milestone 2026-10-12 ~05:00 (per Execution Operator): the owner has a working Kurek.apk on Android that controls Kurek on the PC by voice, remotely over Tailscale, tested on mobile data. ⚠️ OPEN RISK (security): the :8790 control API has no authentication and actions/desktop.py exec()s model-generated code; remote access widens exposure to every device on the tailnet. SHIP is reviewing the repo and security; treat it as open until SHIP reports.

- 2026-10-12 05:31 (ATLAS): ✅ CLOSED: Kurek remote OPEN RISK (from the 2026-10-12 ~05:00 milestone), per Execution Operator, user-approved. kureksistant PR #11 squash 822966c (05:31): loopback bind by default (KUREK_REMOTE_BIND=tailscale opt-in); required Bearer token with compare_digest for remote requests; CSRF/Origin blocks, no CORS *; 64KB body cap; remote exec tools gated by KUREK_REMOTE_ALLOW_EXEC; hardcoded token and IP removed from the Android app, release/kurek-remote.apk deleted; SECURITY.md added. Leaked token rotated by the owner (old one returns 401); still in git history but inert. No published APK release. Remaining (local only): actions/desktop.py still exec()s model-generated code for local use; the localhost API is unauthenticated by design when loopback-bound. Not re-verified by ATLAS (cheap mode).

## Current status (2026-10-13 23:51 UTC+2): v0.2.1 Omarchy Integration & Stability Refactor

- **Commit:** `main` = `f0a7cdf` (`feat(arch): Omarchy Hyprland integration, SQLite FTS5 memory & stability hardening (v0.2.1)`). Full report: [[artifacts/kureksistant/refactor-stability-v021-2026-10-13]]. ⚠️ *Correction 2026-10-14 00:47: `f0a7cdf` was a local commit that was never pushed (kept on `backup/pre-v0.2.1`); the real release is PR #13 squash `3761c78`.*
- **1. Zero-config `.env` installs:** Eliminated raw `config/api_keys.json` reads across all `actions/` modules (`dev_agent`, `code_helper`, `flight_finder`, `desktop`, `file_processor`, `computer_settings`, `computer_control`, `youtube_video`). All key access routes through `memory.config_manager.get_gemini_key()` checking environment variables first.
- **2. Omarchy Workstation UX (Hyprland, Ghostty, Herdr, Fish):** Added first-class prioritization for `ghostty` and `herdr` emulators in `open_app.py` and aliases for `fish`. Replaced legacy X11 `pyautogui` hotkeys in `computer_settings.py` with native `hyprctl dispatch` (`cyclenext`, `killactive`, `fullscreen 0`, `movewindow l/r`, `dpms off`), `grim` screenshots on Wayland, and terminal `btop`/`htop` execution.
- **3. Android Remote SSE & Conversational Confirmation:** Muted local workstation PipeWire/mpv TTS during remote phone queries over Tailscale `/remote/prompt`. Bound headless `notify-send` confirmation gate and conversational affirmative/negative ("yes"/"no") turn resolution for pending destructive operations.
- **4. LLM Prompt Alignment:** Synchronized `core/prompt.txt` with actual runtime tool schemas (`screen_vision`, `manage_memory`, `system_monitor`, `vault_knowledge`, `workstation_radar`, `process_sentinel`), removing legacy PyQt6 HUD instructions and defunct tool names.
- **5. Systemd 600M Envelope Safety:** Added low-memory Chromium flags in `browser_control.py`. Wrapped heavy project builds in `dev_agent.py` using `systemd-run --user --scope` to isolate child memory outside `kurek.service` cgroup. Enforced 120s timeout in `ActionRegistry.run`.
- **6. SQLite WAL + FTS5 Memory Engine:** Migrated memory storage in `memory/memory_manager.py` from full-file JSON rewrites to SQLite in WAL mode with FTS5 full-text indexing (`entries_fts`), automatic zero-loss migration from `long_term.json`, and decoupled `background_monitor.py` private lock.
- **Verification:** All 90 pytest tests passed (1 skipped), ruff lint clean (0 errors), C trigger recompiled with zero warnings.

## Current status (2026-10-14 00:46 UTC+2): v0.2.1 released

- 2026-10-14 00:28 (EO, logged by ATLAS 2026-10-14 00:47): ✅ kureksistant v0.2.1 deployed. PR #13 squash `3761c78` (merge gate: agy MERGE / Codex BLOCK on the 'Confirmed and executed' wording; merged on owner approval). PC main reset to kureksistant/main; old local `f0a7cdf` kept on branch `backup/pre-v0.2.1`; backups in `~/kurek-backups/pre-v0.2.1-20261014-002747`. Service active, listening only on 127.0.0.1 and the Tailscale IP (:8790). Tailscale SSE 200; wrong/missing token 401. JSON→SQLite memory migration OK (12 entries, 1 session). PC tests 146 pass / 1 skip. ⚠️ Watch: service memory ~500M vs MemoryHigh 512M.
- 2026-10-14 00:46: GitHub release [Kureksistant v0.2.1](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.1) published, target `3761c78`, Latest. Owner phone test passed: online and responding over Tailscale, migrated memory works (knows him and his projects), middle-click works.
- Release notes draft was on the Grok Bot box (`/workspace/kurek-v0.2.1-release-notes.md`).
- Still open (local only): `actions/desktop.py` exec() for local use; loopback API without auth by design; memory headroom.
- *2026-10-14 15:41:* v0.2.1 release now ships downloads (tarball, SHA256SUMS, debug APK). Merge-gate self-check (`scripts/verify.sh`, draft PR #16) and GitHub Issues status tracking (#17–#21) added; see the session note. Pending owner decision: sandbox vs trusted-only verify.

## Update 2026-10-16 20:04 (UTC+2) — promo history + latest release (ATLAS)

- **Latest release:** v0.2.1 (target `3761c78`).
- **Promo history:** not launched yet. X slot Wed 2026-10-21 17:30. Alan approved dropping the tool count from the hub post (10:42).

## Update 2026-10-16 21:11 (UTC+2) — launch audit (ATLAS)

- ⏳ **Released, not promoted:** no Kurek post on @kaly_ndi from 2026-09-01 to 2026-10-16 21:11. Slot Wed 21 Oct 17:30. GitHub Latest v0.2.1 (tarball `8b3a7a6e…`) matches the hub card. Note: the hub card still says "25 tools" (correct for v0.2.1); SHIP 10:38 says main has 27 modules, not released.

<!-- atlas-2132 -->
## Update 2026-10-16 21:32 (UTC+2): owner facts (ATLAS, via EO)
- ✅ **Owner fact (Alan 21:31):** "kurek was first a GUI - then he went daemon, and its spawned by middlle mouse click hes an ai assistant which has no gui thats the point"
  - Kurek is a **GUI-less daemon AI assistant**, spawned by a **middle mouse click**. Earlier versions (the PyQt6 JARVIS era) had a GUI.
  - Any text that describes Kurek as a GUI app is **stale**. The phase-1 PyQt6 GUI and the `legacy/` GUI are history only. A 21:32 scan of this page found no current-state GUI claim.
- ⚠️ **UNVERIFIED (Alan 21:29):** the local Kurek on arch has a different STT model, **27 tools** and a longer listen window, compared with GitHub v0.2.1 (25 tools). This stays unverified until SHIP diffs arch `kurekizmo` against GitHub. It is not for promo copy until then.

<!-- atlas-2133 -->
## README snapshot: source of truth (2026-10-16 21:33)
- Snapshot: [[wiki/sources/kureksistant-README]] (public `nodaysidle/kureksistant` @ `09e3c7d`, committed 2026-10-15T14:07:02+02:00). Owner source of truth (Alan 21:32/21:33). Read it first; it wins over older text on this page.
- Local checkout on arch (read-only `git status` at 21:35, no fetch, so the unpushed count may be stale): `~/dev/nodaysidle/kurekizmo` (origin → `nodaysidle/kureksistant`): 16 uncommitted paths, README.md clean, 0 unpushed vs the local upstream ref.
- Local vs GitHub README diff: README matches GitHub `09e3c7d`; uncommitted Android edits; 2 local-only backup branches (`ab1420a`, `f0a7cdf`). The old-origin remote `kurekizmo` returns API 404 (private, renamed or deleted: unknown) and is **not** snapshotted (SHIP 21:34)

<!-- atlas-2139 -->
## Canonical page + owner decisions (2026-10-16 21:38)
- Permanent rule: the truth is [[wiki/concepts/kurek-canonical-readme]] (on arch: commit `7fab6cd`, local and unpushed) plus [[wiki/sources/kureksistant-README]]. Kurek has no GUI on purpose (middle-click daemon).
- Unrestricted shell is kept: off by default, gated by `KUREK_REMOTE_ALLOW_EXEC=1` with a warning (Alan 21:38). The v0.2.2 PR is allowed; merge and release each need their own yes.

<!-- atlas-2158 -->
## Parked (owner, 2026-10-16 21:46)
- Alan 21:46: "leave kurek for now alone, focus on tomorrows launch". No Kurek work until Alan un-parks it.

<!-- atlas-2303 -->
- **README demo GIF:** **no**, at HEAD `09e3c7d` (icon `desktop/kurek.png` only) (SHIP 23:00, [[wiki/sources/catalog-audit-2026-10-16]]). ⚠️ The 2026-10-10 "real demo GIF" section above is **stale** for the current README.

## X slot on hold (owner, 2026-10-17 04:09)
- The Wed 21 Oct 17:30 v0.2.1 X slot is ⏳ **held pending SHIP diff verification** of the local `arch` build (`kurekizmo`) against GitHub (`kureksistant`). Full slot history and what lifts the hold: [[wiki/decisions/2026-10-15-kurek-v0-2-1-x-slot]].
