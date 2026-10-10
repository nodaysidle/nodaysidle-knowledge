---
type: wiki-note
note_kind: concept
topic_slug: nodaysidle-browser-linux
status: draft
created: 2026-10-07
updated: 2026-10-08
tags:
  - wiki
  - nodaysidle-browser-linux
---

# nodaysidle-browser-linux — overview

## Summary

A small native Linux browser (Rust, GTK 3, WebKitGTK 4.1) for focused browsing, no telemetry, released as v0.1.0 with a host-dependent AppImage. Linux counterpart of the macOS [nodaysidle-browser](https://github.com/nodaysidle/nodaysidle-browser).

## Details

- **Stack:** Rust 2021, MSRV 1.88; GTK 3 + WebKitGTK 4.1 (libsoup3); no GTK 4 move planned.
- **Identity:** app ID `com.nodaysidle.Browser` used as Wayland app_id, X11 WM_CLASS and desktop file name.
- **Features:** search-first Home (DuckDuckGo), custom tab strip, address-bar resolution, find bar, pop-up windows, fullscreen, downloads with cancel/close confirmation, error/crash pages.
- **Privacy:** no telemetry; cookies (`cookies.sqlite`) and history (`history.json`) stored `0600` under `~/.local/share/nodaysidle-browser/`; WebKit sandbox on; permission prompts for location/camera/mic/notifications/pointer lock; Menu → Clear Browsing Data.
- **History:** 56 commits, `ae08c40` → `2fffaab` (2026-10-07 09:34 UTC+2), in fix series X/R/N/I/V. ⚠️ Stale as of 2026-10-08: `a46b2cd`, `a124f2f` and `a813e70` have landed since; `master` = `a813e70`.
- **Remote:** `origin` = github.com/nodaysidle/nodaysidle-browser-linux (handoff's "no git remote" is stale).

## Claims & citations

| Claim | Source |
|-------|--------|
| Stack, MSRV 1.88, features, privacy model | [[sources/index/src-20261007-2d7bab4-browser-linux-readme]] |
| No GTK 4 plan; app identity; module map | [[sources/index/src-20261007-6223dc7-browser-linux-agent-handoff]] (⚠️ unreliable; consistent with README) |
| v0.1.0 feature list | [[sources/index/src-20261007-1764cc7-browser-linux-release-notes-v0-1-0]] |
| 56 commits, series, HEAD | [[sources/index/src-20261007-e02f632-browser-linux-git-log]] |
| Clear Browsing Data exists | [[sources/index/src-20261007-2d7bab4-browser-linux-readme]]; code `src/privacy.rs` @ `2fffaab` (agent check) |
| `origin` remote exists | `git remote -v` 2026-10-07 (agent check); contradicts [[sources/index/src-20261007-6223dc7-browser-linux-agent-handoff]] |

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[wiki/concepts/nodaysidle-browser-linux-audit-status]]
- [[wiki/concepts/nodaysidle-browser-linux-appimage-packaging]]
- [[_system/templates/catalog/nodaysidle-browser-linux]]

## Open questions

- macOS parity gaps (bookmarks, zoom, settings, sync, tab reorder) listed only in [[sources/index/src-20261007-6223dc7-browser-linux-agent-handoff]]; unverified.
- Wayland app_id behaviour untested live per [[sources/index/src-20261007-6223dc7-browser-linux-agent-handoff]].

## Current status (2026-10-08 22:30 UTC+2)

Verified against the public GitHub API by Grok Bot (ATLAS) during [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]]. Newer facts here take precedence over Details.

- **Repo:** public. The default branch is **`master`** (not `main`), HEAD `a813e70` (README promo GIF, PR #1, merged 2026-10-07 22:55). No open PRs, no GitHub homepage URL. The GitHub API detects no licence.
- **Latest release:** v0.1.0 (2026-10-07 09:38) with `nodaysidle-browser-x86_64.AppImage`, SHA-256 `f6d82efa…4404`. The release body already says "Host-dependent AppImage" and gives that SHA-256, so the optional release-body edit (session next action 6) is no longer needed.
- **Demo GIF:** `docs/browser-linux.gif` is in the README and loads.
- **Showcase:** ⚠️ not on the official portfolio (nodaysidle-portfolio-nine.vercel.app). Its "NODAYSIDLE Browser" card links the macOS [nodaysidle-browser](https://github.com/nodaysidle/nodaysidle-browser), not this repo. It is not on showcase-v2 either.
