---
type: source-readme
repo: "nodaysidle/batchrename-pro"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "bff7b4763f53478ce6b7c6309c5ae44fbec82216"
source_commit_date: "2026-09-18T01:17:37+02:00"
readme_path: "README.md"
readme_blob_sha: "50ef3578462b002c95c2342ac0f90334a5dcc84a"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/batchrename-pro/blob/bff7b4763f53478ce6b7c6309c5ae44fbec82216/README.md"
tags: [source, readme, batchrename-pro]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/batchrename-pro` at `bff7b47` (2026-09-18T01:17:37+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<p align="center">
  <img src="https://raw.githubusercontent.com/nodaysidle/batchrename-pro/bff7b4763f53478ce6b7c6309c5ae44fbec82216/src-tauri/icons/128x128.png" width="128" height="128" alt="BatchRename Pro icon">
</p>

<h1 align="center">BatchRename Pro</h1>

<p align="center">
  <strong>Batch rename files safely in one local-first desktop app.</strong><br>
  No cloud. No scripts.
</p>

<p align="center">
  <img alt="macOS Apple Silicon" src="https://img.shields.io/badge/macOS-Apple%20Silicon-black?style=flat-square&logo=apple&logoColor=white">
  <img alt="v0.1.0" src="https://img.shields.io/badge/v0.1.0-release-6B6B80?style=flat-square">
  <img alt="Tauri 2" src="https://img.shields.io/badge/Tauri-2.0-24C8DB?style=flat-square&logo=tauri">
  <img alt="Rust" src="https://img.shields.io/badge/Rust-2021-orange?style=flat-square&logo=rust">
  <img alt="MIT" src="https://img.shields.io/badge/license-MIT-green?style=flat-square">
</p>

<p align="center">
  <a href="https://github.com/nodaysidle/batchrename-pro/releases/download/v0.1.0/BatchRename-Pro-0.1.0-aarch64.dmg"><strong>Download Apple Silicon DMG (v0.1.0)</strong></a>
  ·
  <a href="https://github.com/nodaysidle/batchrename-pro">GitHub</a>
</p>

<p align="center">
  <em>Apple Silicon · ad-hoc signed / not notarized</em>
</p>

## Overview

BatchRename Pro handles file renaming operations through regex patterns, template tokens, and sequential numbering — with live preview, conflict blocking, backup, and full undo. Ships as a Tauri desktop app with dark and light themes.

## Features

- **Batch rename** — regex patterns, template tokens (`{date}`, `{number}`, `{original}`, `{ext}`), sequential numbering with zero-padding, case transforms
- **Live preview** — see results before anything touches disk
- **Conflict blocking** — detects name collisions before applying
- **Undo** — every operation creates a backup; full rollback from SQLite-backed job history
- **Drag-drop input** — drop files or folders directly
- **Accent themes** — volt and graphite

Format conversion and metadata editing are **not shipped** in v0.1.0 (backlog). Convert/Metadata tabs are not shown.

## Technology

| Area | Technology |
|------|------------|
| Shell | Tauri 2 |
| Frontend | Vite 6, React 19, TypeScript, Tailwind CSS 4 |
| Backend | Rust 2021, sequential rename apply |
| Storage | SQLite via rusqlite (WAL mode), FTS5 |

## Requirements

- Node.js 20 or later
- Rust stable 1.75 or later
- Xcode CLI Tools (macOS)

## Installation

1. Download [`BatchRename-Pro-0.1.0-aarch64.dmg`](https://github.com/nodaysidle/batchrename-pro/releases/download/v0.1.0/BatchRename-Pro-0.1.0-aarch64.dmg) (Latest = v0.1.0).
2. Open the DMG and drag `BatchRename Pro.app` to `/Applications`.
3. First launch: right-click → **Open** if Gatekeeper blocks it (ad-hoc / not notarized).

- SHA256: `ef6e33a03881430c329fd9fd888cf4010142598010a89b535cf0eb2c3948309b`

## Development

```bash
git clone https://github.com/nodaysidle/batchrename-pro.git
cd batchrename-pro
npm install
npx tauri dev
```

Production build:

```bash
npm run build && npx tauri build
```

Release binary: `src-tauri/target/release/bundle/macos/BatchRename Pro.app`

## Architecture

```
┌─────────────────────────────────────────────────┐
│  WebView (React 19 + TypeScript + Tailwind CSS) │
│  DropZone │ FileList (virtualized) │ TransformPanel │
│                   ActionFooter                   │
└──────────────────┬──────────────────────────────┘
                   │ Tauri IPC
┌──────────────────┴──────────────────────────────┐
│  Rust Backend                                   │
│  Preview Service │ File Service │ Processing Pipeline (sequential apply) │
│  SQLite (WAL)    │ Convert/Metadata (not shipped) │
└─────────────────────────────────────────────────┘
```

## UI

Dark mode default with light theme support. Glassmorphic design. Two accent themes — volt and graphite.

- Drag-drop zone with animated states
- Virtualized file list (react-window) for 100+ files
- Right sidebar: Rename panel (convert/metadata not shipped)
- Sticky action footer with Apply, Undo, History (History stays reachable with zero files)
- Appearance controls for theme and accent (not a full Settings suite)

## Status

v0.1.0 — Rename workflow complete. Format conversion and metadata editing are not shipped.

## Contributing

This repository is not currently accepting external contributions.

## License

MIT
