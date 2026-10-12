---
type: artifact
artifact_kind: audit
topic_slug: vault-operations
generated: 2026-10-11
generator_agent: ATLAS
verified_at: 2026-10-11T20:10:00+02:00
scope:
  - nodaysidle-cascade-v3
  - whisper-bar
  - nodaysidle-sonora
  - synapse-notes
  - nodaysidle-browser
  - nodaysidle-browser-linux
  - nodaysidle-shareguard
  - nodaysrammar
  - kureksistant
  - Portfolio
  - nodaysidle-apps
tags:
  - artifact
  - audit
  - repo-status
  - weekly-reconcile
---

# Audit: weekly repo status reconcile (2026-10-11)

Run 2026-10-11 ~20:07–20:15 (UTC+2) by Grok Bot (ATLAS executor). Inputs: [[artifacts/vault-operations/sweep-2026-10-11-sunday-catalog]], prior [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]], live GitHub API (`gh`), live portfolio + apps HTTP, Vercel MCP project list. Comparison/summary via box `ask-gemini`. **Vault only** — no GitHub/Vercel mutations. Times UTC+2 (CEST).

## Current status (verified ~20:10)

| Repo | Visibility | Latest release | Assets | README install → asset URL? | Demo GIF | Portfolio-nine | Apps site |
|---|---|---|---|---|---|---|---|
| nodaysidle-cascade-v3 | public | v3.1.0 | 4 (dmg, tar.gz, AppImage, deb) | Y | Y `docs/cascade.gif` | Y 01/09 | Y 01/06 |
| whisper-bar | public | v1.1.2 | WhisperBar.dmg | Y | Y | Y 02/09 | Y 03/06 |
| nodaysidle-sonora | public | v0.1.1 | 5 | Y | Y | Y 03/09 | Y 02/06 |
| synapse-notes | public | v0.4.3 | debug APK | Y | **N** | Y 04/09 | N |
| nodaysidle-browser | public | v2026.7.23 | **0** | N (source only) | **N** | Y 05/09 | N |
| nodaysidle-browser-linux | public | v0.1.0 | AppImage | **P** (releases index) | Y | Y 09/09 | Y 04/06 |
| nodaysidle-shareguard | public | v0.1.2 | DMG + sha256 | Y | Y | Y 08/09 | N |
| nodaysrammar | public | v1.0.1 | zip + sha256 | Y | Y | Y 06/09 | Y 05/06 |
| kureksistant | public | v0.2.0 | tar.gz + SUMS | Y | Y | Y 07/09 | Y 06/06 |

Org: `public_repos=38` (API). Canonical portfolio: https://nodaysidle-portfolio-nine.vercel.app (Vercel `nodaysidle-portfolio` ← public `Portfolio`). Apps: https://nodaysidle-apps.vercel.app (6 tools). Stale: showcase-v2 / project-pages.

Portfolio PR #1 `9b9a0d8` (merged 2026-10-11 19:32) already recorded in vault at 19:38; this reconcile closes remaining catalog/overview drift and marks SWEEP portfolio-missing rows superseded.

## SWEEP findings disposition

| SWEEP claim | Live | Vault action |
|---|---|---|
| Oct 8 SHIP gaps fixed (whisper / shareguard install; sonora notes) | Verified | Re-affirmed on catalogs |
| ShareGuard + browser-linux missing from portfolio | **False now** (on since PR #1) | ⚠️ Superseded markers + Update sections |
| nodaysrammar / kureksistant on apps, absent from portfolio | **False now** (on portfolio) | ⚠️ Superseded + Update |
| nodaysidle-browser 0 assets / theme notes / no GIF | True | Documented on catalog |
| synapse-notes no GIF | True | Documented |
| browser-linux Install → releases index | True (mild) | Documented |
| Public count 38; nodaysrammar may miss org bullets | True (apps + rammar missing from bullet list) | Bullets + frontmatter synced to 38 |

## Conflicts / open items

1. **cascade-v3 / sonora visibility history** — still open from Oct 8 (SWEEP said private-on-Oct-7; vault recorded public at 13:55 that day). Unchanged.
2. **browser-linux licence** — still none; apps card "No licence specified". Owner decision.
3. **nodaysidle-browser shippable download** — on portfolio but latest release has 0 assets; theme-only notes; source-only README. Route: SHIP (+ REEL for GIF).
4. **synapse-notes demo GIF** — on portfolio; no GIF in tree. Route: REEL.
5. **browser-linux Install URL** — mild; links `/releases` not direct AppImage download URL. Route: SHIP optional.

Resolved this pass: SWEEP/vault claims that four apps were missing from portfolio (live already had them after PR #1).

## Pages touched

See audit log entry 2026-10-11 20:10. New artifact: this file. ask-gemini plan archived on agent box at `/workspace/reconcile-2026-10-11/gemini-plan.md` (not in vault).

## Recommendation

- Do **not** re-ping ATLAS for portfolio-missing ShareGuard / browser-linux / nodaysrammar / Kurek.
- SHIP: macOS browser real release asset + README download Install; optional browser-linux direct AppImage link.
- REEL: demo GIFs for `nodaysidle-browser` and `synapse-notes`.
- Owner: browser-linux licence decision (unchanged).
