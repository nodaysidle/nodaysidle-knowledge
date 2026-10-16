---
type: source-readme
repo: "nodaysidle/excalidays"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "2e3a41a1e14822b52b1a0556890f374b7d67d029"
source_commit_date: "2026-09-18T00:56:39+02:00"
readme_path: "README.md"
readme_blob_sha: "70bbd5bd701b30a4f90eef6cff92e7531b14f29b"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/excalidays/blob/2e3a41a1e14822b52b1a0556890f374b7d67d029/README.md"
tags: [source, readme, excalidays]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/excalidays` at `2e3a41a` (2026-09-18T00:56:39+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<div align="center">
  <img src="https://raw.githubusercontent.com/nodaysidle/excalidays/2e3a41a1e14822b52b1a0556890f374b7d67d029/Excalidays/Resources/Assets.xcassets/AppLogo.imageset/AppLogo.png" width="144" alt="Excalidays logo">
  <h1>Excalidays</h1>
  <p><strong>Local-first native macOS Excalidraw document app.</strong></p>
  <p>New / Open <code>.excalidraw</code> → edit in a local canvas → Save. Files stay on your Mac.</p>

  <p>
    <a href="https://github.com/nodaysidle/excalidays/releases/download/v0.1.0/Excalidays-0.1.0.dmg"><strong>Download v0.1.0 DMG</strong></a>
    ·
    <a href="https://github.com/nodaysidle/excalidays/releases/tag/v0.1.0">v0.1.0 release</a>
    ·
    <a href="https://github.com/nodaysidle/excalidays/releases">All releases</a>
  </p>

  <p>
    <img src="https://img.shields.io/badge/macOS-14%2B-111111?logo=apple" alt="macOS 14 or later">
    <img src="https://img.shields.io/badge/Swift-6-F05138?logo=swift&logoColor=white" alt="Swift 6">
    <img src="https://img.shields.io/badge/UI-AppKit%20%2B%20SwiftUI-0A84FF" alt="AppKit and SwiftUI">
    <img src="https://img.shields.io/badge/Excalidraw-0.18.1-6965db" alt="Excalidraw 0.18.1">
    <img src="https://img.shields.io/badge/phase-0%2F1-2ea44f" alt="Phase 0/1">
    <img src="https://img.shields.io/badge/iOS-not%20supported-lightgrey" alt="Not iOS">
  </p>
</div>

<p align="center"><em><code>main</code> is ahead of the public <strong>v0.1.0</strong> DMG. That download is still Phase 0/1 only — not a Phase 2 release.</em></p>

<p align="center">
  <img src="https://raw.githubusercontent.com/nodaysidle/excalidays/2e3a41a1e14822b52b1a0556890f374b7d67d029/docs/screenshots/packaged-release-working.png" width="720" alt="Excalidays editing an Excalidraw document on macOS">
</p>

macOS only. Native AppKit/SwiftUI document shell with a pinned local Excalidraw WKWebView — not iOS, not a web app, not a cloud product.


## The journey

One loop (Phase 0/1):

```text
New / Open .excalidraw
  → NSDocument owns the file
  → local WKWebView loads bundled Excalidraw 0.18.1
  → draw / edit
  → Save (native dirty + snapshot)
```

| Stage | What happens |
|---|---|
| **New / Open** | Standard macOS document flow creates or opens a `.excalidraw` file. |
| **Document** | `NSDocument` (`ExcalidaysDocument`) owns bytes, dirty state, and safe save. |
| **Canvas** | One isolated local `WKWebView` per document loads the bundled Excalidraw runtime (no CDN). |
| **Edit** | Drawing stays Excalidraw; the shell forwards undo/redo and tracks dirty via a typed bridge. |
| **Save** | Explicit snapshot round-trips scene / files / compatible unknown fields back to disk. |

## What it does (Phase 0/1)

- Create, open, edit, and save `.excalidraw` documents on macOS 14+
- Real `NSDocument` / window lifecycle with native dirty indication
- Bundled local Excalidraw 0.18.1 + fonts (offline canvas; CSP `connect-src 'none'`)
- Typed canvas bridge with operation allowlist; undo/redo menu forwarding
- Ad-hoc packaged `.app` / DMG for local install

## What it does **not** (yet)

Phases **2–7** are not shipped as product releases:

| Phase | Not shipped |
|---|---|
| **2** | **Not a shipped release.** On `main` only: Finder open path **PARTIAL**; native menus/toolbar present; Organizer is a local catalog **side door into Open** (**PARTIAL**). Settings still out. Phase 2 overall **not done**. |
| **3** | Image / SVG / PDF import workflows |
| **4** | PNG / SVG / PDF / pasteboard export workflows |
| **5** | In-app history / checkpoints |
| **6** | Full interaction, accessibility, and performance evidence |
| **7** | Notarized Developer ID release |

Also out of scope forever for this product shape: **accounts, cloud sync, collaboration, analytics, AI drawing, iOS / mobile**.

Organizer on `main` is a local SwiftData catalog side door into Open (recents / favorites / tags / thumbs / workspaces where present). It is **not** Settings, **not** sync, and **not** a completed Phase 2 product. The public **v0.1.0** DMG does not include it.


## Format truth

| Format | Behavior in Excalidays |
|---|---|
| `.excalidraw` | Editable. Official runtime restore/serialize; preserve elements, app state, files, attachments, compatible unknown top-level fields. |
| Scene-embedded PNG/SVG | Detected and editable **when** Phase 3 lands — **not** shipped in 0.1.0. |
| Ordinary PNG/JPEG/WebP/GIF/HEIC/SVG | Become **image elements** when import lands — pixels/paths are **not** native Excalidraw shapes. **Not** shipped in 0.1.0. |
| PDF pages | Bounded **image elements** via PDFKit when import lands — no OCR / vector-to-shape. **Not** shipped in 0.1.0. |

## Stack

| Layer | Technology |
|---|---|
| Shell | AppKit + SwiftUI, Swift 6, macOS 14+ |
| Documents | NSDocument / NSDocumentController |
| Build | XcodeGen (project.yml) + xcodebuild |
| Canvas | Local WKWebView + bundled @excalidraw/excalidraw 0.18.1 |
| Canvas build | Node and Vite |
| Isolation | sandboxed; user-selected files; bookmarks; WebKit JIT |

## Network entitlement note

The app includes `com.apple.security.network.client` because WebKit/JIT sandboxes often require it. **Excalidays is not a cloud product**: the canvas is bundled locally, remote script/font/CDN fallbacks are denied, and there are no accounts, sync, or analytics. See `SECURITY.md` and `THIRD_PARTY_NOTICES.md`.


## Releases

Public **v0.1.0** ships an ad-hoc signed DMG (not notarized).

<!-- Updated after gh release create with the real asset URL -->

- **Download:** [`Excalidays-0.1.0.dmg`](https://github.com/nodaysidle/excalidays/releases/download/v0.1.0/Excalidays-0.1.0.dmg)
- **Release page:** https://github.com/nodaysidle/excalidays/releases/tag/v0.1.0
- **Tag:** `v0.1.0`
- First launch on a fresh Mac: Control-click — **Open** — confirm (Gatekeeper + ad-hoc signature).

## Build from source

Requirements: macOS 14+, Xcode / Swift 6 toolchain, Node 22 + npm 11, [XcodeGen](https://github.com/yonaskolb/XcodeGen).

```sh
Scripts/bootstrap.sh      # npm ci (CanvasRuntime) + xcodegen
Scripts/test_all.sh       # canvas tsc/vitest + ExcalidaysTests
Scripts/build_app.sh Debug
Scripts/package_app.sh    # Release ‒ Artifacts/Excalidays.app
Scripts/verify_app.sh
```

Do not install to /Applications unless you intend to; packaging writes `Artifacts/Excalidays.app`.

## License

The Excalidays application license is **unset** (owner-controlled). Third-party software retains its licenses — see [`THIRD_PARTY_NOTICES.md`](https://github.com/nodaysidle/excalidays/blob/2e3a41a1e14822b52b1a0556890f374b7d67d029/THIRD_PARTY_NOTICES.md) (Excalidraw 0.18.1 MIT and bundled font notices).
