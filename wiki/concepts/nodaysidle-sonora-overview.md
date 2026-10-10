---
type: wiki-note
note_kind: concept
topic_slug: nodaysidle-sonora
status: draft
created: 2026-10-07
updated: 2026-10-08
tags:
  - wiki
  - nodaysidle-sonora
---

# NODAYSIDLE Sonora — overview

## Summary

Sonora is a Tauri v2 + Rust + React 19 desktop music player that combines local files, Spotify and YouTube Music in one queue. It offers gapless playback, EBU R128 (-14 LUFS) loudness normalization, and LRCLIB synced lyrics with romanization. It ships for macOS Apple Silicon and Linux. Licence: MIT.

## Details

- **Audio:** symphonia + cpal, a 5 s pre-roll for gapless playback, EBU R128 normalization, and a SQLite FTS5 library index (lofty for tags).
- **Spotify path (disputed, see below):** the root AGENTS.md, which declares itself the source of truth, says Spotify plays natively through Librespot. The latest commit `b2f9a2d` (2026-09-24) says "Spotify via Spotify Connect with YouTube fallback".
- **Docs hierarchy:** root AGENTS.md overrides the older planning docs (PRD, ARD, TRD, TASKS, docs/AGENTS.md). TASKS.md is historical.
- **Releases:**
  - v0.1.0 (2026-09-15)
  - v0.1.1 (2026-09-16; rpm, dmg, AppImage, deb, app.tar.gz)
  - 12 commits in total. ⚠️ Stale as of 2026-10-08: `f34945b`, `2c0e052` and `e3add87` have landed since; `main` = `e3add87`.

## Contradictions & gaps

1. **Spotify playback:** three different descriptions.
   - README: Spotube-style; metadata from Spotify, audio resolved via YouTube Music/yt-dlp.
   - Root AGENTS.md and the librespot plan/spec: native Librespot.
   - Latest commit: Spotify Connect with YouTube fallback.
   
   Current behaviour is unverified; reading the code is needed.
2. **Platforms:** PRD, docs/AGENTS.md and codemap claim Windows; README and releases cover macOS + Linux only.
3. **RAM target:** ARD says sub-90MB, docs/AGENTS.md <100MB, README ~102/<105MB, the librespot plan <120MB.
4. **Versions:** the README header links v0.1.1, but the Install section names v0.1.0 files. rpm assets exist but aren't mentioned.
5. **Stale paths:** codemap lists the planning docs at the repo root (they moved to `docs/` in `e1c3130`). AGENTS files point to `/Volumes/omarchyuser/projekti/sonora`.
6. **TASKS.md:** only 3 of 32 tasks are ticked, despite shipped releases. Root AGENTS.md calls it historical.
7. **Duplicate:** `docs/AGENT.md` is identical to `docs/AGENTS.md`; ingested once.
8. **Thin release notes:** the v0.1.1 body is a single line. ✅ Resolved 2026-10-08 22:24: SHIP rewrote the v0.1.1 body (Linux Spotify sign-in fix, docs cleanup, download table, SHA-256s). Verified 22:30.

## Claims & citations

| Claim | Source |
|-------|--------|
| Features, performance claims, Spotube resolver, platforms | [[sources/index/src-20261007-fa15609-nodaysidle-sonora-readme]] |
| Source of truth, Librespot, TASKS historical | [[sources/index/src-20261007-8d170be-nodaysidle-sonora-agents]] |
| Windows claim, <100MB | [[sources/index/src-20261007-7396417-nodaysidle-sonora-docs-agents]], [[sources/index/src-20261007-02f8cee-nodaysidle-sonora-prd]] |
| sub-90MB, stack rationale | [[sources/index/src-20261007-72f03ba-nodaysidle-sonora-ard]] |
| Data models | [[sources/index/src-20261007-6bd63ba-nodaysidle-sonora-trd]] |
| 3 of 32 tasks ticked | [[sources/index/src-20261007-db207e8-nodaysidle-sonora-tasks]] |
| Style tokens, commands | [[sources/index/src-20261007-c7ca7e6-nodaysidle-sonora-claude]] |
| Stale root paths | [[sources/index/src-20261007-0876748-nodaysidle-sonora-codemap]] |
| Librespot plan, <120MB | [[sources/index/src-20261007-f4f351a-nodaysidle-sonora-plan-librespot]] |
| Spotify Connect needed an external client before librespot | [[sources/index/src-20261007-91e96aa-nodaysidle-sonora-spec-librespot]] |
| Releases and assets | [[sources/index/src-20261007-4ac28d4-nodaysidle-sonora-github-releases]] |
| Commits, latest Spotify change | [[sources/index/src-20261007-7234e1e-nodaysidle-sonora-git-log]] |

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[_system/templates/catalog/nodaysidle-sonora]]

## Verdict: Spotify playback at HEAD `b2f9a2d` (code read 2026-10-07 13:58 UTC+2)

**Spotify Connect first, falling back to YouTube.** The bundled Librespot player is compiled in but not wired up. This settles contradiction #1: the README (YouTube-only) and root AGENTS.md (Librespot) are both wrong about the primary path. The latest commit message is right.

| # | Finding | Evidence | Label |
|---|---------|----------|-------|
| 1 | The app state holds a `SpotifyConnectPlayer`; it is created and attached at startup | `src-tauri/src/lib.rs:33`, `:707–708` | observed |
| 2 | The `spotify_play` command stops Sonora's own audio engine and calls `spotify_player.play_track` | `src-tauri/src/lib.rs:510–518` | observed |
| 3 | `play_track` → `provider.play_remote` → Web API `PUT /me/player/play` on the user's Spotify device | `src-tauri/src/providers/spotify/connect_player.rs:104–116`; `src-tauri/src/providers/spotify.rs:886–897` | observed |
| 4 | Module doc says Spotify refuses librespot the audio keys for many Premium accounts (librespot#1649), "so an official Spotify client has to render the audio" | `connect_player.rs:1–5` | observed |
| 5 | Frontend tries `spotifyPlay` first; on error it shows "Spotify app unavailable … Playing via YouTube" and sets `spotifyRoute = 'youtube'` | `src/stores/playerStore.ts:152–161` | observed |
| 6 | The YouTube path resolves a stream via `spotify_resolve_stream` → `YouTubeMusicProvider::resolve_stream_for_track(title, artist, duration)` and plays it in Sonora's engine | `playerStore.ts:52–57`, `:165–167`; `lib.rs:628–636` | observed |
| 7 | `NativeSpotifyPlayer` (librespot 0.8) exists and the `librespot` dependency is declared, but `lib.rs` has 0 references to it | `src-tauri/src/providers/spotify/native_player.rs:263`; `src-tauri/Cargo.toml:41`; `rg NativeSpotifyPlayer lib.rs` returns 0 | observed |
| 8 | So the Librespot path is dead code at HEAD and Spotify audio comes from the user's Spotify client | from #1–#7 | inferred |
| 9 | Stale comment: `tauriBridge.ts:233` documents the next bridge method as "Starts the native Librespot player", but `spotifyPlay` invokes `spotify_play`, which uses Connect | `src/services/tauriBridge.ts:233–235` | observed |

Not run (no build, no runtime test). The fallback applies only when `spotifyPlay` throws, for example when no Spotify device is available.

## Decisions and fixes (user, 2026-10-07 14:07 UTC+2; commit `f34945b`, push pending authentication)

- **Playback docs:** README, root AGENTS.md and the `tauriBridge.ts` comment now describe Spotify Connect with a YouTube fallback.
- **Librespot player not removed:** `connect_player.rs` imports `normalize_spotify_id` and `EVENT_SPOTIFY_PLAYBACK_STATE` from `native_player.rs`, so removing it would mean moving code. Not a clean removal; left as is.
- **Windows claims** removed (PRD, ARD, TRD, TASKS, docs/AGENTS.md, codemap).
- **RAM:** the target is <90MB everywhere. README keeps the measured ~102MB figure, labelled as measured, next to the target.
- **README links:** now v0.1.1, and the rpm is mentioned.
- **Paths:** `/Volumes` paths removed; codemap paths now point to `docs/`. The duplicate `docs/AGENT.md` is deleted.
- **TASKS.md:** 19 tasks ticked from code evidence (22 of 32 ticked in total). Unverified and left unticked:
  - 3.3: uses a custom R128 implementation, not the `ebur128` crate;
  - 4.1 to 4.4;
  - 7.2 to 7.4;
  - 8.3 and 8.4.

## Librespot player removed (2026-10-07 14:24 UTC+2; commit `2c0e052`, push waiting on user)

- **Code:**
  - Deleted `providers/spotify/native_player.rs`.
  - Moved `normalize_spotify_id`, with its 3 tests, and `EVENT_SPOTIFY_PLAYBACK_STATE` into `providers/spotify.rs`. Base62 validation is now a 22-character alphanumeric check instead of librespot's `SpotifyId`.
  - Removed the librespot-only OAuth helpers and constants. `clear_tokens` still deletes any leftover `librespot_tokens.json`.
- **Dependency:** removed the `librespot` dependency. Cargo.lock lost 102 packages and added none.
- **Checks:** `cargo check` passes with 0 warnings. `cargo clippy` passes with no new warnings. `cargo test`: 82 passed, 2 ignored, plus 2 + 3 integration tests.
- **Docs:** `AGENTS.md` and `docs/codemap.md` no longer mention the unwired player. The old librespot plan under `docs/superpowers/` is left as history.

## Current status (2026-10-08 22:30 UTC+2)

Verified against the public GitHub API by Grok Bot (ATLAS) during [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]]. Newer facts here take precedence over Details.

- **Repo:** public. `main` = `e3add87` (README promo GIF, PR #2, merged 2026-10-07 22:54). No open PRs, no GitHub homepage URL. Licence MIT.
- **Latest release:** v0.1.1 (published 2026-09-16 03:59) with `Sonora_0.1.1_aarch64.dmg`, `Sonora_aarch64.app.tar.gz`, `Sonora_0.1.1_amd64.AppImage`, `Sonora_0.1.1_amd64.deb` and `Sonora-0.1.1-1.x86_64.rpm`.
- **Release notes rewritten 2026-10-08 (SHIP, edited 22:24):** "Linux Spotify sign-in fix" with Fixes and Docs sections, a download table for all 5 files, and SHA-256s that match the GitHub asset digests. https://github.com/nodaysidle/nodaysidle-sonora/releases/tag/v0.1.1
- **Demo GIF:** `docs/sonora.gif` is in the README and loads.
- ⚠️ **Conflict, visibility history:** SWEEP said the repo was private on 2026-10-07 and flipped public, perhaps around the 2026-10-07 ~22:54 pushes. This vault recorded it public via the API at 2026-10-07 13:55. The flip time is unknown.
- **Showcase:** listed on the official portfolio (nodaysidle-portfolio-nine.vercel.app).
