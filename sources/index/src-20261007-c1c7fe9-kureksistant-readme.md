---
type: source
source_id: "src-20261007-c1c7fe9"
retrieval_method: local-file
url: "https://github.com/nodaysidle/kureksistant"
title: "Kureksistant README"
author: ""
published: ""
accessed: "2026-10-07"
status: superseded
supersedes: ""
superseded_by: "src-20261008-ae52ff2"
topic_slug: "kureksistant"
original_path: "../kurekizmo/README.md"
repo_head: "b072178"
tags:
  - source
  - primary
  - kureksistant
---

# Source: Kureksistant README

## Metadata

- **Kind:** repo-readme
- **Trust tier:** primary
- **Catalog:** [[_system/templates/catalog/kurekizmo]] (local folder `kurekizmo`, upstream repo `kureksistant`)

## Raw artifact

- File: `sources/raw/docs/src-20261007-c1c7fe9-kureksistant-readme.md` (verbatim copy at repo HEAD `b072178`, 2026-10-07)

## Key excerpts

> ~55MB headless local daemon summoned in sub-second time via mouse Middle-Click (`mouse:274`) or Fn key

- Covers:
  - pitch: a headless daemon on `127.0.0.1:8790`, ~55MB RAM;
  - install from the v0.1.0 tarball or from source (`install_linux.sh`), plus the macOS `KurekBar.swift` menu bar app;
  - `.env` keys: DEEPSEEK and XAI required; GEMINI, DEEPGRAM and TYPESAFE optional;
  - Linux dependencies: mpv, notify-send, grim, wl-clipboard;
  - known limits, Hyprland bindings, the `kurek` CLI and capabilities (Muse Memory, TypeSafe Jev, screen vision, process_sentinel, draft_to_clipboard, workstation_radar, dream_tool, resource watcher, Hermes sync);
  - a mermaid architecture diagram, the three-phase "Evolution" history, and a license line saying MIT.

## Agent notes

- The README footer says "MIT © Alan Pfeifer (NODAYSIDLE)", but the repo `LICENSE` file is **CC BY-NC 4.0** and carries the header "MARK 53 — JARVIS / Copyright (c) 2026 FatihMakes" (agent check). Contradiction; licence and attribution are unresolved.
- The tool count is stated as "20 native system tools" and "20+"; `AGENTS.md` says 17. `actions/` holds 28 tool modules plus `__init__.py` (agent check).
- File creation is described as "unrestricted", with spoken confirmation only for deletion. This is a security posture worth reviewing.

## Used by wiki notes

- [[wiki/concepts/kureksistant-overview]]
