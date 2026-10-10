---
type: wiki-note
note_kind: concept
topic_slug: x-promo
status: draft
created: 2026-10-08
updated: 2026-10-08
tags:
  - wiki
  - x-promo
  - reel
---

# REEL clip workflow (promo MP4 + README GIF)

## Summary

REEL is a Grok Bot agent that turns a nodaysidle repo into a 10–20s promo MP4 for X and a looping README GIF under 5MB. It uses only real assets: screenshots, the icon, README text, and footage of Linux AppImages. REACH requests clips proactively for every drafted post. Adlof previews each clip, then the GIF is added to the repo README through a pull request and merged.

## Workflow

1. **Request:** REACH messages REEL with the repo, the post angle, and the post date.
2. **Build:** REEL records real footage where it can (Linux AppImages). For macOS-only apps it builds from the icon and README text, because Adlof is on Linux and can't record macOS apps. REEL flags anything the clip can't honestly show.
3. **Copy check:** REACH adjusts the post copy so it claims only what the clip shows.
4. **Preview:** REACH sends Adlof the MP4 and GIF before the post's slot.
5. **README:** after approval, a Cursor cloud agent commits the GIF as `docs/<app>.gif` and puts it as the README hero under the title, then opens a PR. REACH merges it and checks that the raw GIF URL returns 200.
6. **Post:** Adlof posts on X with the MP4 attached.

## Clips produced (2026-10-07)

Stored on the Grok Bot computer under `/workspace/clips/<app>/` (not on this machine).

| App | Files | Source of footage | Notes |
|-----|-------|-------------------|-------|
| WhisperBar | `whisperbar.mp4` (12s, 1080²), `whisperbar.gif` (4.7MB) | icon + README text | macOS-only; no menu-bar or streaming footage |
| ShareGuard | `shareguard.mp4`, `shareguard.gif` | icon + README masked examples | macOS-only; proprietary licence |
| Browser (Linux) | `browser-linux.mp4`, `browser-linux.gif` | real AppImage footage (tabs, Ctrl+F) | needs system GTK3 + WebKitGTK 4.1 |
| Cascade | `cascade.mp4`, `cascade.gif` | real footage: idea typed, five doc tabs | generation needs API keys; "five docs out" is a caption |
| Sonora | `sonora.mp4` (13.6s, 1080p), `sonora.gif` (3.8MB) | real UI screenshot + AppImage Connect views | explicit track title pixelated; YouTube needs yt-dlp |

## README GIF PRs (merged 2026-10-07)

| Repo | PR | Merge commit | GIF path |
|------|----|--------------|----------|
| whisper-bar | #1 | `becc15a` | `docs/whisperbar.gif` (replaced AppIcon hero) |
| nodaysidle-cascade-v3 | #2 | `9e38b03` | `docs/cascade.gif` |
| nodaysidle-sonora | #2 | `e3add87` | `docs/sonora.gif` |
| nodaysidle-shareguard | #3 | `fc8bb3d` | `docs/shareguard.gif` (replaced social-preview hero) |
| nodaysidle-browser-linux | #1 | `a813e70` | `docs/browser-linux.gif` (branch `master`) |

Local clones under `/home/arch/dev/nodaysidle/` are now one commit behind origin for these repos. Run `git pull` before the next local commit.

## Earlier asset

- kureksistant v0.1.0: `docs/demo.gif` (~106KB) in the README hero, made by the owner's coding agent from REACH's prompt (2026-10-06).

## Related

- [[wiki/MOC/moc-x-promo]]
- [[wiki/concepts/x-promo-strategy]]
- [[wiki/concepts/x-promo-calendar-2026-10]]

## Open questions

- Real macOS screen recordings for WhisperBar and ShareGuard would beat icon-and-text clips if a Mac becomes available.
- Clips still needed: Synapse Notes (20 Oct), ClipRail (22 Oct).
