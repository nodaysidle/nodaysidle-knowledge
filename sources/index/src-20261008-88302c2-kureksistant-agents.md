---
type: source
source_id: "src-20261008-88302c2"
retrieval_method: local-file
url: "https://github.com/nodaysidle/kureksistant"
title: "AGENTS.md — Developer & AI Agent Guide for Kurek (v0.1.0 update)"
author: ""
published: ""
accessed: "2026-10-08"
status: active
supersedes: "src-20261007-459dbb7"
superseded_by: ""
topic_slug: "kureksistant"
original_path: "../kurekizmo/AGENTS.md"
repo_head: "d863922"
tags:
  - source
  - primary
  - kureksistant
  - agent-guide
---

# Source: AGENTS.md — Developer & AI Agent Guide for Kurek (v0.1.0 update)

## Metadata

- **Kind:** local-note
- **Trust tier:** primary
- **Catalog:** [[_system/templates/catalog/kurekizmo]] (local folder `kurekizmo`, upstream repo `kureksistant`)

## Raw artifact

- File: `sources/raw/docs/src-20261008-88302c2-kureksistant-agents.md` (verbatim copy at repo HEAD `d863922`, 2026-10-08)

## Key excerpts

> Kurek is an ultra-fast headless personal AI assistant for Arch Linux / Omarchy Quattro (Hyprland) and macOS (~333MB RAM with default faster-whisper STT; lower without Whisper). Features instant Middle Click mouse summon, native desktop launcher, DeepSeek-Flash reasoning, xAI Grok speech (Sol voice), Hermes bidirectional memory continuity, and 24 tool modules in `actions/`.

- Covers:
  - Architecture diagram detailing 127.0.0.1:8790 daemon, STT (Deepgram/Whisper), DeepSeek-Flash, xAI Grok TTS;
  - 24 native system tools in `actions/`;
  - 3-tier Muse Memory + Hermes bidirectional continuity sync;
  - Component table and CLI operations.

## Agent notes

- Supersedes `src-20261007-459dbb7`: Removed legacy JARVIS hardcodes, aligned tool count to 24 and memory model to Muse Memory (~333MB RAM), and updated paths to repository-relative links. Promoted to trust tier primary.

## Used by wiki notes

- [[wiki/concepts/kureksistant-overview]]
