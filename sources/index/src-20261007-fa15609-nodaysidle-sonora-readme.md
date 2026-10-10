---
type: source
source_id: "src-20261007-fa15609"
retrieval_method: local-file
url: "https://github.com/nodaysidle/nodaysidle-sonora"
title: "NODAYSIDLE Sonora README"
author: ""
published: ""
accessed: "2026-10-07"
status: active
supersedes: ""
superseded_by: ""
topic_slug: "nodaysidle-sonora"
original_path: "README.md"
repo_head: "b2f9a2d"
tags:
  - source
  - primary
  - nodaysidle-sonora
---

# Source: NODAYSIDLE Sonora README

## Metadata

- **Kind:** repo-readme
- **Trust tier:** primary
- **Catalog:** [[_system/templates/catalog/nodaysidle-sonora]]

## Raw artifact

- File: `sources/raw/docs/src-20261007-fa15609-nodaysidle-sonora-readme.md` (verbatim copy; repo HEAD `b2f9a2d`, cloned 2026-10-07)

## Key excerpts

- Covers: Tauri v2 + Rust + React 19 music player unifying local files, Spotify, YouTube Music; performance claims (~102 MB idle, ~2% CPU on M4); features (symphonia+cpal, 5s pre-roll gapless, EBU R128 -14 LUFS, LRCLIB lyrics + romanization, SQLite FTS5); architecture; Spotube-style resolver (Spotify metadata, audio via YouTube Music/yt-dlp); privacy; install; dev.

## Used by wiki notes

- [[wiki/concepts/nodaysidle-sonora-overview]]

## Agent notes

- Describes Spotify audio as resolved via YouTube (Spotube-style); root AGENTS.md says Spotify plays natively through Librespot, latest commit b2f9a2d says Spotify Connect with YouTube fallback.
- Header links v0.1.1 downloads; Install section still names v0.1.0 files.
- Platforms: macOS + Linux only (PRD/docs AGENTS.md also claim Windows).
