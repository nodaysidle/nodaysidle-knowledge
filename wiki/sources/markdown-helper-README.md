---
type: source-readme
repo: "nodaysidle/markdown-helper"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "6b6558a5726807315fb50aac5bb633c63ab13467"
source_commit_date: "2026-10-07T09:34:28+02:00"
readme_path: "README.md"
readme_blob_sha: "10f508d4622a992000b722d60395c98a69e8afa2"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/markdown-helper/blob/6b6558a5726807315fb50aac5bb633c63ab13467/README.md"
tags: [source, readme, markdown-helper]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/markdown-helper` at `6b6558a` (2026-10-07T09:34:28+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<p align="center">
  <h1 align="center">AI Rules Builder</h1>
</p>

<p align="center">
  <strong>Create, preview, and share AGENTS.md and Cursor rules for Command Code, Codex, Cursor, agy, and deepseek-harness. Client-first: no database, no auth, no tracking.</strong>
</p>

<p align="center">
  <a href="https://markdown-helper.vercel.app"><img src="https://img.shields.io/badge/Live%20Demo-markdown--helper.vercel.app-7928CA?style=flat-square&logo=vercel&logoColor=white" alt="Live Demo"></a>
  <img src="https://img.shields.io/badge/Framework-Next.js%2016%20%7C%20React%2019-000000?style=flat-square&logo=next.js&logoColor=white" alt="Next.js">
  <img src="https://img.shields.io/badge/Styling-Tailwind%20CSS%20v4-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white" alt="Tailwind">
  <img src="https://img.shields.io/badge/API-Read--only%20%2Fapi%2Frules-4c8c6b?style=flat-square" alt="API">
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License">
</p>

---

> **The Problem:** Every AI coding agent expects a different rules file shape (`AGENTS.md`, `.mdc` frontmatter, legacy `.cursorrules`), and teams waste time reformatting the same engineering principles by hand.
>
> **The Result:** One builder toggles 20 curated rule sets, analyzes `package.json` in-browser, previews markdown live, exports the correct filename per tool, and exposes a read-only JSON API for automation.

---

Create, preview, and share rules-for-AI files for AI coding agents. State lives in `localStorage` or in share URLs; the only server surface is a read-only JSON API that AI tools can call programmatically.

## Features

- **Interactive rule builder** — pick a target tool and the output adapts to that tool's conventions (AGENTS.md, `.cursor/rules/*.mdc` with frontmatter, legacy `.cursorrules`).
- **Curated rule sets** — 20 editable rule sets in 7 categories (general, code style, testing, security, documentation, framework & UI, backend), toggleable individually.
- **Project analysis** — drop in `package.json` or `requirements.txt`; parsing happens in the browser, dependencies are detected and matching rule sets are suggested with reasons. Accept or dismiss each suggestion.
- **Live preview** — side-by-side editor (left) and rendered markdown (right), with a raw-source view. Copy to clipboard, download the correctly named file, and estimate token cost at a glance.
- **Save locally** — name and save configurations to `localStorage`; load or delete them any time.
- **Share links** — the full builder state is base64url-encoded into the `?share=` parameter; anyone opening the link sees your exact configuration.
- **JSON API** — `/api/rules` and `/api/rules/:id` for programmatic access, documented in-app at `/api`.

### Target tool conventions

| Tool | Output file(s) | Format |
| --- | --- | --- |
| Command Code | `AGENTS.md` (project root or `.commandcode/`) | Markdown |
| Codex CLI | `AGENTS.md` (project root) | Markdown |
| Cursor CLI | `.cursor/rules/ai-rules.mdc` | Markdown + `description:` / `globs:` / `alwaysApply:` frontmatter |
| Cursor CLI (legacy) | `.cursorrules` | Plain Markdown |
| agy | `AGENTS.md` | Markdown |
| deepseek-harness | `AGENTS.md` | Markdown |

## Getting started

```bash
npm install
npm run dev     # http://localhost:3000
```

For a production build:

```bash
npm run build
npm start
```

Other scripts: `npm run typecheck` (tsc), `npm run lint` (eslint).

### Deploy to Vercel

```bash
npm i -g vercel
vercel          # preview
vercel --prod   # production
```

Or import the repository in the [Vercel dashboard](https://vercel.com/new) — no extra configuration is needed; the build command is auto-detected from `package.json`.

## API reference

Base URL: `https://markdown-helper.vercel.app`. Read-only, no auth, CORS enabled, `cache-control: public, max-age=300`.

### `GET /api/rules`

Lists the target tools and metadata for every rule set.

```bash
curl -s https://your-app.vercel.app/api/rules | jq -r '.ruleSets[].id'
```

### `GET /api/rules/{id}`

Returns one rule set with its `rules` array plus a ready-to-append markdown `content` field.

```bash
curl -s https://your-app.vercel.app/api/rules/security-web | jq -r '.content' >> AGENTS.md
```

`404` responses are JSON: `{ "error": "...", "available": [...ids] }`.

The catalog of ids lives in [`lib/catalog.ts`](https://github.com/nodaysidle/markdown-helper/blob/6b6558a5726807315fb50aac5bb633c63ab13467/lib/catalog.ts) and is also listed in-app at [`/api`](https://github.com/nodaysidle/markdown-helper/blob/6b6558a5726807315fb50aac5bb633c63ab13467/api).

## Share link format

The `?share=` parameter is base64url of `JSON.stringify(config)` with a config schema `{ v: 1, tool, fileOption, title, selected: string[], custom: string }`. Decoding is in [`lib/share.ts`](https://github.com/nodaysidle/markdown-helper/blob/6b6558a5726807315fb50aac5bb633c63ab13467/lib/share.ts); malformed payloads are rejected and surface an error toast.

## Project structure

```
markdown-helper/
├── app/
│   ├── layout.tsx              # shell: header, footer, fonts, toast provider
│   ├── page.tsx                # the builder (client component)
│   ├── globals.css             # Tailwind v4 + theme tokens (light/dark)
│   ├── icon.svg                # favicon
│   ├── api/
│   │   ├── page.tsx            # human-readable API docs page
│   │   └── rules/
│   │       ├── route.ts        # GET /api/rules
│   │       └── [id]/route.ts   # GET /api/rules/:id
├── components/
│   ├── BrandMark.tsx
│   ├── ToastProvider.tsx       # global toasts (aria-live)
│   ├── icons.tsx
│   ├── ToolPicker.tsx          # tool dropdown + output file variant + title
│   ├── UploadAnalyzer.tsx      # drag & drop / picker + detected deps + suggestions
│   ├── RuleSetList.tsx         # searchable catalog with toggles
│   ├── CustomEditor.tsx        # free-form markdown input
│   ├── SavedConfigs.tsx        # localStorage list UI
│   └── Preview.tsx             # rendered/source preview + copy/download/share
├── lib/
│   ├── catalog.ts              # the curated rule sets (edit here)
│   ├── tools.ts                # target tool profiles & output naming
│   ├── markdown.ts             # composer: config -> final document
│   ├── analyze.ts              # package.json / requirements.txt parsing + suggestions
│   ├── config.ts               # defaults + schema-safe merging
│   ├── share.ts                # base64url encode/decode for ?share=
│   ├── storage.ts              # localStorage persistence
│   ├── clipboard.ts            # clipboard write with fallback
│   ├── download.ts             # blob download helper
│   ├── types.ts
│   └── cn.ts
├── INSTRUCITONS.md             # original build spec
├── README.md
├── package.json
├── next.config.ts
├── postcss.config.mjs
├── eslint.config.mjs
└── tsconfig.json
```

## Adding rule sets

Edit `lib/catalog.ts`. Each entry:

```ts
{
  id: "codestyle-typescript",        // unique, kebab-case; used by the API
  name: "TypeScript Style",
  category: "Code Style",            // must be one of CATEGORIES
  description: "Shown under the toggle.",
  signals: ["typescript"],           // dependency fragments that trigger suggestions
  rules: ["Rule one.", "Rule two."], // exported as markdown bullets
}
```

Rule ids are stable identifiers — changing an id affects the API, existing share links, and saved configurations (which are filtered defensively, so unknown ids are dropped).

## Tech stack

- [Next.js](https://nextjs.org) (App Router, TypeScript) — one framework covers the UI and the `/api` route handlers deployed as serverless functions on Vercel.
- [Tailwind CSS](https://tailwindcss.com) v4 with `@tailwindcss/typography`; theme tokens via CSS variables with automatic light/dark.
- [react-markdown](https://github.com/remarkjs/react-markdown) + `remark-gfm` for the live preview.
- Inter + JetBrains Mono via `next/font`.

## Privacy

Project files are parsed client-side and never uploaded. Saved configurations stay in `localStorage`. Share links carry configuration in the URL only.

## License

MIT © [nodaysidle](https://github.com/nodaysidle)
