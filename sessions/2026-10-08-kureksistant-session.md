---
type: session
topic_slug: kureksistant
session_id: 2026-10-08-kureksistant
status: active
last_agent: Antigravity
last_updated: 2026-10-10T07:35:00+02:00
threads_active: []
tags:
  - session
  - kureksistant
---

# Session: kureksistant audit and cleanup

## Resume here (read first)

- Overview + current status: [[wiki/concepts/kureksistant-overview]]
- Audit (C−): [[artifacts/kureksistant/audit-2026-10-08]]
- Discrepancies: [[wiki/concepts/kureksistant-source-discrepancies]]
- MOC: [[wiki/MOC/moc-nodaysidle-knowledge]] (no kureksistant inbox idea or topic MOC exists)
- Umbrella session: [[sessions/2026-10-07-vault-operations-session]]

## Decisions made

- 2026-10-08 — The user asked for a read-only audit first, with no changes without approval.
- 2026-10-08 — The user approved re-cutting the v0.1.0 release without keys. The `config/api_keys.json` on the user's own computer must **not** be removed or changed.
- 2026-10-08 — The user approved: move the legacy GUI to `legacy/` with the daemon as canonical; repo polish; basic CI. Then: "after its done you can merged it".
- 2026-10-08 — The user approved the README RAM and tool-count correction (~333MB, 24 tools), merged once CI passes.
- 2026-10-08 — The user clarified lineage: `kurekizmo` was made private on GitHub; `kureksistant` was created as the public repository because TypeSafe Jev cognitive triage and deep optimizations (~333MB daemon, faster-whisper) were added.
- 2026-10-08 — The user approved fixing stability bugs and installer deps in code and repo before updating vault docs.
- 2026-10-08 — The user wants all nodaysidle work logged in this vault for future agents.

## Progress

- 2026-10-08 02:57–03:03 — A Cursor cloud agent (`bc-e01c8f24-b3e6-5c91-afb6-bee6dd7d455c`) audited `main` @ `99a7cec` read-only. Grade C−. Critical finding: the public v0.1.0 tarball contained `config/api_keys.json` with likely-live Gemini and OpenRouter keys.
- 2026-10-08 — v0.1.0 asset re-cut on the same tag without secrets. New SHA-256 `a4085d73ae8764f6b9034e3caabd4c4278f345d074f7909dad171dea63861003`; `SHA256SUMS.txt` replaced; verified 0 `api_keys.json` and 0 `.env`.
- 2026-10-08 — [PR #2](https://github.com/nodaysidle/kureksistant/pull/2) squash-merged after CI passed (`main` → `31d7e56`): legacy GUI moved to `legacy/`, `SECURITY.md`/`NOTICE`/SPDX licence, `.env` settings, CI, package deny-list.
- 2026-10-08 — The Cursor GitHub app could not set topics (403, "Resource not accessible by integration"). The user set the topics and description by hand.
- 2026-10-08 ~03:32 — [PR #3](https://github.com/nodaysidle/kureksistant/pull/3) squash-merged after CI passed (`main` → `52d009b`): ~333MB / 24 tools in the README, badge, AGENTS.md and daemon docstring.
- 2026-10-08 03:40 — Vault updated: audit artifact, overview status, discrepancies, this session, LATEST, audit log.
- 2026-10-08 05:47 — Antigravity fast-forwarded local repo to `52d009b` and committed/pushed `d863922` to `origin/main`:
  - Fixed `kurek_daemon.py:454` `UnboundLocalError` on `last_tool_output`.
  - Fixed `core/dream_cycle.py:66` handling of string/dict/None return types from `query_deepseek`.
  - Fixed F821 undefined symbols in `actions/file_controller.py` (`re`), `actions/screen_vision.py` (`BASE_DIR`), and `actions/code_helper.py` (`_default_path` → `_resolve_save_path`).
  - Aligned dependencies: added `google-genai` and `typesafe-sdk` to `requirements.txt`, updated `install_linux.sh` to install via `requirements.txt`.
  - Expanded `.github/workflows/ci.yml` ruff F82 check to cover `actions/`.
  - Verified local daemon smoke test and ruff syntax/F82 checks (all passing).
- 2026-10-08 05:54 — Re-ingested README, AGENTS.md, and re-cut v0.1.0 release SHA256SUMS.txt at `d863922` into `sources/raw/docs/` and `sources/index/` (`src-20261008-ae52ff2`, `src-20261008-88302c2`, `src-20261008-f95e626`). Marked historical stubs superseded in frontmatter and updated `sources/README.md`.

## Do not re-fetch

- [[sources/index/src-20261008-ae52ff2-kureksistant-readme]], [[sources/index/src-20261008-88302c2-kureksistant-agents]], [[sources/index/src-20261008-f95e626-kureksistant-sha256sums-v0-1-0]]. These are active at `d863922`. Superseded stubs (`src-20261007-c1c7fe9`, `src-20261007-459dbb7`, `src-20261007-e1be179`) must not be cited for current metrics.

## Next actions

1. **Human:** revoke the old Gemini and OpenRouter keys (the old tarball was public). Status unconfirmed.
2. ~~Fix the `/prompt` `UnboundLocalError` at `kurek_daemon.py:505`~~ done at `d863922`.
3. ~~Fix the `core/dream_cycle.py` str-vs-dict handling of the `query_deepseek` return value~~ done at `d863922`.
4. ~~Fix F821s: `re` (`actions/file_controller.py`), `BASE_DIR` (`actions/screen_vision.py`), `_default_path` (`actions/code_helper.py`)~~ done at `d863922`.
5. ~~Align `install_linux.sh` deps and `requirements.txt` (`typesafe-sdk`, `google-genai`)~~ done at `d863922`.
6. Add auth (token or Unix socket) to the localhost control API; review the `exec` in `actions/desktop.py`. Deferred.
7. Decide the OpenRouter story (AGENTS.md says never; the legacy config still references it).
8. Optional: drive ruff/mypy toward green on the legacy code, or relax the strict config.
9. ~~Re-ingest the README, AGENTS.md and SHA256SUMS at `d863922`~~ done at `d863922`.

## Thread registry

| Thread | Focus | Status | Last output |
|--------|--------|--------|-------------|
| kureksistant audit + cleanup | audit, release re-cut, PR #2, PR #3 | done | [[artifacts/kureksistant/audit-2026-10-08]] |
| kureksistant stability bugfixes | items 2–5 above (daemon error, dream cycle, F821s, deps) | done (`d863922`) | [[wiki/concepts/kureksistant-overview]] |

## Handoff notes

- Repo is public; `main` = `d863922`. Local clone `../kurekizmo` is clean and fully in sync with origin.
- Never touch the user's local `config/api_keys.json` or `.env`.
- **Standing reminder for next session**: Confirm human revocation of the old Gemini and OpenRouter API keys in their respective provider dashboards (due to the historical pre-audit public release leak).
- The Cursor GitHub app has no repo-admin permission (topics, settings). Give the user manual steps instead.

## Update 2026-10-10 05:11 (UTC+2): 2026-10-10 perf/IPC overhaul

- The owner pushed kureksistant `02382f2` (05:03) and vault commit `8e80480` (05:04). That vault commit added only `wiki/concepts/kureksistant-overview.md`; it had no audit entry and no session note until this update.
- Grok Bot (ATLAS) checked the code.
  - **Verified:** UDS IPC, the C trigger, sentence streaming, the mpv sink, the Hyprland watcher and the systemd unit.
  - **Unbacked:** the <2ms / sub-400ms / 60ms figures.
  - **Stale:** "24 tools".
  - **Conflict:** `MemoryHigh=250M` versus ~333MB; the daemon swaps.
  - See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].
- **Open for the owner:**
  - commit the untracked notes the overview links to (10 links are broken on GitHub);
  - raise `MemoryHigh`;
  - add latency benchmarks;
  - fix the `ai-assitant` topic;
  - refresh the release notes or cut a new release.
- The vault is left uncommitted; the owner commits it himself.

## Update 2026-10-10 05:40 (UTC+2): PR #4 merged

- [PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f` fixed audit items 1–4 and 8, each with a test, with CI green. Local clone and installed unit updated; the service has been active since 05:38:49 at 345 MiB with ~0 swap; a UDS subscribe returns a state event and stays open. See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].
- **Still open (owner decision):**
  - **PR B (not yet approved):** hardcoded paths; installer system dependencies; socket authentication and the `/tmp` socket fallback; JSON escaping and the timeout in the C trigger. ✅ **Closed 2026-10-10 05:51 by [PR #5](https://github.com/nodaysidle/kureksistant/pull/5) `e1d3575`.**
  - **PR C (optional):** `hyprctl` is spawned on every focus change; the latency claims (<1/<2ms, sub-400ms, 60ms) are still unmeasured; cleanups. ✅ **Closed 2026-10-10 06:11 by [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920`** (merged by [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c`).
  - **v0.2.0** has not been cut (v0.1.0 is still the only release). ✅ **Done 2026-10-10 06:11:** [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0) released (`e91a14c`).
- The vault is uncommitted; the owner commits it.

## Update 2026-10-10 05:51 (UTC+2): PR #5 merged

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

## Update 2026-10-10 06:11 (UTC+2): v0.2.0 released

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

## Update 2026-10-10 07:35 (UTC+2): showcase card 06, real GIF, launch

- Verified: [nodaysidle-apps PR #3](https://github.com/nodaysidle/nodaysidle-apps/pull/3) `46251cb` (Six tools, 06 / 06, `#kurek`, 14/14 links 302, voiced clip, JARVIS credit); [kureksistant PR #8](https://github.com/nodaysidle/kureksistant/pull/8) `022d4be` (real REEL GIF).
- **Launch on X: Wed 21 Oct 2026, 15:15 Europe/Ljubljana**, as reported by Execution Operator. ⚠️ **Conflict:** REACH's plan file on the box (`/workspace/reach/x-promo-strategy-2026-10-12.md`, mtime 2026-10-09 17:30) has Wed 21 Oct 15:15 as "Browser build thread (or the poll winner)". In that file Kurek appears only as a no-link recap on Wed 14 Oct 20:30 and a re-feature on Thu 29 Oct citing stale v0.1.0 figures (~333MB, `docs/demo.gif`). REACH needs to confirm or update the plan.
- **Next:** REEL/REACH to reconcile the X calendar; the Thu 29 Oct row still cites v0.1.0 figures.
- The vault is uncommitted; `sources/raw/` was untouched.

- 2026-10-10 16:28: owner commit 5477ef5 added vault_knowledge (tool #25, now 25 tools via 6137128); PR #9 9f82d28 hardened vault reads, env vault path, short-query fix; installed 16:27 (Loaded 25 actions). Overview fixed minimally by ATLAS; REACH launch conflict resolved.
