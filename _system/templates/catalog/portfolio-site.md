---
type: catalog-entry
name: NODAYSIDLE Portfolio
status: completed
short_description: Dependency-free editorial portfolio site; build-time HTML from profile + presentation JSON; Vercel static deploy.
github_status: mixed
repo_url: https://github.com/nodaysidle/Portfolio
stale_repo_url: https://github.com/nodaysidle/nodaysidle-project-pages
site_url: https://nodaysidle-portfolio-nine.vercel.app
showcase_url: https://nodaysidle-showcase-v2.vercel.app
profile_index_repo: https://github.com/nodaysidle/nodaysidle
local_path: ../Portfolio
github_portfolio_repo: https://github.com/nodaysidle/Portfolio
local_note: Editorial portfolio source; Vercel production alias in docs/deployment.md.
stack:
  - Node.js 22+
  - static HTML/CSS/JS
tags:
  - catalog
  - web
  - portfolio
updated: 2026-10-17
---

# Portfolio site

Canonical **presentation** layer for featured GitHub projects (`data/presentation.json`). Not the research vault—link research briefs here when a project should appear on the public site.

- **Public showcase repo:** [nodaysidle-project-pages](https://github.com/nodaysidle/nodaysidle-project-pages) → [nodaysidle-showcase-v2.vercel.app](https://nodaysidle-showcase-v2.vercel.app)
- **Profile index:** [nodaysidle/nodaysidle](https://github.com/nodaysidle/nodaysidle)
- **Editorial portfolio repo:** [github.com/nodaysidle/Portfolio](https://github.com/nodaysidle/Portfolio) → [nodaysidle-portfolio-nine.vercel.app](https://nodaysidle-portfolio-nine.vercel.app)
- **Edit flow (local):** `../Portfolio/README.md` → “Add or edit projects”

## Status 2026-10-08 (owner decision; verified 22:30 UTC+2)

- **Official showcase (owner-confirmed via SWEEP, 2026-10-08):** https://nodaysidle-portfolio-nine.vercel.app. It is served by the Vercel project `nodaysidle-portfolio` (Vite); the last production deployment was READY on 2026-10-07 09:38.
  - It lists Cascade, WhisperBar and Sonora. Its "NODAYSIDLE Browser" card is the macOS `nodaysidle-browser`. It also links `synapse-notes`.
  - **ShareGuard and nodaysidle-browser-linux are not listed.**
- ⚠️ **Stale as of 2026-10-08, not canonical:** the `showcase_url` https://nodaysidle-showcase-v2.vercel.app and its repo [nodaysidle-project-pages](https://github.com/nodaysidle/nodaysidle-project-pages) (last push 2026-09-06).
  - Of the reconciled repos it lists only Cascade V3, with a v3.0.0 DMG link and "Not Intel, Windows, or Linux" copy.
  - The "Public showcase repo" bullet above is kept as written but no longer describes the canonical surface.
- ⚠️ **Conflict:** this entry says the editorial portfolio is a dependency-free static build from the public [Portfolio](https://github.com/nodaysidle/Portfolio) repo, and that repo's GitHub homepage is portfolio-nine. ✅ **Resolved 2026-10-08 23:41:** the latest production deployment comes from the public `Portfolio` repo (see the section below).
  - However, the Vercel project serving portfolio-nine is named `nodaysidle-portfolio` and uses Vite.
  - `nodaysidle-portfolio` is one of the user's 12 private repos (the public API returns 404).
  - The Vercel API returned no git link, so which repo deploys the site is unverified. Needs owner confirmation.
- Details: [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].

## Status 2026-10-08 23:41 (UTC+2): deploy source confirmed; new downloads showcase

- ✅ **Conflict resolved: which repo deploys portfolio-nine.**
  - The latest production deployment (`dpl_D3YGzcmFeTnmF9VHpuTaPrUJUFSo`, READY 2026-10-07 09:38) was built from the **public `nodaysidle/Portfolio`** repo, `master` @ `a225402` ("Publish full editorial portfolio source…"). It was deployed by hand from the CLI with `npx vercel --prod`; Vercel shows `source: cli`. Verified with the Vercel API.
  - Older deployments, up to 2026-09-18, came from the private `nodaysidle-portfolio` repo. That is per the user and Execution Operator; this agent did not check those older deployments.
  - The Vercel *project* is still named `nodaysidle-portfolio` and its framework setting is Vite.
- **Unchanged:** nodaysidle/Portfolio, the Vercel project `nodaysidle-portfolio` and nodaysidle-portfolio-nine.vercel.app were left untouched and remain the **official portfolio**.
- **New downloads showcase:** https://nodaysidle-apps.vercel.app ([nodaysidle-apps](https://github.com/nodaysidle/nodaysidle-apps)), live 2026-10-08 ~23:40. It offers Cascade, Sonora, WhisperBar and NODAYSIDLE Browser for Linux. See [[_system/templates/catalog/nodaysidle-apps]].
- showcase-v2 / nodaysidle-project-pages remain stale and not canonical.

## Update 2026-10-11 19:38 (ATLAS)

- nodaysidle/Portfolio PR #1 squash-merged as 9b9a0d8 (Oct 11 19:32, per Execution Operator, user-approved), deploying to nodaysidle-portfolio-nine.vercel.app. Added 4 cards, portfolio now 9 projects: nodaysrammar v1.0.1 (MIT), Kurek v0.2.0 (CC BY-NC 4.0), ShareGuard v0.1.2 (proprietary, no apps-site card), Browser for Linux v0.1.0 (no licence claim). macOS Browser card unchanged, renumbered 05/09 (its release still has no assets). Closes SWEEP Oct 11 gap 4 except the Browser-card download issue.

## Update 2026-10-11 20:10 (UTC+2) — weekly reconcile cross-check

- Live HTTP check re-confirmed 9 cards on https://nodaysidle-portfolio-nine.vercel.app (matches the 19:38 Portfolio PR #1 note above).
- Apps site still 6 tools; ShareGuard remains portfolio-only (no apps card).
- Full catalog reconcile: [[artifacts/vault-operations/repo-status-reconcile-2026-10-11]]. SWEEP portfolio-missing rows marked superseded in [[artifacts/vault-operations/sweep-2026-10-11-sunday-catalog]].

- 2026-10-12 03:50 (ATLAS): Portfolio PR #2 merged as 4a542d0: macOS NODAYSIDLE Browser card hidden per owner decision 2026-10-12; portfolio now 8 projects (closes reconcile 2026-10-11 conflict 3 for the portfolio).
- 2026-10-17 (Claude Opus, catalog reconcile against [[sessions/LATEST]] and [[artifacts/2026-10-17-vault-and-grokbot-audit]]): `repo_url` → **Portfolio** (the repo that deploys portfolio-nine, resolved 2026-10-08 23:41). `nodaysidle-project-pages` / showcase-v2 kept as `stale_repo_url` and `showcase_url` for history; not canonical.
