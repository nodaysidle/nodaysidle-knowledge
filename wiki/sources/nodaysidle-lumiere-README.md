---
type: source-readme
repo: "nodaysidle/nodaysidle-lumiere"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "c9a1305f4f7d77069783ca2994c13e10f1785d24"
source_commit_date: "2026-10-16T23:26:52+02:00"
readme_path: "README.md"
readme_blob_sha: "c8dc885be7da6ca5244b54b0aae554158aa9af4c"
fetched: "2026-10-16T23:30:12+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/nodaysidle-lumiere/blob/c9a1305f4f7d77069783ca2994c13e10f1785d24/README.md"
tags: [source, readme, nodaysidle-lumiere]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/nodaysidle-lumiere` at `c9a1305` (2026-10-16T23:26:52+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<img src="https://raw.githubusercontent.com/nodaysidle/nodaysidle-lumiere/c9a1305f4f7d77069783ca2994c13e10f1785d24/github/social-preview.png" alt="Lumiere — NODAYSIDLE" width="100%">

# Lumiere

> Native macOS screenshot polish and annotation — local-first, no network, no accounts.

![Platform](https://img.shields.io/badge/platform-macOS%2015%2B-black?style=flat-square&logo=apple)
![Swift](https://img.shields.io/badge/Swift-6.0-FA7343?style=flat-square&logo=swift)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

![Lumiere Logo](https://raw.githubusercontent.com/nodaysidle/nodaysidle-lumiere/c9a1305f4f7d77069783ca2994c13e10f1785d24/Lumiere/Resources/Brand/LumiereLogo.svg)

## Overview

Lumiere is a native macOS app for turning clipboard screenshots into clean, annotated exports. It watches for copied images, applies local image cleanup, provides vector annotation tools, and exports PNG/JPEG/HEIC — all on-device with no network or backend dependencies.

## Features

- **Auto-capture** — clipboard monitoring detects screenshots and copied images automatically
- **Shadow styling** — apply directional shadow depth to screenshots
- **Perspective correction** — auto-detect document edges and correct perspective with Vision framework
- **Vector annotations** — arrow, rectangle, text, callout, and blur tools
- **Floating toolbar** — glass-panel NSPanel with cursor-proximity reveal and hide
- **Export** — PNG (lossless), JPEG, and HEIC output
- **Local-first** — no cloud, no telemetry, no accounts
- **Dark Volt UI** — NODAYSIDLE dark theme with `#C8FF00` accent

## Technology

| Area | Technology |
|------|------------|
| Language | Swift 6 |
| Interface | SwiftUI + AppKit (NSPanel, NSPasteboard, NSSavePanel) |
| Build | Xcode project (`xcodebuild`) |
| Image Processing | Core Image, Vision framework |
| Machine Learning | Core ML (heuristic fallback — no `.mlmodel` required) |
| Storage | SwiftData |
| Events | Combine |

## Requirements

- macOS 15.0 or later
- Xcode 16+ / Swift 6+
- Apple Silicon recommended

## Installation

The latest release ([v0.1.1](https://github.com/nodaysidle/nodaysidle-lumiere/releases/tag/v0.1.1)) has no downloadable assets. The newest pre-built app is [`Lumiere-v0.1.0-macos.dmg`](https://github.com/nodaysidle/nodaysidle-lumiere/releases/download/v0.1.0/Lumiere-v0.1.0-macos.dmg) on [v0.1.0](https://github.com/nodaysidle/nodaysidle-lumiere/releases/tag/v0.1.0) (no checksum file is attached).

1. Open the DMG and drag `Lumiere.app` to `/Applications`
2. **Right-click → Open** on first launch to bypass Gatekeeper

Or build from source (macOS 15+, Xcode):

```bash
Scripts/package-internal-dmg.sh
open build/Lumiere-Internal-AdHoc.dmg
```

The DMG is **not Developer ID signed or notarized**. For NDI/Kaly internal use and trusted installs only.

## Development

```bash
# Debug build
xcodebuild -project Lumiere.xcodeproj -scheme Lumiere -configuration Debug -derivedDataPath build/DebugDerivedData build

# Run tests (8 tests)
xcodebuild -project Lumiere.xcodeproj -scheme Lumiere -destination 'platform=macOS' -derivedDataPath build/TestDerivedData test

# Internal DMG
Scripts/package-internal-dmg.sh
```

## Project Structure

```text
Lumiere/
├── Core/                    Logging, services, theme
│   ├── Services/            ClipboardMonitor, ImageProcessing, CoreML, Annotations, Settings
│   └── Theme/               Color+Palette (Volt #C8FF00)
├── Features/
│   ├── UI/                  Views (ImageDisplay, GlassPanel, DrawingLayer, AnnotationInput), PanelManager
│   └── Settings/            SettingsView
├── Models/                  Annotation, ImageProcessing, CaptureEvent, Settings types
└── Resources/               AppIcon, LumiereLogo.svg
```

## Privacy

Lumiere is intentionally local-first:

- No network calls
- No cloud processing
- No telemetry
- No accounts
- All image processing happens on-device
- Clipboard access is read-only; no clipboard data is persisted beyond the current session

## License

MIT.

## Author

[NODAYSIDLE](https://github.com/nodaysidle)
