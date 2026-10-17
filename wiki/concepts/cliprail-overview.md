---
type: wiki-note
note_kind: concept
topic_slug: cliprail
status: draft
created: 2026-10-17
updated: 2026-10-17
tags:
  - wiki
  - cliprail
---

# ClipRail (cliprail) — overview

## Summary

ClipRail is a local, text-only clipboard history for the macOS menu bar. It keeps recent plain-text clips and up to 3 pinned favorites one click away, with search, delete, pause and re-copy. It makes no network access, needs no account, and never auto-pastes. It is a **finished macOS build, unmaintained** (owner 2026-10-16): no rebuilds, launched as-is.

## Details

- **Platform:** macOS 14+ only (Swift 6, SwiftUI menu bar app). No Linux or Windows build.
- **Version:** 1.2.0. Only release: [`v1.2.0-dmg.20260727`](https://github.com/nodaysidle/cliprail/releases/tag/v1.2.0-dmg.20260727) (published 2026-07-27 02:39 +02:00).
- **Download:** `ClipRail-1.2.0.dmg` (~195 KB) + `.sha256`. SHA-256 `a83120148c67d7a33fb191ae2a373f237c80313b4e584471db29aae464115c0d` (README and SHIP catalog audit agree).
- **Signing:** ad-hoc (no Developer ID, not notarized). On first launch, right-click → Open, or use "Open anyway" in System Settings.
- **Features:** last 10 unpinned clips (newest first); 3 pinned clips that survive Clear; live case-insensitive search; single-row delete; pause with no backfill; 60-second dedupe; relative timestamps; tap a row to re-copy.
- **Privacy:** local UserDefaults only. No URLSession, sockets, telemetry, analytics or sync. No microphone, camera, Accessibility or global-hotkey permissions.
- **Deliberately out of scope:** image history, cloud sync, universal clipboard, automation hooks.

## Current status (2026-10-17)

- README fix merged 2026-10-16 22:59: [PR #5](https://github.com/nodaysidle/cliprail/pull/5), `d8ad7badf1a55d6d05bc8662fb3a55e65fe85685` (direct DMG + `.sha256` link). No new release.
- SCOUT demand score **4/5**, the top of the 2026-10-16 ranking ([[sessions/handoffs/2026-10-16-SCOUT]]).
- **X launch: Tue 3 Nov 2026 17:30** Europe/Ljubljana (confirmed EO 2026-10-16 22:39). Drafts are due to Alan by 14:00 that day.
- No local checkout under `~/dev/nodaysidle/` on arch. No demo GIF in the README (it has a social-preview image only).
- Promo note: REEL had an icon+text clip ready on 2026-10-12 (no real UI footage recorded in the vault).

## Contradictions and gaps

- None found between the README snapshot, the catalog and [[sessions/LATEST]]. Nothing here was re-checked against GitHub live on 2026-10-17.

## Related

- Truth source: [[wiki/sources/cliprail-README]] (`d8ad7ba`)
- Catalog: [[_system/templates/catalog/cliprail]]
- Release audit: [[wiki/sources/catalog-audit-2026-10-16]]
- Promo rules: [[wiki/concepts/x-promo-strategy]]
