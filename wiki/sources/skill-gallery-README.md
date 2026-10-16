---
type: source-readme
repo: "nodaysidle/skill-gallery"
visibility: "public"
fork: false
default_branch: "master"
source_commit: "e035a2e93f08e422f1f39ffe893613f900b56db0"
source_commit_date: "2026-10-07T09:37:45+02:00"
readme_path: "README.md"
readme_blob_sha: "a4ddabad76d44b9bfc93a3763db59445b5a9c824"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/skill-gallery/blob/e035a2e93f08e422f1f39ffe893613f900b56db0/README.md"
tags: [source, readme, skill-gallery]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/skill-gallery` at `e035a2e` (2026-10-07T09:37:45+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<p align="center">
  <h1 align="center">Agent Gallery</h1>
</p>

<p align="center">
  <strong>Offline-friendly gallery of 119 open-source AI agent and RAG templates from awesome-llm-apps—search, filter, and deep-link every starter with plain-English summaries.</strong>
</p>

<p align="center">
  <a href="https://agent-gallery.vercel.app"><img src="https://img.shields.io/badge/Live%20Demo-agent--gallery.vercel.app-7928CA?style=flat-square&logo=vercel&logoColor=white" alt="Live Demo"></a>
  <img src="https://img.shields.io/badge/Templates-119-4E6EF2?style=flat-square" alt="119 templates">
  <img src="https://img.shields.io/badge/Stack-HTML%20%7C%20CSS%20%7C%20vanilla%20JS-151518?style=flat-square" alt="Static">
  <img src="https://img.shields.io/badge/Build-zero-4c8c6b?style=flat-square" alt="Zero build">
  <img src="https://img.shields.io/badge/License-Apache--2.0-green?style=flat-square" alt="License">
</p>

---

> **The Problem:** The awesome-llm-apps catalog is huge and README-native—hard to browse offline or compare templates quickly.
>
> **The Result:** A static site with curated metadata in `data/apps.js`, hash routing for detail pages, and zero npm dependencies at runtime.

---

Data source: [shubhamsaboo/awesome-llm-apps](https://github.com/shubhamsaboo/awesome-llm-apps) (Apache-2.0).

Browse starters, advanced agents, agent teams, voice agents, RAG tutorials, MCP apps, generative UI, always-on agents, LLM apps, and framework crash courses — each with a plain-English summary, key features, setup notes, and a link to the original source folder.

## Tech stack

Plain **HTML + CSS + vanilla JS**, zero dependencies, zero build step. Data lives in
`data/apps.js` (curated from the upstream README, Oct 2026) so the site works fully offline.

## Run locally

No install needed — just serve the folder (ES modules/`file://` restrictions don't apply
since everything is classic scripts, so you can even open `index.html` directly):

```bash
git clone https://github.com/nodaysidle/skill-gallery.git
cd skill-gallery

# option 1: zero-install
npx --yes serve .

# option 2: via npm scripts
npm install   # no-op, no dependencies
npm run dev   # serves on http://localhost:3000

# option 3: python
python3 -m http.server 8000
```

Then open the printed URL. Search, category/difficulty/tag filters, and per-template
detail pages (`#/app/<id>`) all work client-side.

## Deploy to Vercel

This is a static site — no build command, output directory is `.`:

```bash
npx --yes vercel        # preview deploy
npx --yes vercel --prod # production deploy
```

Or connect this repository in the Vercel dashboard (framework preset: **Other**).

## Project layout

```
index.html      # shell: header, <main>, footer
styles.css      # all styling, no framework
app.js          # hash router: home, browse (#/browse), detail (#/app/:id)
data/apps.js    # window.APP_DATA — 11 categories, 119 templates, setup guides, featured picks
package.json    # `npm run dev` (serve) convenience script
```

## Refreshing the data

Re-check the upstream [README](https://github.com/shubhamsaboo/awesome-llm-apps) for new
templates, add entries to `data/apps.js` (fields: `id, title, emoji, cat, level, tags,
path, keys, desc, summary, highlights`), and optionally feature them via `featured: [...]`.

## License

Apache-2.0 for curated upstream listings; site code MIT © [nodaysidle](https://github.com/nodaysidle).
