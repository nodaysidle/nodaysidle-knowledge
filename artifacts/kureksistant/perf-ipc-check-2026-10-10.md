---
type: artifact
artifact_kind: audit
topic_slug: kureksistant
generated: 2026-10-10
generator_agent: auditor
repo_ref: main @ 02382f2
vault_ref: 8e80480
verified_at: 2026-10-10T06:10:00+02:00
verified_at_initial: 2026-10-10T05:11:00+02:00
repo_ref_latest: main @ e91a14c (v0.2.0)
tags:
  - artifact
  - audit
  - kureksistant
---

# Audit: kureksistant 2026-10-10 perf/IPC overhaul, vault note vs code

Read-only check by Grok Bot (ATLAS), 2026-10-10 05:11 (UTC+2), per user.

- **Compared:** the owner's vault commit `8e80480` ("record 2026-10-10 sub-400ms streaming and UDS IPC overhaul", 05:04) with [nodaysidle/kureksistant](https://github.com/nodaysidle/kureksistant) `main` @ `02382f2` ("feat: sub-400ms streaming TTS, UDS trigger client, and Hyprland IPC watcher", 05:03:51, 13 files, +1116/−124).
- **Sources:** the cursor-github connector (repo, commit, issues/PRs, releases), raw files at `main`, the check-runs API, and read-only checks on the owner's machine (systemd, sockets, bindings).
- **Not done:** nothing in the repo was changed, and no latency was measured.
- **Labels:** **verified** = code or machine state backs the claim; **unbacked** = the code exists but no benchmark or test supports the number; **stale** = superseded by newer facts.

## What 8e80480 changed

It added `wiki/concepts/kureksistant-overview.md` to git for the first time (+96 lines). The file had been untracked; the commit captures the whole note, including a new "Done 2026-10-10" block. That block is attributed to "Antigravity", while the commit author is `nodaysidle`. No other vault file was touched: no audit entry and no session note.

## Claims in the 2026-10-10 block

| Claim (overview) | Verdict | Evidence |
|---|---|---|
| UDS server at `$XDG_RUNTIME_DIR/kurek.sock` alongside HTTP :8790 | **verified** | `kurek_daemon.py:816-842` (`AF_UNIX` bind). Live `/run/user/1000/kurek.sock` (srwxr-xr-x). Journal 03:33:28 "Listening at Unix Domain Socket … / http://127.0.0.1:8790". |
| Real-time state events over UDS for Waybar/AGS | **verified (code)** | `kurek_daemon.py:236-244` `_broadcast_state_uds`, `:884`. No Waybar/AGS consumer was found. | ✅ *(2026-10-10 05:40) Working: subscribers were being closed by the finally block; [PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f` fixed it. A live subscribe got a state event and stayed open.*
| C trigger `bin/kurek-trigger.c` → `~/.local/bin/kurek-trigger`, auto-spawn fallback | **verified** | `bin/kurek-trigger.c:37-54` (connect, then retry); `install_linux.sh:43-46` compiles it with gcc; the binary exists (17k, 03:32). |
| Summon latency ~50ms → **<2ms** | **unbacked** | No benchmark or test in the repo. The code itself says **<1ms** (`bin/kurek-trigger.c:2`, README:124/131/147, AGENTS.md:58). The vault says <2ms, so the two numbers don't match each other either. |
| Sentence-buffered streaming `core/llm_client.py:stream_deepseek_sentences` | **verified** | `core/llm_client.py:869` (function); `:31` `_SENT_END = (?<=[.!?])\s+\|(?<=\n)\s*\n`; daemon `kurek_daemon.py:506-557` calls `tts.speak_chunk` per sentence. The vault's `[.!?\n]` is simplified; the real rule needs whitespace after the punctuation. |
| Chunks "immediately dispatch" to xAI Grok TTS (Sol) | **verified, with a caveat** | `core/tts.py:536-561` `XAITTSEngine`: one blocking `requests.post("https://api.x.ai/v1/tts")` per sentence. Audio is streamed per sentence, not per token. |
| First-syllable latency ~3.5s → **~350–500ms** / "sub-400ms" | **unbacked** | No benchmark, timing log or test (`tests/` has only `test_daemon_smoke.py`). It depends on DeepSeek time-to-first-sentence plus a full xAI TTS round trip. The vault's own range (350–500ms) contradicts its "sub-400ms" title. |
| Persistent mpv sink, IPC `kurek_mpv.sock`, `/dev/shm` chunks, `stop` barge-in | **verified (code)** | `core/mpv_sink.py:35,72-76,115-138,151`. Live `/run/user/1000/kurek_mpv.sock`. "Zero NVMe writes" holds only when `/dev/shm` exists (it falls back to the runtime dir, `:124`). Barge-in was not exercised. |
| Hyprland watcher on `.socket2.sock`, "completely eliminating" `hyprctl` | **partly unbacked** | `core/hyprland_watcher.py:21-58` is event-driven, but it still calls `hyprctl activewindow -j` to seed state (`:85-108`). `actions/screen_vision.py:63-65` falls back to `hyprctl` if the watcher returns nothing. "O(1)" is a dict lookup, which is fine. |
| Zero-disk window vision via `grim -g … -` → `io.BytesIO`, **sub-60ms** | **verified (Linux path) / unbacked (60ms)** | `actions/screen_vision.py:80-99`. The macOS fallback writes `/tmp/kurek_screen_cap.png` (`:109`). There is no timing data for 60ms. |
| systemd user unit, `graphical-session.target`, journald, `MemoryHigh=250M` / `MemoryMax=450M` | **verified, conflicts with the RAM figure** | `desktop/kurek.service` matches `~/.config/systemd/user/kurek.service`; the unit is active since 03:33:30. **Live 05:10:** cgroup MemoryCurrent 237 MiB, peak 251 MiB, MemoryHigh 250 MiB, RSS 275 MiB. The journal shows a "239.7M memory swap peak". A 250M soft cap sits below the documented ~333MB (with faster-whisper), so the cap throttles the daemon and pushes it into swap. The unit's comment "Comfortably accommodates faster-whisper" is not borne out. | ✅ **Resolved 2026-10-10 05:40** by [PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f`: 400M/600M installed; live 345 MiB, 402 MiB peak, 12 KiB swap.
| Hyprland bindings mouse:274 and SUPER+mouse:274 → `kurek-trigger toggle` | **verified (local)** | `~/.config/hypr/bindings.lua:39-40`. This is outside the repo. |

## Stale or conflicting facts elsewhere in the overview

| Fact | Verdict | Evidence |
|---|---|---|
| 24 tools | **stale / unverified** | ✅ *Corrected 2026-10-10 06:11: 24 is right (journal "Loaded 24 actions"); the 27 files include helpers.* `main` has 27 `actions/*.py` modules, excluding `__init__.py`; the local clone has 28. README:28/156, AGENTS.md:3/28/34 and the daemon still say 24. The number of registered tools was not counted. |
| ~333MB RAM | **unbacked as current** | The 2026-10-08 audit measured ~333MB. The live service now uses 237–251 MiB, but only because the 250M cap forces it to swap. No new measurement exists. |
| Release v0.1.0 | **verified, but the notes are stale** | ✅ *2026-10-10 06:11: superseded by [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0); the v0.1.0 notes are still unedited.* Still the only release (assets re-cut 2026-10-08, SHA-256 `a4085d73…1003`). There is no release for `02382f2`. The release body still says "~55MB idle" and "20 built-in actions". |
| Licence CC BY-NC 4.0 (derived from FatihMakes' JARVIS) | **verified** | `LICENSE` copyright FatihMakes + NODAYSIDLE, `SPDX-License-Identifier: CC-BY-NC-4.0`; README badge. The GitHub API shows "Other" (NOASSERTION), as expected. |
| Paid API keys required | **verified** | README:94-95 (DEEPSEEK and XAI required), :114 "Not fully offline"; the v0.1.0 notes mention "API credits". |
| Topic `ai-assistant` | **stale (typo on GitHub)** | ✅ *Fixed 2026-10-10 06:11 (topic `ai-assistant`).* The live topic is `ai-assitant`. |
| Open issues | **verified: none** | `open_issues_count: 0`. Only #1–#3 exist, all merged PRs. |
| CI | **verified, but shallow** | `lint-and-smoke` passed on `02382f2`. It runs only `tests/test_daemon_smoke.py` (`.github/workflows/ci.yml:66`). There are no tests for UDS, streaming, mpv or the watcher. |
| History "7 commits, 2026-10-03 → 10-06" | **stale** | `main` now has 10+ commits up to `02382f2`. |

## Link problems

- **No audit entry** in `_audit/log.md` and **no session note** for the 2026-10-10 change. `sessions/LATEST.md` still points at [[sessions/2026-10-08-kureksistant-session]], which has no 10-10 entry.
- **Wikilinks resolve locally, but not on GitHub.** All 12 links in the overview point at files that exist on this machine. Only 2 are in git at `8e80480` / `origin/main` ([[wiki/MOC/moc-nodaysidle-knowledge]] and [[_system/templates/catalog/kurekizmo]]). The other 10 are untracked, so they are broken in the pushed vault:
  - [[artifacts/kureksistant/audit-2026-10-08]] and [[sessions/2026-10-08-kureksistant-session]];
  - [[wiki/concepts/kureksistant-source-discrepancies]];
  - 7 `sources/index/src-*kureksistant*` notes.
- **Attribution:** the 10-10 block says "Antigravity" but the commit author is the owner. It is unclear which one did the work.

## Recommended next steps

- **Owner:** commit the linked artifacts, session and sources so the overview's links resolve on GitHub.
- **Owner:** raise `MemoryHigh` (e.g. to ≥400M) or measure without Whisper; at 250M it causes swapping. ✅ *Done: 512M/600M (PR #6 `f1d7920`).*
- **Owner:** add timing logs or a benchmark for trigger, first-audio and capture latency before quoting <2ms / sub-400ms / 60ms; settle on <1ms or <2ms. ✅ *Done for the trigger (~0.8ms median, `bench_trigger.py`); sub-400ms and 60ms are dropped, not measured.*
- **Owner:** fix the topic typo; refresh the v0.1.0 release notes (55MB / 20 actions) or cut v0.2.0 for `02382f2`; recount the tools (24 vs 27 modules). ✅ *Done: topic `ai-assistant`; v0.2.0 cut at `e91a14c`; 24 tools verified (24 `TOOL` dicts in 28 files).*

## Update 2026-10-10 05:40 (UTC+2): PR #4 verified

Verified on GitHub (PR state, merge SHA, diff, check-runs) and passively on the machine (`systemctl --user show`, journal, a read-only UDS subscribe; the trigger was not toggled).

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

## Update 2026-10-10 05:51 (UTC+2): PR #5 verified

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
  - **PR C:** `hyprctl` spawned on every focus change; unmeasured latency claims (<1/<2ms, sub-400ms, 60ms); cleanups. ✅ **Closed 2026-10-10 06:11 by [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920`** (merged by [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c`).
  - **v0.2.0:** not cut. ✅ **Done 2026-10-10 06:11:** [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0) released (`e91a14c`).
- See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].

## Update 2026-10-10 06:10 (UTC+2): PR #6, PR #7 and v0.2.0

- ✅ [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920` (squash-merged 06:02:40 CEST): lazy Hyprland geometry (no `hyprctl` per focus change), `KUREK_TIMING` logs, `scripts/bench_trigger.py`, safer sentence splitter, `MemoryHigh=512M` / `MemoryMax=600M`, docs limited to measured figures.
- ✅ [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c` (06:05:56 CEST): v0.2.0 bump + `CHANGELOG.md`. CI green (run 38022871050). The informational bench on that run: 0.840ms median, 1.061ms p95, 200 runs.
- ✅ **[v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0)** published 06:07:28 CEST, Latest, tag → `e91a14c`. Asset `kureksistant-v0.2.0-linux-x86_64.tar.gz` (942,506 bytes, SHA-256 `6b85603070959836f1fecd51bd3b2450d8bc9cbefb6ed0af240f1847e6e619da`) + `SHA256SUMS.txt` (106 bytes). Re-download `sha256sum -c` OK; secret scans clean; only `.example` key/env files.
- **Claims table, resolved:**
  - <2ms vs <1ms → **~0.8ms median, measured** (vault and repo now agree).
  - sub-400ms / ~350–500ms → **removed** (unmeasured; timing logs exist now).
  - "completely eliminating hyprctl" → **removed**; geometry is fetched lazily.
  - sub-60ms capture → **no longer claimed**.
  - `MemoryHigh=250M` conflict → **resolved** (512M/600M); RAM documented as ~450MB peak observed.
  - 24 tools → **verified**. Topic typo → **fixed**. Release notes 55MB / 20 actions → superseded by v0.2.0 notes.
- **Still open:** the link problems above (untracked vault files), the attribution question, HTTP API auth, `exec` in `desktop.py`.

## Update 2026-10-10 06:11 (UTC+2): PR #6/#7 and v0.2.0 verified

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
