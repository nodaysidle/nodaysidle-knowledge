---
type: session
topic_slug: vault-operations
session_id: 2026-10-07-vault-operations
status: active
last_agent: Grok Bot (ATLAS)
last_updated: 2026-10-09T11:56:00+02:00
threads_active: []
tags:
  - session
---

# Session: Vault operations

## Resume here (read first)

- Inbox: [[inbox/2026-10-07-vault-operations-idea]]
- MOC: [[wiki/MOC/moc-nodaysidle-knowledge]]
- Catalog: [[_system/templates/CATALOG]]

## Decisions made

- Vault root: `/home/arch/dev/nodaysidle/nodaysidle-knowledge`
- Sibling code clones: `/home/arch/dev/nodaysidle/{repo}`

## Progress

- 2026-10-07 10:05 — Ingested 6 `nodaysidle-browser-linux` sources (README, audit, AGENT-HANDOFF [unreliable], APPIMAGE, v0.1.0 release notes, git log) at HEAD `2fffaab`; see `sources/README.md`.
- 2026-10-07 10:05 — Repo count verified: 36 public repos (09:31 log said 31; correction logged).
- 2026-10-07 10:10 — User correction: 48 total = 36 public + 12 private (kureksistant, cascade-v3, sonora, synapse-notes private); appended to org reference.
- 2026-10-07 10:15 — Wiki notes for browser-linux (overview, audit-status, appimage-packaging); A1–A9 re-checked at `2fffaab` (A5, A6 fixed; rest partial); AppImage = host-dependent.
- 2026-10-07 10:20 — Action 6 done: release-notes fix committed locally in browser repo (`a46b2cd`, unpushed); published SHA-256 = `f6d82efa…4404`; A1 → fixed.
- 2026-10-07 13:17 — Push of `a46b2cd` approved but **failed** (no GitHub HTTPS credentials; `gh` unauthenticated). Still 1 ahead of origin. Human must authenticate (e.g. `gh auth login`), then push.
- 2026-10-07 13:24 — Push retry failed with the same auth error; still 1 ahead.
- 2026-10-07 13:39 — User pushed `a46b2cd` (`2fffaab..a46b2cd`); fetch confirms origin/master = `a46b2cd`; A1 marked pushed. Release-body edit still optional (needs valid `gh`).
- 2026-10-07 13:50 — Ingested kureksistant (5 sources, 2 wiki notes). Found a licence conflict (MIT vs CC BY-NC 4.0); the GitHub API says the repo is public.
- 2026-10-07 13:55 — User decisions: kureksistant licence = CC BY-NC 4.0 (derived from FatihMakes' JARVIS; README MIT wrong); repo stays public. Reference corrected: the 4 "private" repos are public; private count unknown (48 total per user).
- 2026-10-07 14:00 — Cloned nodaysidle-cascade-v3, nodaysidle-sonora, synapse-notes (anonymous HTTPS). Ingested 29 sources (cascade 5, sonora 13, synapse 11) + 3 overview wiki notes.
- 2026-10-07 14:05 — kureksistant README licence fixed (`3930a18`, pushed via SSH, b072178..3930a18). Sonora Spotify path settled: Connect first, YouTube fallback; Librespot unwired. Drafted brief `briefs/draft/nodaysidle-browser-linux-audit-completion-brief-v1.md` (review_status: pending).
- 2026-10-07 14:20 — Applied user decisions (items 1–24): 5 commits. kureksistant pushed (SSH); browser-linux, cascade-v3, sonora and synapse-notes push pending HTTPS auth. Librespot left in place; synapse Q&A doc change withheld (the code shows no screen).
- 2026-10-07 14:18 — Recorded the 12 private repos; org count resolved (48). Four pushes still waiting on the user (browser-linux a124f2f, cascade-v3 b5d1d1d, sonora f34945b, synapse-notes d659005).
- 2026-10-07 14:19 — Verified user pushes on origin: browser-linux a124f2f, cascade-v3 b5d1d1d, sonora f34945b, synapse-notes d659005. Synapse Q&A wording kept as is.
- 2026-10-07 14:24 — Browser brief closed as not needed (user-attested). Sonora Librespot player removed (`2c0e052`); push waiting on user.
- 2026-10-07 14:20 — Implemented video generation optimizer for Veo 3.1, Omni, Kling, and Runway with TypeSafe Jev diagnostics in `nodaysidle-prompt-optimizer` (`a6f4718`, pushed & deployed to Vercel). Added wiki concept note `wiki/concepts/nodaysidle-prompt-optimizer-overview.md` and updated catalog and MOC.
- 2026-10-07 14:27 — Verified sonora push: origin/main = 2c0e052.
- 2026-10-08 02:50 — REACH added X promo notes: [[wiki/MOC/moc-x-promo]] (strategy, Oct calendar + drafts, REEL clip workflow + README GIF PRs). Local clones of whisper-bar, cascade-v3, sonora, shareguard, browser-linux are 1 commit behind origin.
- 2026-10-08 03:32 — Execution Operator: kureksistant audit (C−), v0.1.0 re-cut without leaked keys (SHA-256 `a4085d73…1003`), PR #2 (`31d7e56`) and PR #3 (`52d009b`) merged. Details: [[sessions/2026-10-08-kureksistant-session]].
- 2026-10-08 03:52 — Installed 6 Obsidian community plugins (`dataview`, `templater-obsidian`, `table-editor-obsidian`, `obsidian-linter`, `omnisearch`, `obsidian-local-rest-api`) into `.obsidian/plugins/` per user approval.
- 2026-10-08 05:08 — Configured Templater `templates_folder` to `_system/templates` in `.obsidian/plugins/templater-obsidian/data.json`.
- 2026-10-08 22:35 — Grok Bot (ATLAS) reconciled repo status for whisper-bar, cascade-v3, sonora, shareguard and browser-linux (API-verified 22:30). Created a ShareGuard catalog entry, added status sections, and marked conflicts and stale items. See [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].
- 2026-10-08 22:32 — Verified the owner-approved squash merges: whisper-bar PR #2 → `239f1a7` and shareguard PR #4 → `eeaaca0` (both merged 22:30). The ShareGuard README now links the DMG, so the ZIP conflict is resolved.
- 2026-10-08 23:41 — Grok Bot (ATLAS) recorded the new downloads showcase https://nodaysidle-apps.vercel.app (repo `nodaysidle-apps`, PR #1 `44052bc`; Vercel `nodaysidle-apps`, deployment READY; 200 + 11/11 downloads 302). Added catalog entry [[_system/templates/catalog/nodaysidle-apps]]. The portfolio-nine deploy-source conflict is resolved (public `Portfolio` `a225402`, CLI deploy). SHIP's 22:47–22:58 fixes are already in the reconcile artifact. Catalog pages now point to them.
- 2026-10-09 10:32 — Grok Bot (ATLAS) checked nodaysrammar (new public repo, v1.0.0, MIT) against Antigravity's 09:56 notes. Marked the conflicts: ONNX Runtime bundled but unused, models generated rather than trained, release has no assets or checksums, USERGUIDE hardcodes a local path. Org count is now 38. See [[artifacts/nodaysrammar/repo-check-2026-10-09]].
- 2026-10-09 10:34–10:35 — Corrected the "could of" finding (the rule exists at `inference-engine.js:252`). Set nodaysrammar to needs-work (catalog, overview, CATALOG row).
- 2026-10-09 10:57–10:58 — Another agent (unattributed, no audit entry) recorded v1.0.1 on the nodaysrammar catalog page and overview and set them to active.
- 2026-10-09 11:56 — Grok Bot (ATLAS): nodaysrammar is **active and released**: v1.0.1 (`ce2cbd7`, zip SHA-256 verified) plus CI `81082cf`. It is card 05 on nodaysidle-apps (`aab4c1d`, 12/12 links 302). The homepage and topics are fixed. Every audit contradiction is resolved. See [[artifacts/nodaysrammar/repo-check-2026-10-09]].
- 2026-10-09 17:40 — REACH added [[wiki/concepts/x-promo-strategy-2026-10-12]] (X plan from Mon 12 Oct: nodaysrammar Tue 13, showcase roundup Fri 16, week-1 drafts); linked from [[wiki/MOC/moc-x-promo]]. Drafts only.

## Do not re-fetch

- `nodaysidle-browser-linux` docs at `2fffaab` (already in `sources/raw/docs/`); re-ingest only if HEAD moves.

## Next actions

1. Validate and expand atomic wiki concept coverage across active portfolio projects.
2. ~~Ingest in-progress projects~~ all five done (browser-linux, kureksistant, cascade-v3, sonora, synapse-notes).
3. Prepare reviewable candidate briefs under `briefs/` awaiting human promotion approval.
4. ~~Browser-linux wiki notes + A1–A9 check + AppImage verdict~~ done 10:15.
5. ~~AGENT-HANDOFF.md~~ marked historical (`a124f2f`).
6. ~~Release-notes AppImage fix~~ committed `a46b2cd` (local). Pushed 13:39. Optional: add host-dependency + SHA-256 lines to the GitHub release body (needs authenticated `gh`). ✅ 2026-10-08 22:30: the v0.1.0 release body already has both lines; nothing left to do.
7. Browser follow-ups: A3 confusables policy; A4 document-level recheck; A2 pin appimagetool URL / checksum PATH tool; A9 CI now that origin exists.
8. Private repos: the 4 named are public (corrected 13:55). Name the actual private repos and re-sync with an authenticated `gh` to verify the 48 total.
9. ~~Remaining ingests~~ done 14:00 (repos are public).
10. ~~Kureksistant licence/visibility~~ resolved 13:55: CC BY-NC 4.0, stays public.
11. ~~kureksistant README licence fix~~ done 14:05: commit `3930a18` pushed (footer + badge). Still open: tool count (17/20/28) and JARVIS paths in AGENTS.md.
12. ~~Doc fixes per repo~~ committed 14:20 (`b5d1d1d`, `f34945b`, `d659005`). Pushed by user; verified on origin 14:19 (fetch: origin == local for all four).
13. ~~Sonora Spotify path~~ done 14:05: Connect first, YouTube fallback, Librespot unwired (see the sonora wiki note).
14. Human: review the brief `briefs/draft/nodaysidle-browser-linux-audit-completion-brief-v1.md` (move it to `in-review/` or give feedback).
15. ~~Synapse Q&A~~ resolved 14:19: user keeps README wording as is (ask-notes Edge Function, no UI caller); no doc change.
16. ~~Sonora Librespot removal~~ committed 14:24 as `2c0e052`: cargo check, clippy and test pass. Pushed by user; verified origin/main = 2c0e052 at 14:27.
17. Optional (needs `gh`): update the GitHub release bodies (cascade v3.1.0 Linux steps and Jev key; synapse v0.2.0 status names). As of 2026-10-08 22:30, the cascade v3.1.0 body is still DMG-only.
18. ~~Org repo count~~ resolved 14:18: 36 public + 12 private = 48 (the user listed the private repos; see `_system/reference/github-org-repositories.md`).
19. Human: review [whisper-bar PR #2](https://github.com/nodaysidle/whisper-bar/pull/2) and [shareguard PR #4](https://github.com/nodaysidle/nodaysidle-shareguard/pull/4). Both are drafts and README-only. ✅ Done 2026-10-08 22:30: the owner approved both and they were squash-merged (`239f1a7`, `eeaaca0`); verified 22:32.
20. Human: confirm which repo deploys portfolio-nine (`Portfolio` or private `nodaysidle-portfolio`), and whether ShareGuard and browser-linux should be added to it. ✅ 2026-10-08 23:41: deploy source = public `Portfolio` (`a225402`, CLI). portfolio-nine is unchanged. browser-linux is on the new downloads showcase [[_system/templates/catalog/nodaysidle-apps]]; ShareGuard is not.
21. Human: WhisperBar licence. The README says MIT, but GitHub detects no LICENSE file.
22. Optional: ShareGuard's theme-only `v0.1.1` release (no assets) looks newer than the real `v0.1.0-dmg.20260727` app release. Rename or annotate it?
23. Human: browser-linux licence. The repo has none, so its downloads-showcase card says "No licence specified". This is the owner's decision.
24. Human: nodaysrammar. Either wire up ONNX Runtime Web or drop the WASM/ONNX claims, and describe the models accurately (they are not trained). ✅ Done `ce2cbd7` (dropped).
25. Human: nodaysrammar v1.0.0. Attach a packaged zip + SHA-256, or drop the "Checksums" wording. Also fix the `/home/arch/...` path in USERGUIDE. ✅ Done: v1.0.1 zip + SHA-256, and the path was removed (`ce2cbd7`).
26. Optional: run nodaysrammar `npm test` and ingest README, USERGUIDE and AGENTS.md as sources. (CI now runs the browser tests and fails instead of skipping, `81082cf`.)
27. Human: nodaysrammar is not on the Chrome Web Store (sideload only). Decide whether to list it.
28. Human: `git pull` in `/home/arch/dev/nodaysidle/chrome-extension` (local HEAD `4f41689`, origin `main` = `81082cf`).

## Thread registry

| Thread | Focus | Status | Last output |
|--------|--------|--------|-------------|
| browser-linux audit completion | brief A2–A4, A7–A9 | draft / pending review | [[briefs/draft/nodaysidle-browser-linux-audit-completion-brief-v1]] |

## Handoff notes

Promotion still requires human `review_status: approved` on briefs. Never delete `sources/raw/`.

- **Process (2026-10-09 11:56, per user):** teammate bots report to Execution Operator, and the owner talks only to Execution Operator.

- 2026-10-11 19:07: SWEEP Oct 11 18:13 weekly catalog sweep recorded in [[artifacts/vault-operations/sweep-2026-10-11-sunday-catalog]]. OPEN: (1) nodaysidle-browser (macOS) v2026.7.23 has 0 assets, install covers source builds only, not shippable; (2) browser-linux install links the releases index, not the AppImage; (3) nodaysidle-browser and synapse-notes have no demo GIF; (4) nodaysrammar, kureksistant, ShareGuard and browser-linux missing from the portfolio (nodaysidle-portfolio-nine), whose Browser card points at a release with no downloads. CLEARED: whisper-bar and shareguard README install links; sonora release notes. Uncommitted.

- 2026-10-11 19:38: nodaysidle/Portfolio PR #1 squash-merged as 9b9a0d8 (Oct 11 19:32, per Execution Operator, user-approved), deploying to nodaysidle-portfolio-nine.vercel.app. Added 4 cards, portfolio now 9 projects: nodaysrammar v1.0.1 (MIT), Kurek v0.2.0 (CC BY-NC 4.0), ShareGuard v0.1.2 (proprietary, no apps-site card), Browser for Linux v0.1.0 (no licence claim). macOS Browser card unchanged, renumbered 05/09 (its release still has no assets). Closes SWEEP Oct 11 gap 4 except the Browser-card download issue.

- 2026-10-11 20:10: ATLAS weekly wiki reconcile. Live: public_repos=38; portfolio-nine 9 apps (PR #1 already recorded 19:38); apps site 6. Marked SWEEP portfolio-missing rows superseded. Synced org bullet list (+nodaysidle-apps, +nodaysrammar). Updated catalogs/overviews for ShareGuard, browser-linux, nodaysrammar, Kurek, macOS browser (0 assets), synapse-notes (no GIF). Artifact [[artifacts/vault-operations/repo-status-reconcile-2026-10-11]]. ask-gemini used for comparison. Uncommitted.

- 2026-10-12 03:32: Owner decisions 2026-10-12 (via Execution Operator): (1) macOS NODAYSIDLE Browser card to be hidden from the portfolio (no Macs available); (2) nodaysrammar stays off the Chrome Web Store for now (cost, no ROI; sideload only); (3) Kurek security fixes (unauthenticated HTTP :8790, exec() in actions/desktop.py) parked while the owner tests; he is prototyping phone-based remote control of Kurek. ⚠️ Risk: remote control would expose the unauthenticated control API and model-generated exec() beyond localhost; fix auth before exposing it.

- 2026-10-12 03:35: REEL demo clip status (box /workspace/clips/<app>/, not committed to repos): synapse-notes (real screenshots, personal notes blurred, no voice-capture footage) and browser-linux v0.1.0 (real AppImage footage) now have GIF+MP4, closing their no-demo-GIF gap once committed to the repos. Also ready: whisperbar, shareguard, cliprail (icon+text), cascade (real footage), sonora (real footage, explicit title blurred), nodaysrammar v1.0.1 (real Chromium), kurek v0.2.0 (icon+text). macOS nodaysidle-browser skipped (card being hidden). Note: REEL says kurek README demo.gif is a mock-up, but kureksistant PR #8 022d4be already replaced it with REEL's real v0.2.0 GIF; REEL's note is stale on that point.

- 2026-10-12 03:50 (ATLAS): kureksistant PR #10 squash 395d7bf (2026-10-12 03:49, per Execution Operator): optional Microsoft-Decision-1 auto-screen decision via OpenRouter with TypeSafe fallback, 1.5s timeout, KUREK_AUTO_SCREEN=0 opt-out, validated null. ⚠️ Privacy risk: prompt text is sent to OpenRouter when the key is set. No latency claims. | browser-linux PR #2 merged as 31ede82: README install now links the AppImage directly (closes reconcile 2026-10-11 conflict 5). | Portfolio PR #2 merged as 4a542d0: macOS NODAYSIDLE Browser card hidden per owner decision 2026-10-12; portfolio now 8 projects (closes reconcile 2026-10-11 conflict 3 for the portfolio).

- 2026-10-12 05:12 (ATLAS): 🏁 Milestone 2026-10-12 ~05:00 (per Execution Operator): the owner has a working Kurek.apk on Android that controls Kurek on the PC by voice, remotely over Tailscale, tested on mobile data. ⚠️ OPEN RISK (security): the :8790 control API has no authentication and actions/desktop.py exec()s model-generated code; remote access widens exposure to every device on the tailnet. SHIP is reviewing the repo and security; treat it as open until SHIP reports.

- 2026-10-12 05:31 (ATLAS): ✅ CLOSED: Kurek remote OPEN RISK (from the 2026-10-12 ~05:00 milestone), per Execution Operator, user-approved. kureksistant PR #11 squash 822966c (05:31): loopback bind by default (KUREK_REMOTE_BIND=tailscale opt-in); required Bearer token with compare_digest for remote requests; CSRF/Origin blocks, no CORS *; 64KB body cap; remote exec tools gated by KUREK_REMOTE_ALLOW_EXEC; hardcoded token and IP removed from the Android app, release/kurek-remote.apk deleted; SECURITY.md added. Leaked token rotated by the owner (old one returns 401); still in git history but inert. No published APK release. Remaining (local only): actions/desktop.py still exec()s model-generated code for local use; the localhost API is unauthenticated by design when loopback-bound. Not re-verified by ATLAS (cheap mode).
