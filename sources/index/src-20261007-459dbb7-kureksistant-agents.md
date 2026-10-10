---
type: source
source_id: "src-20261007-459dbb7"
retrieval_method: local-file
url: "https://github.com/nodaysidle/kureksistant"
title: "AGENTS.md — Developer & AI Agent Guide for Kurek (JARVIS)"
author: ""
published: ""
accessed: "2026-10-07"
status: superseded
supersedes: ""
superseded_by: "src-20261008-88302c2"
topic_slug: "kureksistant"
original_path: "../kurekizmo/AGENTS.md"
repo_head: "b072178"
tags:
  - source
  - secondary
  - kureksistant
  - agent-guide
---

# Source: AGENTS.md — Developer & AI Agent Guide for Kurek (JARVIS)

## Metadata

- **Kind:** local-note
- **Trust tier:** secondary
- **Catalog:** [[_system/templates/catalog/kurekizmo]] (local folder `kurekizmo`, upstream repo `kureksistant`)

## Raw artifact

- File: `sources/raw/docs/src-20261007-459dbb7-kureksistant-agents.md` (verbatim copy at repo HEAD `b072178`, 2026-10-07)

## Key excerpts

> Never use OpenRouter for Kurek. All DeepSeek calls route straight to `https://api.deepseek.com/chat/completions`.

- Covers: an ASCII architecture diagram (STT, LLM, TTS, "17 Computer Control & Core Tools", memory), a component/file table, env vars, the IDLE/LISTENING/THINKING/SPEAKING state machine, the three-tier memory (`memory/kurek_history.json`, `memory/long_term.json`, Hermes sync to `~/.hermes/profiles/eldio/memories/`), the tool list and dev CLI commands.

## Agent notes (why secondary)

- File links point to `/home/arch/Projects/JARVIS/...`, not to this repo path (14 mentions of JARVIS). The document appears to have been carried over from an earlier project (inferred).
- Says ~60MB RAM and 17 tools; the README says ~55MB and 20.
- Its memory model (JSON files + Hermes) differs from the README's "Muse Memory" (`~/memory/YYYY-MM-DD.md`, `~/MEMORY.md`, `~/ALIGNMENT_SYNTHESIS.md`). It may predate commit `9973462` (inferred).

## Used by wiki notes

- [[wiki/concepts/kureksistant-overview]]
