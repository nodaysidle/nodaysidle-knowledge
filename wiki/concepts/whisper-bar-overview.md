---
type: wiki-note
note_kind: concept
topic_slug: whisper-bar
status: draft
created: 2026-10-16
updated: 2026-10-16
tags:
  - wiki
  - whisper-bar
---

# WhisperBar (whisper-bar) — overview

## Summary

WhisperBar is a native macOS menu bar dictation app written in Swift 6, with Deepgram live streaming and optional OpenRouter refinement. API keys are stored in the Keychain, and transcript history is kept locally in SQLite with FTS5 search. Licence: MIT. Repo: [nodaysidle/whisper-bar](https://github.com/nodaysidle/whisper-bar).

## Details

- **Platform:** macOS Apple Silicon (arm64), macOS 14+. No Linux or Windows build.
- **Latest release:** v1.1.2 (published 2026-09-22 01:13 UTC+2). Verified via GitHub Releases on 2026-10-16.
- **Download:** https://github.com/nodaysidle/whisper-bar/releases/download/v1.1.2/WhisperBar.dmg (SHA-256 `7db0c6d5…84da`, from the GitHub asset digest and the hub card).
- **README demo GIF:** yes, `docs/whisperbar.gif` ("WhisperBar: talk faster than you type"). Whether it loads wasn't checked.
- **Requires** your own Deepgram / OpenRouter API keys. The app is ad-hoc signed, not notarized.

## Current status (2026-10-16 20:06 UTC+2)

- **Promo history:** **NOT launched.** Slot: Sat 2026-10-17 17:30 Europe/Ljubljana (Alan 10:27). It's a regular catalog post, not a launch, so the "avoid weekends for launches" rule in [[wiki/concepts/x-promo-strategy]] still stands.
- ⚠️ **REEL warning:** there's no real UI footage (icon and slogan only). The X cuts (owner item 6) may need Alan to capture the HUD. Copy must stay within what's on screen.
- ✅ **Hub card verified** v1.1.2 (SHIP via EO 03:39; [[sessions/handoffs/2026-10-16-ATLAS]], weekend SHIP proposal).
- **Open work:** unknown. No open-work items found beyond the REEL cuts and the Sat draft.

<!-- atlas-2125 -->
## Promo history update 2026-10-16 21:25
- Sat 17 Oct 2026 17:30 X post: **publish APPROVED** (Alan 21:25 via EO). Alan posts it himself. Drafts are due to Alan by 14:00 Sat (standing rule). It is a regular catalog post, not a launch.

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[_system/templates/catalog/whisper-bar]]
- [[wiki/concepts/x-promo-strategy]]
- [[sessions/LATEST]]

## Update 2026-10-16 21:11 (UTC+2) — launch audit (ATLAS)

- ⏳ **Released, not promoted:** no WhisperBar post on X as of 21:11. GitHub Latest v1.1.2 (`7db0c6d5…`) matches the hub card.

<!-- atlas-2133 -->
## README snapshot: source of truth (2026-10-16 21:33)
- Snapshot: [[wiki/sources/whisper-bar-README]] (public `nodaysidle/whisper-bar` @ `2108144`, committed 2026-10-08T22:58:02+02:00). Owner source of truth (Alan 21:32/21:33). Read it first; it wins over older text on this page.
- Local checkout on arch (read-only `git status` at 21:35, no fetch, so the unpushed count may be stale): no local checkout found under `~/dev/nodaysidle/`.
- Local vs GitHub README diff: no local checkout; README listed by SHIP 21:34 under no-local-copy

<!-- atlas-2158 -->
## Promo history update 2026-10-16 21:58
- The Sat 17 Oct 17:30 post is **cleared**: SHIP gate PASS, REACH copy score ≥ 0.85 (per EO 21:58). Publish was approved at 21:25; Alan posts it. Not live yet.

<!-- atlas-2239 -->
## Maintenance status
- Mac app: unmaintained finished build (owner, 2026-10-16). Platform is macOS only.

<!-- atlas-2303 -->
- **README demo GIF:** yes, `docs/whisperbar.gif` loads (HTTP 200, 144 frames) (SHIP 23:00, [[wiki/sources/catalog-audit-2026-10-16]]). This resolves the earlier "not checked".
