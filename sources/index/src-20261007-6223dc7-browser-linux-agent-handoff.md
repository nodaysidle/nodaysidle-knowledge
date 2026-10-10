---
type: source
source_id: "src-20261007-6223dc7"
retrieval_method: local-file
url: "https://github.com/nodaysidle/nodaysidle-browser-linux"
title: "Agent handoff — nodaysidle-browser-linux (UNRELIABLE)"
author: ""
published: ""
accessed: "2026-10-07"
status: active
supersedes: ""
superseded_by: ""
topic_slug: "nodaysidle-browser-linux"
original_path: "../nodaysidle-browser-linux/docs/AGENT-HANDOFF.md"
repo_head: "2fffaab"
tags:
  - source
  - secondary
  - nodaysidle-browser-linux
  - unreliable
---

# Source: Agent handoff — nodaysidle-browser-linux (UNRELIABLE)

## Metadata

- **Kind:** local-note
- **Trust tier:** secondary
- **Catalog:** [[_system/templates/catalog/nodaysidle-browser-linux]]

## Raw artifact

- File: `sources/raw/docs/src-20261007-6223dc7-browser-linux-agent-handoff.md` (verbatim copy at repo HEAD `2fffaab`, 2026-10-07)

## ⚠️ Reliability warning

**Known to be partly wrong (per user instruction). Do not cite as authoritative; verify every claim against code or a primary source.** Concrete discrepancies observed during ingest:

- "Open items" says *No git remote and therefore no CI*; the repo has `origin` = `https://github.com/nodaysidle/nodaysidle-browser-linux.git`, and `_audit/log.md` 09:35 records the publish.
- Header says *Last updated: 2026-10-03* but the file was modified 2026-10-05 and mentions later work (Clear Browsing Data, `url_display`).

## Key excerpts

- Covers: project paths, profile data layout, stack (gtk-rs 0.18, webkit2gtk 2.0 crate, no GTK 4 plan), app identity, widget architecture and module map, behaviour notes (tabs, address bar, shortcuts, find bar, fullscreen, pop-ups, teardown, downloads, permissions, error pages, history, cookies), stability rules, build/test commands, open items (macOS parity gaps, pop-up heuristic, untested Wayland app_id).

## Used by wiki notes

- (none yet)
