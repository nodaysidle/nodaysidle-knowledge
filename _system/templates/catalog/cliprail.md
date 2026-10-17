---
type: catalog-entry
name: ClipRail
status: completed
status_note: "Finished macOS build, unmaintained (owner 2026-10-16 22:39/22:41: no Mac rebuilds; launched as-is with README fixes only)."
release_status: released
short_description: Local, text-only clipboard history for the macOS menu bar — recent clips, pinned favorites, search, pause and re-copy, with no network access, no account and no auto-paste.
github_status: published
repo_url: https://github.com/nodaysidle/cliprail
site_url: https://github.com/nodaysidle/cliprail/releases/tag/v1.2.0-dmg.20260727
local_path: "[PLACEHOLDER: ../cliprail when cloned locally]"
stack:
  - Swift 6
  - SwiftUI
  - macOS 14+ menu bar
updated: 2026-10-17
tags:
  - catalog
  - native
  - macos
---

# ClipRail

Portfolio group: **Native apps** (`cliprail`). macOS-only menu bar utility for plain-text clipboard reuse. Truth source: README snapshot [[wiki/sources/cliprail-README]] (`d8ad7ba`, 2026-10-16T22:59:16+02:00).

## Facts (from the README snapshot)

- **Version 1.2.0** · macOS 14+ · Swift 6 · SwiftUI.
- Last 10 unpinned plain-text clips, up to 3 pinned clips that survive Clear, live search, delete, pause, 60-second dedupe, re-copy (no auto-paste).
- Privacy: local UserDefaults only; no network, sync, telemetry or account; no microphone, camera, Accessibility or global-hotkey permissions.
- Download: `ClipRail-1.2.0.dmg` (~195 KB) + `.sha256`, SHA-256 `a83120148c67d7a33fb191ae2a373f237c80313b4e584471db29aae464115c0d`, from release `v1.2.0-dmg.20260727` (the only release; published 2026-07-27 02:39 +02:00).
- Signing: **ad-hoc** (no Developer ID, not notarized; [[wiki/sources/catalog-audit-2026-10-16]]). First launch needs right-click → Open ("Open anyway").

## Status

- 2026-10-16 22:35 (SCOUT): demand score **4/5**, the top pick in [[sessions/handoffs/2026-10-16-SCOUT]].
- 2026-10-16 22:41 (EO): macOS-only menu bar app; **finished Mac build, unmaintained, launched as-is**; README fix only, no Mac rebuild.
- 2026-10-16 22:59 (ATLAS, verified): [PR #5](https://github.com/nodaysidle/cliprail/pull/5) merged as `d8ad7badf1a55d6d05bc8662fb3a55e65fe85685` (README: download `ClipRail-1.2.0.dmg` + `.sha256`). **No new release**; Latest is still `v1.2.0-dmg.20260727`.
- **X launch slot: Tue 3 Nov 2026 17:30** Europe/Ljubljana (confirmed EO 22:39). Drafts are due to Alan by 14:00 that day.
- No overview page yet under `wiki/concepts/`. No local checkout on arch.
- 2026-10-17 (Claude Opus): entry created from [[sessions/LATEST]] and the README snapshot; nothing re-checked live. See [[artifacts/2026-10-17-vault-and-grokbot-audit]].
