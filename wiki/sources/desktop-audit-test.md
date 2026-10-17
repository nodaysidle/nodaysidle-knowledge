---
type: source
source_id: "desktop-audit-test"
title: "Desktop app ship-stage audit (batchrename-pro, cliprail, cursorpad, monospace-notes, nodaysidle-vois)"
author: Claude (Opus 5.5)
date: "2026-10-17"
source_note: "Read-only audit of fresh clones of the GitHub default branches (deleted after the audit) plus gh release/issue/PR/run metadata. Local copies were inspected with git rev-parse/log/status only."
tags: [source, audit, catalog, macos, releases, readme]
---

# Desktop app ship-stage audit, 2026-10-17 (read-only)

Scope: `nodaysidle/{batchrename-pro,cliprail,cursorpad,monospace-notes,nodaysidle-vois}`. All five repo names resolved as given. All are public and use `main` as the default branch. **No open issues and no closed issues exist in any of the five repos**, so "top issues" below means audit findings plus open PRs.

Each latest-release asset was downloaded and hashed with `sha256sum`. Every asset is a valid `Apple DMG, version 4`. The bundle contents could not be inspected because no DMG extractor (7z/hdiutil) exists on arch, so Info.plist version, architecture and signing inside each DMG are **unverified**.

## Summary

| Repo | HEAD (main) | Latest release / tag | Build system | Linux check | README vs release |
|---|---|---|---|---|---|
| batchrename-pro | `bff7b47` (2026-09-18) | v0.1.0 (2026-06-06), 13 commits behind main | Tauri 2 (Vite/React/TS + Rust) | **Yes**: typecheck ✅, 10/10 unit ✅, vite build ✅, `cargo test` 29/29 ✅ | ✅ DMG link + SHA match; no `.sha256` asset; no demo GIF |
| cliprail | `d8ad7ba` (2026-10-16) | Latest = `v1.2.0-dmg.20260727`; tags v1.2.1, v1.2.0 also exist | SwiftPM (tools 6.0, macOS 14) | No (no Swift toolchain; macOS-only) | ✅ DMG + `.sha256` + README SHA all match; no demo GIF |
| cursorpad | `0347fbf` (2026-09-21) | v1.0.0 (2026-09-21), 2 commits behind | SwiftPM (tools 6.0, macOS 14) | No | ⚠️ No download link/SHA in README; HEAD claims "v1.1.0 release" but no v1.1.0 tag/release; no `.sha256`; no GIF |
| monospace-notes | `9484711` (2026-09-24) | v1.0.0 (2026-09-24), at HEAD | SwiftPM (tools 6.0, macOS 14) | No | ⚠️ README never links the release; asset is `Monospace.Notes.dmg` but README says `Monospace Notes.dmg`; no `.sha256`; screenshots only, no GIF |
| nodaysidle-vois | `1f637db` (2026-09-18) | v0.2.0 (2026-08-31), 2 commits behind | SwiftPM (tools 6.2, macOS 14) | No | ✅ DMG link + `SHA256SUMS.txt` match; README doesn't print the hash; no GIF |

None of the five READMEs embeds a demo GIF, and no repo contains a `.gif` file.

## batchrename-pro

- **Default branch / HEAD:** `main` @ `bff7b4763f53478ce6b7c6309c5ae44fbec82216` ("Merge PR #5 cursor/hybrid-release-on-tag").
- **Latest release:** `v0.1.0` "BatchRename Pro 0.1.0" (2026-06-06). Asset: `BatchRename-Pro-0.1.0-aarch64.dmg` (7,139,735 B), sha256 `ef6e33a0…48309b`.
- **Build:** Tauri 2. Frontend is Vite + React 19 + TypeScript; backend is Rust in `src-tauri/`. Version is 0.1.0 in package.json, tauri.conf.json and Cargo.toml. CI: `build.yml` (latest 3 runs on main all succeeded, last on 2026-09-17) and `release-on-tag.yml`.
- **Linux checks run here (in the throwaway clone):** `npm ci --ignore-scripts` → `tsc --noEmit` passed; `npm run test:unit` 10/10 passed; `vite build` passed; `cargo test --locked` in `src-tauri` 29/29 passed (webkit2gtk-4.1 is present). **Cannot verify:** `tauri build` for macOS, the `.app`/DMG bundle, ad-hoc signing, or runtime behaviour on macOS.
- **README vs release:** The platform claim (macOS Apple Silicon, ad-hoc signed / not notarized) matches the `aarch64` asset name. The version badge and download link point to v0.1.0, which is the actual Latest. The README SHA256 `ef6e33a0…` **matches** the downloaded DMG. There is no `.sha256` asset on the release (the hash only appears in the README) and no demo GIF.
- **Top issues:** (1) main is 13 commits ahead of v0.1.0 and has not been released. (2) `tsconfig.tsbuildinfo` is committed and gets dirtied by local builds. (3) There are two script dirs, `scripts/` and `Scripts/`, which collide on case-insensitive macOS filesystems. No open issues or PRs.

## cliprail

- **Default branch / HEAD:** `main` @ `d8ad7badf1a55d6d05bc8662fb3a55e65fe85685` ("docs(readme): point download at ClipRail-1.2.0.dmg + .sha256 (Latest) (#5)", 2026-10-16).
- **Latest release:** `v1.2.0-dmg.20260727` "ClipRail 1.2.0 — macOS DMG" (2026-07-27). Assets: `ClipRail-1.2.0.dmg` (199,149 B) and `ClipRail-1.2.0.dmg.sha256`. Older releases: `v1.2.1` "NODAYSIDLE theme fleet" (0 assets) and `v1.2.0`.
- **Build:** SwiftPM (`swift-tools-version: 6.0`, `.macOS(.v14)`). `Scripts/package_app.sh` hard-codes `APP_VERSION="1.2.0"`. Tests are in `Tests/ClipRailTests` (~46 test functions). Workflow: `release-on-tag.yml` only, with no recorded runs.
- **Linux:** not possible. Arch has no Swift toolchain, and the app targets macOS AppKit/SwiftUI. **Cannot verify:** `swift build/test`, packaging, signing, or the DMG contents.
- **README vs release:** "Version 1.2.0 · macOS 14+" and "Latest, Apple Silicon". The README SHA `a8312014…115c0d` matches the downloaded DMG, which also matches the `.sha256` asset. No demo GIF.
- **Top issues:** (1) Tag confusion: `v1.2.1` and `v1.2.0-dmg.20260727` point at the same commit `33fd0b9`. v1.2.1 is a higher version number with no assets, yet the README and plist say 1.2.0. (2) Open PR #4 "verified release download link + SHA-256" is **CONFLICTING** and was superseded by merged #5, so it is stale. (3) Open PR #1 "Cursor Cloud instructions (macOS-only)" dates from 2026-07-07 and looks stale. (4) The 199 KB DMG is unusually small; its contents were not verified.

## cursorpad

- **Default branch / HEAD:** `main` @ `0347fbf41db21ef4cfbd8a82b763fc532b70ceca` ("feat: v1.1.0 release - Preferences window…", 2026-09-21).
- **Latest release:** `v1.0.0` "CursorPad v1.0.0 — Native Cursor-Themed Notepad" (2026-09-21). Asset: `CursorPad.dmg` (479,403 B), sha256 `9708d2e7…72a963`.
- **Build:** SwiftPM (tools 6.0, macOS 14, zero deps). `Scripts/package_app.sh` has `BUNDLE_VERSION="1.0.0"`. Tests are in `Tests/CursorpadTests` (~148 test functions; README claims 145). No GitHub workflows.
- **Linux:** not possible (macOS/TextKit 2). **Cannot verify:** build, tests, launch-time claims (<100 ms), signing, or the DMG.
- **README vs release:** The README has **no download link, no release version and no SHA**. It only gives build-from-source steps. It claims "macOS 14+ · Apple Silicon" but the architecture diagram says "Universal DMG Assembly", which contradicts that and is unverified. RELEASE_NOTES.md and the HEAD commit describe **v1.1.0**, but the only tag/release is v1.0.0 and the packaging script still says 1.0.0. No `.sha256`, no GIF.
- **Top issues:** (1) The v1.1.0 release was announced in commits/notes but never tagged or released. (2) Open PR #1 "verified release download link + SHA-256" (2026-10-16, MERGEABLE) would fix the missing download section. (3) The "Universal" vs "Apple Silicon" wording is inconsistent.

## monospace-notes

- **Default branch / HEAD:** `main` @ `948471102e17086b366045b25757ec2fdca56e97` ("docs: add CLAUDE.md working preferences", 2026-09-24).
- **Latest release:** `v1.0.0` "Monospace Notes 1.0.0" (2026-09-24), tagged at HEAD. Asset: `Monospace.Notes.dmg` (830,887 B), sha256 `dea6e2b7…82f1f9`.
- **Build:** SwiftPM (tools 6.0, macOS 14). `Scripts/package_app.sh` has `SHORT_VERSION="1.0.0"`. Also has `Scripts/test.sh` and `Scripts/ax_audit.swift`. Tests are in `Tests/MonospaceNotesTests` (~246 `@Test`/test funcs; README claims 241). No GitHub workflows.
- **Linux:** not possible. **Cannot verify:** build, the 241-test claim, the ~80 ms launch claim, Developer ID vs ad-hoc signing, or the DMG.
- **README vs release:** Platform "macOS 14+ on Apple silicon" is consistent. However, the README **never links the GitHub release** and covers only build from source. The release asset name `Monospace.Notes.dmg` differs from the documented `dist/Monospace Notes.dmg` (GitHub replaced the space). No SHA anywhere, no `.sha256` asset. It has screenshots (`docs/screenshots/*.png`) but no demo GIF.
- **Top issues:** (1) The README needs a Download section with the asset link and SHA-256. (2) There is no checksum asset. No open issues or PRs.

## nodaysidle-vois

- **Default branch / HEAD:** `main` @ `1f637dbf0ff84d9b531c457b1de7579a24983bea` ("Merge PR #4 cursor/hybrid-release-automation", 2026-09-18).
- **Latest release:** `v0.2.0` "NODAYSIDLE Voice v0.2.0" (2026-08-31). Assets: `NODAYSIDLE-Voice-0.2.0.dmg` (3,782,101 B) and `SHA256SUMS.txt`. The earlier release is v0.1.0.
- **Build:** SwiftPM (`swift-tools-version: 6.2`, macOS 14, with `Package.resolved`, i.e. it has deps such as WhisperKit). `version.env` contains `MARKETING_VERSION=0.2.0`, `BUILD_NUMBER=2`. Scripts are `package_app.sh` and `package_dmg.sh`. Tests are in `Tests/NODAYSIDLEVoiceTests` (~39). Workflow: `release-on-tag.yml`, with no recorded runs.
- **Linux:** not possible (Swift 6.2 + AppKit/AVFoundation/WhisperKit). **Cannot verify:** build, tests, mic/accessibility permissions, local-model download, or the DMG.
- **README vs release:** "macOS only (Apple silicon), macOS 14+". The download links point to v0.2.0, which is Latest. `SHA256SUMS.txt` matches the downloaded DMG (`25b4536b…38854b`). The README mentions `SHA256SUMS.txt` in the build section but doesn't print the hash or link the checksum asset in Install. No demo GIF (the `Artifacts/UI-Audit/*.png` screenshots are not embedded as a demo).
- **Top issues:** (1) The README Install section should link `SHA256SUMS.txt` and show the hash. (2) The repo root contains the internal `CODEX-CLI-PROMPT.md` and an `Artifacts/` folder, which add public-repo noise. No open issues or PRs.

## Local copies on arch

Inspected with read-only `git rev-parse` / `log` / `status` / `cat-file`. Nothing was fetched, checked out or modified. "Behind" counts were computed against the fresh GitHub clones.

| Path | Branch | Local HEAD | vs GitHub default HEAD |
|---|---|---|---|
| `/home/arch/Projects/cursorpad` | `main` | `0347fbf` | **Equal** to GitHub `0347fbf`; clean |
| `/home/arch/Projects/_audit-temp/batchrename-pro-06c33623` | detached `HEAD` | `06c3362` (2026-06-10) | On GitHub main, **9 behind** `bff7b47`; 4 untracked files (`src-tauri/tests/`, `ui-fixtures/`, 2 PNGs) |
| `/home/arch/Projects/_github-markdown-cleanup/batchrename-pro` | `main` | `0a5782b` (2026-06-07) | **12 behind**, 0 ahead; clean |
| `/home/arch/Projects/_github-migrations/batchrename-pro` | `task/dox-agents` | `d314b84` (2026-07-25) | **3 ahead / 9 behind**. The 3 commits are **not on GitHub main** (local-only or unmerged branch); `tsconfig.tsbuildinfo` modified |
| `/home/arch/Projects/_theme-worktrees/batchrename-pro` | n/a | n/a | ⚠️ **Not a git repository / likely broken worktree.** `.git` file points to `/Volumes/omarchyuser/projekti/nodaysidle-batchrenamepro/.git/worktrees/batchrename-pro`, which doesn't exist on arch. Not repaired or pruned. |
| `/home/arch/Projects/_theme-worktrees/cliprail` | n/a | n/a | ⚠️ **Not a git repository / likely broken worktree.** `.git` file points to `/Volumes/omarchyuser/projekti/nodaysidle-cliprail/.git/worktrees/cliprail`, which is missing. Not repaired or pruned. |
| `/home/arch/Projects/_release-worktrees/cliprail-20260727-012541` | detached `HEAD` | `33fd0b9` (2026-07-24, = tag v1.2.1 / v1.2.0-dmg.20260727) | On GitHub main, **3 behind** `d8ad7ba`; 7 dirty files (README, CHANGELOG, USERGUIDE, .gitignore, install_app.sh, internal AGENTS.md modified; `Scripts/package_dmg.sh` untracked) |
| `/home/arch/Projects/_github-migrations/nodaysidle-vois` | `main` | `dbd3b21` (2026-08-30) | On GitHub main, **2 behind** `1f637db`; clean |

**monospace-notes:** the brief expected no local copy, but **one exists** at `/home/arch/Projects/monospace-notes` (`origin` = github.com/nodaysidle/monospace-notes). It is on `main` @ `9484711`, which **equals** the GitHub HEAD, and is clean. (`/home/arch/Projects/monospace` is a separate spec-only folder inside the `/home/arch/Projects` git repo and is not a monospace-notes checkout.)
