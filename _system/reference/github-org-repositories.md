---
type: reference
source_url: https://github.com/nodaysidle?tab=repositories
synced: 2026-10-07
public_repo_count: 36
tags:
  - reference
  - github
---

# nodaysidle GitHub repositories

Canonical list from the [public repositories tab](https://github.com/nodaysidle?tab=repositories). Re-sync with:

```bash
curl -s "https://api.github.com/users/nodaysidle/repos?per_page=100&type=owner" \
  | jq -r '.[] | "- [\(.name)](\(.html_url))" + (if .homepage != null and .homepage != "" then " — " + .homepage else "" end)' | sort
```

## Published on GitHub

- [batchrename-pro](https://github.com/nodaysidle/batchrename-pro)
- [BrewLedger](https://github.com/nodaysidle/BrewLedger)
- [cliprail](https://github.com/nodaysidle/cliprail)
- [cursorpad](https://github.com/nodaysidle/cursorpad)
- [excalidays](https://github.com/nodaysidle/excalidays)
- [hermes-agent](https://github.com/nodaysidle/hermes-agent) — https://hermes-agent.nousresearch.com
- [hermes-gpt](https://github.com/nodaysidle/hermes-gpt) — https://hermes-gpt.tonysimons.dev
- [kureksistant](https://github.com/nodaysidle/kureksistant) — https://github.com/nodaysidle/kureksistant
- [markdown-helper](https://github.com/nodaysidle/markdown-helper) — https://markdown-helper.vercel.app
- [monospace-notes](https://github.com/nodaysidle/monospace-notes)
- [nodaysidian](https://github.com/nodaysidle/nodaysidian)
- [nodaysidle](https://github.com/nodaysidle/nodaysidle) — profile README and public project index
- [nodaysidle-browser](https://github.com/nodaysidle/nodaysidle-browser)
- [nodaysidle-browser-linux](https://github.com/nodaysidle/nodaysidle-browser-linux)
- [nodaysidle-cascade-v3](https://github.com/nodaysidle/nodaysidle-cascade-v3)
- [nodaysidle-cistilka](https://github.com/nodaysidle/nodaysidle-cistilka)
- [nodaysidle-cloudscribe](https://github.com/nodaysidle/nodaysidle-cloudscribe)
- [nodaysidle-echocore-pro](https://github.com/nodaysidle/nodaysidle-echocore-pro)
- [nodaysidle-flowstate](https://github.com/nodaysidle/nodaysidle-flowstate)
- [nodaysidle-knowledge](https://github.com/nodaysidle/nodaysidle-knowledge) — research vault (this repo)
- [nodaysidle-lumiere](https://github.com/nodaysidle/nodaysidle-lumiere)
- [nodaysidle-project-pages](https://github.com/nodaysidle/nodaysidle-project-pages) — https://nodaysidle-showcase-v2.vercel.app
- [nodaysidle-prompt-optimizer](https://github.com/nodaysidle/nodaysidle-prompt-optimizer)
- [nodaysidle-shareguard](https://github.com/nodaysidle/nodaysidle-shareguard)
- [nodaysidle-sonora](https://github.com/nodaysidle/nodaysidle-sonora)
- [nodaysidle-voice-anywhere-v2](https://github.com/nodaysidle/nodaysidle-voice-anywhere-v2)
- [nodaysidle-vois](https://github.com/nodaysidle/nodaysidle-vois)
- [nodaysrecording](https://github.com/nodaysidle/nodaysrecording)
- [nodaystypst](https://github.com/nodaysidle/nodaystypst)
- [pocket-drafts](https://github.com/nodaysidle/pocket-drafts)
- [Portfolio](https://github.com/nodaysidle/Portfolio) — https://nodaysidle-portfolio-nine.vercel.app
- [scribeflowpro](https://github.com/nodaysidle/scribeflowpro)
- [skill-gallery](https://github.com/nodaysidle/skill-gallery) — https://agent-gallery.vercel.app
- [small-count](https://github.com/nodaysidle/small-count)
- [synapse-notes](https://github.com/nodaysidle/synapse-notes)
- [whisper-bar](https://github.com/nodaysidle/whisper-bar)

## Local clones (sibling monorepo)

When using a multi-repo checkout under `~/dev/nodaysidle/`, catalog `local_path: ../{folder}` may differ from the GitHub repo name (e.g. `kurekizmo` → `kureksistant`).

## Update 2026-10-07 10:10 (UTC+2) — total including private repos

Append-only note; the public list above is unchanged and still counts 36.

- **Total org repositories: 48** = 36 public (listed above) + 12 private. Source: user correction, 2026-10-07; not independently verifiable here, because `gh` is unauthenticated and the public API returns public repos only.
- Known private repos (per user): `kureksistant`, `nodaysidle-cascade-v3`, `nodaysidle-sonora`, `synapse-notes`. The other 8 private repos have not been named.
- ⚠️ These four also appear in the public list above, which was taken from the public API. That conflicts with the user's correction. Kept as-is (no history rewrite); needs re-sync or human confirmation.

## Correction 2026-10-07 13:55 (UTC+2) — the four "private" repos are public

Append-only; the 10:10 entry above is left as written.

- `kureksistant`, `nodaysidle-cascade-v3`, `nodaysidle-sonora` and `synapse-notes` are **public**. The GitHub API reports `"private": false, "visibility": "public"` for each, and all four were cloned anonymously over HTTPS. The user confirmed kureksistant stays public.
- So none of the 12 private repos has been identified, and the private count is **unknown**. The total of **48** is the user's figure, unverified (36 public by API + an unknown number of private repos).

## Update 2026-10-07 14:18 (UTC+2) — the 12 private repos (per user)

Append-only. Source: the user's own list, 2026-10-07; not API-verified, because `gh` is unauthenticated. **Total: 36 public + 12 private = 48. The count is resolved.**

| # | Repo | Language | Description |
|---|---|---|---|
| 1 | kurekizmo | Python | — |
| 2 | jev-review | TypeScript (MIT) | Staged TypeSafe Jev code-review workflow |
| 3 | nodaysidle-portfolio | JavaScript | Cinematic portfolio of apps |
| 4 | nodaysidle-whispering | Rust | Local-first macOS dictation |
| 5 | nodaysnotes | Swift | Minimal native macOS notes |
| 6 | hermes-continuity | Python | Sanitized Hermes continuity snapshot |
| 7 | nodaysgent | TypeScript | Local-first agent runtime monorepo |
| 8 | nodaysidle-control-room | Swift | macOS control surface for agent ops |
| 9 | nodaysidle-project-page-2 | CSS | NIGHTSHIFT Edition 03 catalogue |
| 10 | twentyone | TypeScript | Android remote controller for nodaysgent over Cloudflare |
| 11 | orbit-browser | Rust (MIT) | Tauri 2 macOS browser |
| 12 | werkstatt-infinite | Kotlin | — |

- **kurekizmo vs kureksistant:** `kurekizmo` is a private repo. `kureksistant` is public. The local folder `/home/arch/dev/nodaysidle/kurekizmo` has an old-origin remote that points at `kureksistant`.
- **10:10 entry was wrong:** it listed `kureksistant`, `nodaysidle-cascade-v3`, `nodaysidle-sonora` and `synapse-notes` as private. All four are public (see the 13:55 correction). The entry is left as written.

## Update 2026-10-08 22:30 (UTC+2): five-repo status check

Append-only; earlier entries unchanged. Checked with the public GitHub API during [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].

- `whisper-bar`, `nodaysidle-cascade-v3`, `nodaysidle-sonora`, `nodaysidle-shareguard` and `nodaysidle-browser-linux` are all **public** (`"private": false`). None has a GitHub homepage URL set. `nodaysidle-browser-linux` uses `master` as its default branch; the other four use `main`.
- ⚠️ **Conflict, visibility history:** SWEEP (2026-10-08 22:18) reported cascade-v3 and sonora as newly public and private as of 2026-10-07. The 13:55 correction above already recorded both as public via the API on 2026-10-07; only the 10:10 entry (since corrected) called them private. Any private→public flip time is unverified.
- ⚠️ **Conflict, portfolio:** the list above shows `Portfolio — https://nodaysidle-portfolio-nine.vercel.app` (the public repo's homepage field). However, the Vercel project serving that domain is `nodaysidle-portfolio`, which matches private repo #3 in the 14:18 list (public API: 404). Which repo deploys the site is unverified.
- The owner confirmed portfolio-nine as the official showcase. `nodaysidle-project-pages` (showcase-v2) is stale and not canonical.

## Update 2026-10-08 23:41 (UTC+2): new public repo nodaysidle-apps

Append-only. The public API (`/users/nodaysidle/repos`) now returns **37** public repos (was 36), including the new [nodaysidle-apps](https://github.com/nodaysidle/nodaysidle-apps) — https://nodaysidle-apps.vercel.app (downloads showcase, created 2026-10-08).

- ✅ The "Conflict, portfolio" note in the 22:30 update is resolved. portfolio-nine's latest production deployment (2026-10-07 09:38) came from the public `Portfolio` repo, `master` @ `a225402`, via a CLI deploy. Earlier deployments, up to 2026-09-18, came from the private `nodaysidle-portfolio` repo (per user).

## Update 2026-10-09 10:32 (UTC+2): new public repo nodaysrammar

Append-only. The public API now returns **38** public repos (37 at 2026-10-08 23:41). The new one is [nodaysrammar](https://github.com/nodaysidle/nodaysrammar), a Chrome MV3 grammar checker created 2026-10-09 10:02, MIT, no homepage. Its local folder is `../chrome-extension` (the folder name differs from the repo name). See [[_system/templates/catalog/nodaysrammar]].
