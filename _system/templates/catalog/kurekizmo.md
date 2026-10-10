---
type: catalog-entry
name: Kureksistant (Kurek)
status: in-progress
short_description: Personal AI assistant (~333MB RAM with faster-whisper, 24 tools) with screen vision, Grok voice, clipboard manager, Jev cognition, Muse Memory; v0.1.0 Linux bundle.
repo_url: https://github.com/nodaysidle/kureksistant
site_url: https://github.com/nodaysidle/kureksistant/releases/tag/v0.1.0
local_path: ../kurekizmo
stack:
  - Python
  - desktop integration
  - Hyprland / Omarchy
tags:
  - catalog
  - native
  - ai-tools
---

# Kureksistant (`kurekizmo` local tree)

Autonomous assistant and workstation radar. Local folder name `kurekizmo`; upstream repo **kureksistant**.

- **Repo:** [github.com/nodaysidle/kureksistant](https://github.com/nodaysidle/kureksistant)
- **Local clone:** `../kurekizmo`
- **Status 2026-10-08:** audited (C−). v0.1.0 re-cut without leaked keys; PRs #2/#3 merged (`main` = `52d009b`). See [[wiki/concepts/kureksistant-overview]] and [[artifacts/kureksistant/audit-2026-10-08]].

- **Status 2026-10-10 05:11:** `main` = `02382f2` (UDS IPC, C trigger, sentence-streaming TTS, mpv sink, Hyprland watcher, systemd unit). The code is verified; the latency figures (<2ms / sub-400ms / 60ms) are unbacked. `MemoryHigh=250M` conflicts with ~333MB. Tools: 27 modules versus the documented 24. *(✅ Corrected 2026-10-10 06:11: 24 tools loaded.)* Still v0.1.0. See [[artifacts/kureksistant/perf-ipc-check-2026-10-10]].

- **Status 2026-10-10 05:40:** `main` = `c83f46f` ([PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f`). Fixed, each with a test: UDS subscribers stay open (state events work); dream cycle; stuck THINKING → IDLE; honest failure speech instead of "All set.". MemoryHigh/swap is resolved (400M/600M; live 345 MiB). Open: PR B (paths, installer dependencies, socket auth and `/tmp` fallback, C trigger escaping/timeout) is not approved *(✅ closed 2026-10-10 05:51 by [PR #5](https://github.com/nodaysidle/kureksistant/pull/5) `e1d3575`)*; PR C is optional (hyprctl per focus change, unmeasured latency, cleanups); v0.2.0 has not been cut.

- **Status 2026-10-10 05:51:** `main` = `e1d3575` ([PR #5](https://github.com/nodaysidle/kureksistant/pull/5) `e1d3575`). Findings 5, 6, 9 and 10 are fixed: templated unit + `install_path`; installer dependency checks + gcc + Playwright; 0600 socket + `SO_PEERCRED`, no `/tmp`; trigger JSON escaping + 500ms I/O timeouts. Memory 450M/600M; live 280 MiB, 452 MiB peak. Open, not approved: PR C (hyprctl per focus change, unmeasured latency, cleanups) and v0.2.0. *(✅ Both done 2026-10-10 06:11: [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920`, [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0).)*

- **Status 2026-10-10 06:11:** **Released [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0)** (Latest, `e91a14c`; tarball 942,506 bytes, SHA-256 `6b85603070959836f1fecd51bd3b2450d8bc9cbefb6ed0af240f1847e6e619da`). [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920` closes PR C (lazy Hyprland geometry, measured ~0.8ms trigger wording, cleanups, 512M/600M); [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c` adds the changelog. Topic fixed, 24 tools confirmed. Live 313 MiB / 396 MiB peak right after the 06:10 restart. Open, owner not yet decided: ⚠️ unauthenticated HTTP :8790 (security risk); ⚠️ `actions/desktop.py` exec() of model code (security risk); end-to-end first-audio and capture latency not measured.

- **Status 2026-10-10 07:35:** on the downloads showcase as **card 06** (https://nodaysidle-apps.vercel.app/#kurek; [nodaysidle-apps PR #3](https://github.com/nodaysidle/nodaysidle-apps/pull/3) `46251cb`; voiced clip; CC BY-NC 4.0 JARVIS credit; 14/14 links 302). **Real demo GIF:** [kureksistant PR #8](https://github.com/nodaysidle/kureksistant/pull/8) `022d4be` (merged 06:30:45 CEST, not ~07:33) replaces the mock-up `docs/demo.gif` (it showed ~55MB / 20 tools / <100ms) with REEL's v0.2.0 GIF (800×800, ~2.7MB). It is byte-identical to `/workspace/clips/kurek/kurek.gif`; the hashes match. `main` = `022d4be`. **Launch on X: Wed 21 Oct 2026, 15:15 Europe/Ljubljana**, as reported by Execution Operator. ⚠️ **Conflict:** REACH's plan file on the box (`/workspace/reach/x-promo-strategy-2026-10-12.md`, mtime 2026-10-09 17:30) has Wed 21 Oct 15:15 as "Browser build thread (or the poll winner)". In that file Kurek appears only as a no-link recap on Wed 14 Oct 20:30 and a re-feature on Thu 29 Oct citing stale v0.1.0 figures (~333MB, `docs/demo.gif`). REACH needs to confirm or update the plan.
