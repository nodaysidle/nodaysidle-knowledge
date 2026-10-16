---
type: source-readme
repo: "nodaysidle/nodaysidle-project-pages"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "8c7eb16d36bcdfaa6dfd2d95369c9de4ac85d746"
source_commit_date: "2026-09-06T05:26:27+02:00"
readme_path: "README.md"
readme_blob_sha: "d576353ff30c628bb53daa6c2c65f9c3dab02ec6"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/nodaysidle-project-pages/blob/8c7eb16d36bcdfaa6dfd2d95369c9de4ac85d746/README.md"
tags: [source, readme, nodaysidle-project-pages]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/nodaysidle-project-pages` at `8c7eb16` (2026-09-06T05:26:27+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

# NODAYSIDLE Project Pages

Public showcase for NODAYSIDLE — five flagship products as full-bleed void-black scroll-snap chapters.

Live site: [https://nodaysidle-project-pages.vercel.app](https://nodaysidle-project-pages.vercel.app)

![Platform](https://img.shields.io/badge/platform-Web-black?style=flat-square)
![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react)
![Vite](https://img.shields.io/badge/Vite-8-646CFF?style=flat-square&logo=vite)

## Flagship chapters (home)

Home is a SpaceX-style scroll of five chapters — not a catalogue grid. Nav is only these five names. Each chapter has its own accent color.

| Chapter | Platform | CTA |
|---------|----------|-----|
| **Cascade V3** | macOS · Apple Silicon · aarch64 | Download Apple Silicon DMG (+ GitHub) |
| **Voice Anywhere** 0.4.0 | Android 12+ | Download APK |
| **NODAYSIDLE Voice** 0.2.0 | macOS 14+ · Apple silicon | Download DMG |
| **Synapse Notes** 0.4.3 | Android · Capacitor | Download debug APK |
| **Excalidays** 0.1.0 | macOS · Phase 0/1 | Download DMG |

`featuredSlugs` order: `nodaysidle-cascade-v3` → `nodaysidle-voice-anywhere-v2` → `nodaysidle-vois` → `synapse-notes` → `excalidays`.

Cascade honesty: aarch64 / ad-hoc / not notarized — no Intel/Win/Linux claim. Excalidays is Phase 0/1 only.

## Technology

| Area | Technology |
|------|------------|
| Framework | React 19 |
| Build | Vite 8 |
| Styling | Plain CSS |
| Deployment | Vercel (static) |
| Routing | SPA rewrites via `vercel.json` |

## Development

```bash
npm install
npm run dev
```

Dev server at `http://127.0.0.1:5173`.

## Build

```bash
npm run build
```

Output in `dist/`. Preview with `npm run preview`.

## Project structure

```text
src/data.js     Product truth, featuredSlugs, download URLs, accents
src/main.jsx    Home chapters, detail routes, header/footer
src/styles.css  Void-black scroll-snap chapter layout
vercel.json     SPA route rewrites
```

## Status

Active — public web showcase. Content updated as flagship releases ship.

## Contributing

This repository is not currently accepting external contributions.
