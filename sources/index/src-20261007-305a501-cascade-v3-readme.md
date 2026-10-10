---
type: source
source_id: "src-20261007-305a501"
retrieval_method: local-file
url: "https://github.com/nodaysidle/nodaysidle-cascade-v3"
title: "NODAYSIDLE Cascade V3 README"
author: ""
published: ""
accessed: "2026-10-07"
status: active
supersedes: ""
superseded_by: ""
topic_slug: "cascade-v3"
original_path: "README.md"
repo_head: "20f7098"
tags:
  - source
  - primary
  - cascade-v3
---

# Source: NODAYSIDLE Cascade V3 README

## Metadata

- **Kind:** repo-readme
- **Trust tier:** primary
- **Catalog:** [[_system/templates/catalog/cascade-v3]]

## Raw artifact

- File: `sources/raw/docs/src-20261007-305a501-cascade-v3-readme.md` (verbatim copy; repo HEAD `20f7098`, cloned 2026-10-07)

## Key excerpts

- Covers: Tauri 2 app that turns one idea + locked preset into PRD/ARD/TRD/TASKS/AGENTS via one DeepSeek request + local deterministic TS compiler; layer ownership table; features; privacy (memory-only keys, no telemetry); install (macOS DMG 3.1.0, build from source, Arch/Omarchy AppImage/deb); usage; live probe; output files; 5 presets; architecture pipeline; dev scripts; MIT.

## Used by wiki notes

- [[wiki/concepts/cascade-v3-overview]]

## Agent notes

- Self-contradiction: Install says "Apple Silicon only. No Windows, Linux, or Intel macOS build in this release" but the same README has a Linux/Arch section, a Linux badge, and v3.1.0 ships Linux assets.
- Features table says "no retry, no repair pass"; layer table says "at most one repair request" (AGENTS.md and v3.1.0 notes agree with one repair).
- "compiler and audits run entirely on your Mac" — predates Linux support (inferred).
