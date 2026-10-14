# Audit log

Append-only record of promotions and significant vault edits. Agents may append; never delete or rewrite prior entries.

## 2026-10-07T09:30:00+02:00 — bootstrap

- **Actor:** human+agent (vault bootstrap)
- **Action:** initialize vault layout
- **Paths:** `_audit/log.md`, `inbox/`, `sessions/`, `wiki/MOC/`, `briefs/`, `projects/`, `sources/`, `artifacts/`
- **Notes:** Catalog URLs set for markdown-helper, skill-gallery, portfolio production site. GitHub repos for markdown-helper and skill-gallery are canonical names; publish when ready.

## 2026-10-07T09:31:00+02:00 — sync github org

- **Actor:** agent
- **Action:** align catalog with https://github.com/nodaysidle?tab=repositories (31 public repos)
- **Paths:** `_system/reference/github-org-repositories.md`, catalog entries for markdown-helper, skill-gallery, portfolio-site, nodaysidle-browser-linux
- **Notes:** `markdown-helper`, `skill-gallery`, `Portfolio`, and `nodaysidle-browser-linux` are local workspace only until pushed. Public portfolio surfaces: `nodaysidle-project-pages`, `nodaysidle/nodaysidle`.

## 2026-10-07T09:35:00+02:00 — publish repos

- **Actor:** human+agent
- **Action:** create public GitHub repositories and push initial sources
- **Repos:** nodaysidle-knowledge, markdown-helper, skill-gallery, nodaysidle-browser-linux, Portfolio
- **Notes:** README headers aligned with nodaysidle portfolio style (centered title, badges, problem/result block).

## 2026-10-07T09:43:00+02:00 — agy bootstrap run

- **Actor:** agy (Research Orchestrator) | **Action:** validated first-reads, created `wiki/concepts/agent-entrypoint-checklist.md`, linked MOC, updated session state.

## 2026-10-07T09:51:00+02:00 — align cursor & pi agents

- **Actor:** human+agent | **Action:** add `_system/config/cursor-pi-vault-bootstrap.md`, `.cursorrules`, and `AGENTS.md` to automate agent alignment without manual prompting.

## 2026-10-07T10:05:00+02:00 — correction: public repo count (re: 09:31 entry)

- **Actor:** agent (Grok Bot)
- **Action:** count check only; prior entries left unchanged
- **Finding:** the 09:31 entry says "31 public repos"; the correct current count is **36**. `_system/reference/github-org-repositories.md` lists 36 and the public GitHub API (`/users/nodaysidle/repos`, per the reference's re-sync command) returned 36 names, identical to the reference list (empty diff). `gh repo list` was unavailable (gh not authenticated).
- **Likely cause:** 31 was the count before the 09:35 publish of 5 repos (nodaysidle-knowledge, markdown-helper, skill-gallery, nodaysidle-browser-linux, Portfolio); 31 + 5 = 36. Inferred, not confirmed.

## 2026-10-07T10:05:00+02:00 — ingest nodaysidle-browser-linux sources

- **Actor:** agent (Grok Bot)
- **Action:** ingest 6 sources from `../nodaysidle-browser-linux` (HEAD `2fffaab`); verbatim copies to `sources/raw/docs/`, index stubs to `sources/index/`, table added to `sources/README.md`
- **Paths:** `sources/index/src-20261007-{2d7bab4,030f677,6223dc7,e79ab38,1764cc7,e02f632}-browser-linux-*.md`, matching `sources/raw/docs/` files
- **Notes:** `docs/AGENT-HANDOFF.md` flagged unreliable (secondary; says no git remote, but `origin` exists). No `AUDIT.md`, `PRD.md`, `ARD.md`, `TRD.md` or `TASKS.md` in repo; `agenthandoff_audit.md` ingested as the audit. Release notes ("Portable") contradict APPIMAGE.md (host-dependent). Browser repo not modified.

## 2026-10-07T10:10:00+02:00 — repo total incl. private (user correction)

- **Actor:** agent (Grok Bot), per user correction
- **Action:** appended a note to `_system/reference/github-org-repositories.md`: 48 total = 36 public + 12 private. Private (per user): kureksistant, nodaysidle-cascade-v3, nodaysidle-sonora, synapse-notes; the other 8 are unnamed. Public list untouched.
- **Notes:** `public_repo_count: 36` frontmatter kept. Conflict: the public API listing at 10:05 included these four repos. Unverified; flagged for re-sync. The 10:05 "36" correction is about public repos only and still stands.

## 2026-10-07T10:15:00+02:00 — nodaysidle-browser-linux wiki notes + audit re-check

- **Actor:** agent (Grok Bot)
- **Action:** created 3 draft wiki concept notes and linked them from `wiki/MOC/moc-nodaysidle-knowledge.md`
- **Paths:** `wiki/concepts/nodaysidle-browser-linux-{overview,audit-status,appimage-packaging}.md`
- **Notes:**
  - Audit A1–A9 re-checked at `2fffaab`: A5 and A6 fixed; A1–A4 and A7–A9 partial.
  - fmt, clippy and test (65 passed) all green. Build output went to `/tmp/ndi-check-target`; the browser repo is unmodified.
  - AppImage verdict: host-dependent is correct; the release notes' "Standalone/Portable" is wrong. The repo fix is suggested, not applied.

## 2026-10-07T10:20:00+02:00 — AppImage wording fix (session action 6, user-approved)

- **Actor:** agent (Grok Bot), with user approval
- **Action:** browser repo `docs/RELEASE-NOTES-v0.1.0.md`:
  - "Standalone/Portable" → "Host-dependent AppImage, requires system GTK 3 + WebKitGTK 4.1";
  - SHA-256 `06a91e47…` → `f6d82efa…4404`, the published asset's value; the local `dist/` build is identical.
- **Commit:** `a46b2cd`, local only, not pushed. The GitHub release body was not edited (`gh` not authenticated; the body has no standalone wording).
- **Vault:** updated `wiki/concepts/nodaysidle-browser-linux-appimage-packaging.md` and `…-audit-status.md` (A1 → fixed).

## 2026-10-07T13:17:00+02:00 — push attempt for browser-linux a46b2cd (failed)

- **Actor:** agent (Grok Bot), with user approval to push
- **Action:** `git push origin master` (no force) in `nodaysidle-browser-linux`. `a46b2cd` is the only commit ahead of `origin/master`.
- **Result:** failed, exit 128: `fatal: could not read Username for 'https://github.com': terminal prompts disabled`. No credentials are configured for HTTPS and `gh` is not authenticated. No retry or token workaround was attempted. A1 is still unpushed.

## 2026-10-07T13:24:00+02:00 — push retry for browser-linux a46b2cd (failed again)

- **Actor:** agent (Grok Bot), with user approval ("Push it")
- **Result:** `git push origin master` (no force) failed with exit 128, the same error as before: `fatal: could not read Username for 'https://github.com': terminal prompts disabled`. `a46b2cd` is still the only commit ahead. No workaround attempted; A1 is still unpushed.

## 2026-10-07T13:39:00+02:00 — browser-linux a46b2cd pushed (by user)

- **Actor:** human (push); agent (verification + vault update)
- **Result:** user pushed `2fffaab..a46b2cd master -> master`. Agent `git fetch`: `origin/master` = `a46b2cd`, branch in sync (the fetch also brought in tag `v0.1.0`).
- **Vault:** A1 marked pushed in `wiki/concepts/nodaysidle-browser-linux-audit-status.md`; session progress updated.

## 2026-10-07T13:50:00+02:00 — ingest kureksistant sources + wiki notes

- **Actor:** agent (Grok Bot)
- **Action:** ingested 5 sources from `../kurekizmo` (upstream `kureksistant`, HEAD `b072178`): README, AGENTS.md, `dist/RELEASE_NOTES.md`, `dist/SHA256SUMS.txt`, git log. Verbatim copies went to `sources/raw/docs/` and index stubs to `sources/index/`; rows added to `sources/README.md`.
- **Wiki:** `wiki/concepts/kureksistant-{overview,source-discrepancies}.md` (draft), linked from the MOC.
- **Notes:**
  - No PRD, ARD, TRD or TASKS files exist; `docs/` holds only `demo.gif` (binary, skipped).
  - AGENTS.md is tagged secondary because it has JARVIS-era paths.
  - The release checksum matches the published asset.
  - Contradictions found: README says MIT but LICENSE is CC BY-NC 4.0 (FatihMakes / JARVIS header); tool count 17 vs 20 vs 28 modules.
  - The GitHub API reports the repo as **public**, which conflicts with the user's 10:03 "private" statement. Not resolved.
  - Repo not modified.

## 2026-10-07T13:55:00+02:00 — kureksistant decisions + repo-reference correction (user)

- **Actor:** user decisions; agent recorded them
- **Decisions:**
  - kureksistant licence is CC BY-NC 4.0, because it is derived from FatihMakes' JARVIS; the README's MIT line is wrong;
  - kureksistant stays public.
- **Paths:** `wiki/concepts/kureksistant-source-discrepancies.md` (decisions section), `_system/reference/github-org-repositories.md` (new correction entry), session actions 10 (resolved) and 11 (README licence fix proposed; repo not edited).
- **Correction:** the 4 repos called private in the 10:10 entry are public, so the private count is unknown; 48 total is per the user and unverified. Prior entries are left unchanged.

## 2026-10-07T14:00:00+02:00 — clone + ingest cascade-v3, sonora, synapse-notes

- **Actor:** agent (Grok Bot), user-approved clone
- **Clones:** plain `git clone https://github.com/nodaysidle/<name>.git` into `/home/arch/dev/nodaysidle/`; none existed beforehand. Results:
  - nodaysidle-cascade-v3 @ `20f7098`
  - nodaysidle-sonora @ `b2f9a2d`
  - synapse-notes @ `a6e10fa`
- **Ingest:** 29 sources (cascade 5, sonora 13, synapse 11). Each has a verbatim copy in `sources/raw/docs/` and an index stub in `sources/index/`; rows added to `sources/README.md`. GitHub release bodies were fetched from the public API into one file per repo.
- **Wiki:** `wiki/concepts/{cascade-v3,nodaysidle-sonora,synapse-notes}-overview.md` (draft), linked from the MOC.
- **Notes:**
  - Each overview lists its contradictions.
  - Sonora's `docs/AGENT.md` is a duplicate of `docs/AGENTS.md`; ingested once.
  - Skipped as out of scope: cascade `ROADMAP.md`, `CLAUDE.md`, `audit/CHANGELOG.md`; synapse subfolder AGENTS.md files.
  - Repos not modified.

## 2026-10-07T14:05:00+02:00 — kureksistant licence fix, sonora Spotify verdict, browser-linux brief

- **Actor:** agent (Grok Bot), user-approved
- **kureksistant (repo):** commit `3930a18` changes the README licence footer to CC BY-NC 4.0 (link to LICENSE, credit to FatihMakes' "MARK 53 — JARVIS") and the licence badge from MIT to CC BY-NC 4.0. `git push origin main` succeeded over SSH (`b072178..3930a18`).
- **sonora (read-only):** at `b2f9a2d`, Spotify plays via Spotify Connect (Web API `PUT /me/player/play`) with a YouTube Music fallback. `NativeSpotifyPlayer` (librespot) is present but not referenced from `lib.rs`. Evidence is in the `wiki/concepts/nodaysidle-sonora-overview.md` verdict section. Session action 13 is done.
- **Brief:** `briefs/draft/nodaysidle-browser-linux-audit-completion-brief-v1.md` (`review_status: pending`, `promoted: false`). Nothing written to `projects/`.

## 2026-10-07T14:20:00+02:00 — apply user decisions across 5 repos

- **Actor:** agent (Grok Bot), user-approved. One commit per repo; no history rewrite or force push.
- **Commits:**
  - browser-linux `a124f2f`: AGENT-HANDOFF banner. **Push failed** (HTTPS auth).
  - kureksistant `99a7cec`: 28 tools, AGENTS.md aligned with README. **Pushed** over SSH (`3930a18..99a7cec`).
  - cascade-v3 `b5d1d1d`: Linux install and checksums, one-repair wording, Jev key, historical spec banner. **Push failed** (HTTPS auth).
  - sonora `f34945b`: Connect + YouTube fallback docs, Windows claims dropped, <90MB target, v0.1.1/rpm links, paths fixed, `docs/AGENT.md` deleted, TASKS ticks verified in code, bridge comment fixed. **Push failed** (HTTPS auth).
  - synapse-notes `d659005`: codemap Android-only plus history note, January plans superseded, doc pointers fixed. **Push failed** (HTTPS auth).
- **Not done:**
  - Librespot removal: not a clean removal; shared items are imported from `native_player.rs`.
  - Synapse Q&A doc change: the code shows no screen calls `ask-notes`.
  - GitHub release bodies: `gh` is not logged in.
- **Vault:** decision sections added to the browser audit-status note, the brief, and the kureksistant, cascade, sonora and synapse wiki notes. Org repo count left open.

## 2026-10-07T14:18:07+02:00 — private repo list recorded; org count resolved

- **Actor:** agent (Grok Bot), per user.
- **Change:** appended the 12 private repos (name, language, description) to `_system/reference/github-org-repositories.md`. **Total: 36 public + 12 private = 48. Resolved.**
- **Notes:**
  - `kurekizmo` is a private repo. `kureksistant` is public.
  - The local `kurekizmo` folder has an old-origin remote that points at `kureksistant`.
  - The 10:10 entry's list of four "private" repos was wrong; those four are public.
- **Source and edits:** the user's list; not API-verified. No earlier entries were edited.
- **Pending:** the user's pushes of `a124f2f` (browser-linux), `b5d1d1d` (cascade-v3), `f34945b` (sonora) and `d659005` (synapse-notes).

## 2026-10-07T14:19:52+02:00 — user pushes verified; synapse Q&A kept

- **Actor:** agent (Grok Bot), per user.
- **Verification:** ran `git fetch origin` in four repos. Each origin branch equals the local HEAD, with no ahead/behind:
  - nodaysidle-browser-linux `master` = `a124f2f`
  - nodaysidle-cascade-v3 `main` = `b5d1d1d`
  - nodaysidle-sonora `main` = `f34945b`
  - synapse-notes `main` = `d659005`
- **Decision:** the synapse-notes Q&A wording stays as is. The README says ask-notes is not in the UI. No change.
- **Session:** action 12 done; action 15 resolved.

## 2026-10-07T14:20:00+02:00 — prompt-optimizer video generation expansion & wiki documentation

- **Actor:** agent (Antigravity), per user request.
- **Repo (`nodaysidle-prompt-optimizer`):**
  - Added dedicated `video` prompt optimizer supporting Google Veo 3.1, Google Omni, Kling (1.5/2.0), and Runway (Gen-3 Alpha).
  - Enforced structured section-tagged plain text (`[SCENE & SUBJECT]`, `[TEMPORAL ACTION & DYNAMICS]`, `[CAMERA PATH & CINEMATOGRAPHY]`, `[LIGHTING & ATMOSPHERE]`, `[NEGATIVE / ARTIFACT GUARDS]`) instead of raw JSON dictionaries to remove copy-paste friction into generative video models.
  - Extended TypeSafe Jev System One diagnostics for video: audits temporal progression (`lacks_temporal_action`) and camera trajectory choreography (`lacks_camera_movement`).
  - Added preset examples (Veo 3.1 Supermoto Drift, Kling/Runway FPV Chase) and UI target chips.
  - Committed (`a6f4718`), pushed to GitHub (`origin master`), and redeployed to Vercel production (`https://nodaysidle-prompt-optimizer.vercel.app`).
- **Vault (`nodaysidle-knowledge`):**
  - Created wiki concept note `wiki/concepts/nodaysidle-prompt-optimizer-overview.md`.
  - Updated `_system/templates/catalog/nodaysidle-prompt-optimizer.md` and linked in `wiki/MOC/moc-nodaysidle-knowledge.md`.


## 2026-10-07T14:24:52+02:00 — browser brief closed; Sonora Librespot removal

- **Actor:** agent (Grok Bot), per user.
- **Browser:**
  - Brief `nodaysidle-browser-linux-audit-completion-brief-v1` is now `status: closed-not-needed`, with a banner. review_status stays pending; nothing written to `projects/`.
  - Audit-status note: the user confirmed the browser works. This is user-attested, not agent-verified.
- **Sonora `2c0e052`:**
  - Removed the unused Librespot player and the `librespot` dependency (Cargo.lock: −102 packages).
  - `cargo check`, `cargo clippy` and `cargo test` pass.
  - **Push failed** (HTTPS auth). The user needs to run `git push origin main`.
- **Session:** action 16 done; push pending.

## 2026-10-07T14:27:16+02:00 — sonora push verified

- **Actor:** agent (Grok Bot), per user.
- **Check:** ran `git fetch` in nodaysidle-sonora; origin/main = `2c0e052` = local HEAD (the user pushed `f34945b..2c0e052`).
- **Session:** action 16 is complete.

## 2026-10-08T02:50:00+02:00 — X promo strategy and REEL workflow notes

- **Actor:** agent (REACH, Grok Bot), per user via dr eggbot; user approved the vault write in chat.
- **Added:** `wiki/MOC/moc-x-promo.md`, `wiki/concepts/x-promo-strategy.md`, `wiki/concepts/x-promo-calendar-2026-10.md`, `wiki/concepts/reel-clip-workflow.md`.
- **Edited:** `wiki/MOC/moc-nodaysidle-knowledge.md` (added an "X promo" section, nothing else changed).
- **Notes:** the README GIF PRs were merged on GitHub 2026-10-07 (whisper-bar #1, cascade-v3 #2, sonora #2, shareguard #3, browser-linux #1), so local clones are behind origin. Nothing committed in this vault.

## 2026-10-08T03:40:00+02:00 — kureksistant audit, release re-cut, PRs #2/#3 (logged)

- **Actor:** agent (Execution Operator, Grok Bot), per user. The repo work ran in Cursor cloud agent `bc-e01c8f24-b3e6-5c91-afb6-bee6dd7d455c`, 2026-10-08 02:57–03:32.
- **Audit:** read-only audit of `kureksistant` `main` @ `99a7cec`; grade C−. Report filed as `artifacts/kureksistant/audit-2026-10-08.md` (verbatim body; no secrets in it).
- **Release (user-approved):**
  - The public v0.1.0 tarball contained `config/api_keys.json` with likely-live Gemini and OpenRouter keys.
  - The asset was re-cut on the same tag without secrets. New SHA-256 `a4085d73ae8764f6b9034e3caabd4c4278f345d074f7909dad171dea63861003`; `SHA256SUMS.txt` replaced; verified 0 `api_keys.json` and 0 `.env`.
  - The user's local `api_keys.json` was left untouched on purpose.
  - **Pending, human:** revoke the old keys. Unconfirmed.
- **PRs (user-approved merges, CI green):**
  - [#2](https://github.com/nodaysidle/kureksistant/pull/2) → `31d7e56`: legacy GUI moved to `legacy/`, SECURITY.md/NOTICE/SPDX licence, `.env` settings, CI, package deny-list.
  - [#3](https://github.com/nodaysidle/kureksistant/pull/3) → `52d009b`: docs now say ~333MB / 24 tools.
- **GitHub settings:** the user set the topics and description by hand (the Cursor app got a 403 on topics).
- **Vault:**
  - **Added:** the artifact above and `sessions/2026-10-08-kureksistant-session.md`.
  - **Edited:**
    - `wiki/concepts/kureksistant-overview.md` (current-status section);
    - `wiki/concepts/kureksistant-source-discrepancies.md` (audit findings section);
    - `sessions/LATEST.md` (points at the new session; previous kept);
    - `sessions/2026-10-07-vault-operations-session.md` (one progress line);
    - `wiki/MOC/moc-nodaysidle-knowledge.md` (links);
    - `_system/templates/catalog/kurekizmo.md` (short_description, status line).
  - Earlier entries not modified. Nothing under `projects/`. Nothing committed in this vault.
- **Open (deferred by user):** `/prompt` UnboundLocalError (`kurek_daemon.py:505`), `dream_cycle` str-vs-dict, F821s, installer deps, unauthenticated control API, `exec` in `actions/desktop.py`, ruff/mypy errors in legacy code.

## 2026-10-08T03:52:00+02:00 — install obsidian community plugins suite

- **Actor:** agent (Antigravity), per user request ("all of them that you recommended").
- **Action:** installed 6 Obsidian community plugins to `.obsidian/plugins/` and configured `.obsidian/community-plugins.json`.
- **Plugins installed:**
  - `dataview` (v0.5.70, blacksmithgu/obsidian-dataview) — query YAML frontmatter tables and metadata across sessions, MOCs, briefs, and sources.
  - `templater-obsidian` (v2.25.1, SilentVoid13/Templater) — template automation for research scaffolds and catalog entries.
  - `table-editor-obsidian` (v0.23.2, tgrosinger/advanced-tables-obsidian) — markdown table editing and alignment.
  - `obsidian-linter` (v1.33.0, platers/obsidian-linter) — markdown and YAML formatting normalization across multi-agent sessions.
  - `omnisearch` (v1.31.0, scambier/obsidian-omnisearch) — full-text fuzzy and semantic indexing across notes, sources, and audits.
  - `obsidian-local-rest-api` (v5.4.0, coddingtonbear/obsidian-local-rest-api) — secure local REST API for programmatic agent access.

## 2026-10-08T05:08:00+02:00 — configure templater template directory

- **Actor:** agent (Antigravity), per user request ("can you do it for me?").
- **Action:** created `.obsidian/plugins/templater-obsidian/data.json` setting `templates_folder` to `_system/templates`.

## 2026-10-08T05:47:00+02:00 — kureksistant stability fixes & lineage recorded

- **Actor:** agent (Antigravity), per user instruction ("1. fix the code 2. fix the repo 3. update the vault docs in the end").
- **Lineage context:** Recorded user clarification: `kurekizmo` was made private on GitHub; `kureksistant` was created as the public repository specifically incorporating TypeSafe Jev cognitive memory triage and headless daemon optimizations (~333MB RAM, faster-whisper, 24 tools).
- **Repo (`kureksistant`):**
  - Fast-forwarded local clone `../kurekizmo` from `99a7cec` to `52d009b`.
  - Fixed `kurek_daemon.py:454` `last_tool_output` `UnboundLocalError` on initial turn non-tool response.
  - Fixed `core/dream_cycle.py:66` string/dict/None return handling for `query_deepseek`.
  - Fixed F821 undefined symbols in `actions/file_controller.py` (`re`), `actions/screen_vision.py` (`BASE_DIR`), and `actions/code_helper.py` (`_default_path` → `_resolve_save_path`).
  - Added `google-genai` and `typesafe-sdk` to `requirements.txt`; updated `install_linux.sh` virtualenv setup to install from `requirements.txt`.
  - Expanded CI workflow `.github/workflows/ci.yml` to enforce ruff F82 across `actions/`.
  - Verified tests (daemon smoke test green, ruff syntax/F82 checks clean).
  - Committed as `d863922` and pushed to `origin/main` over SSH (`52d009b..d863922`).
- **Vault:** updated `sessions/2026-10-08-kureksistant-session.md` and `wiki/concepts/kureksistant-overview.md`.

## 2026-10-08T05:54:00+02:00 — re-ingest kureksistant sources at d863922

- **Actor:** agent (Antigravity), per user instruction ("you tackle the last task, the re-ingest").
- **Action:** re-ingested 3 sources for `kureksistant` at commit `d863922`:
  - `sources/raw/docs/src-20261008-ae52ff2-kureksistant-readme.md` (verbatim copy of README) & index `sources/index/src-20261008-ae52ff2-kureksistant-readme.md` (active).
  - `sources/raw/docs/src-20261008-88302c2-kureksistant-agents.md` (verbatim copy of AGENTS.md) & index `sources/index/src-20261008-88302c2-kureksistant-agents.md` (active).
  - `sources/raw/docs/src-20261008-f95e626-kureksistant-sha256sums-v0-1-0.txt` (re-cut release asset checksums) & index `sources/index/src-20261008-f95e626-kureksistant-sha256sums-v0-1-0.md` (active).
- **Superseded:** marked pre-audit stubs `src-20261007-c1c7fe9`, `src-20261007-459dbb7`, and `src-20261007-e1be179` as `status: superseded` with `superseded_by` links.
- **Vault:** updated `sources/README.md`, `wiki/concepts/kureksistant-overview.md` (citations table), and `sessions/2026-10-08-kureksistant-session.md` (action item 9 complete).

## 2026-10-08T06:09:00+02:00 — standing reminder logged for next session

- **Actor:** agent (Antigravity), per user instruction ("note it for next time we do this").
- **Action:** added standing handoff reminder to `sessions/2026-10-08-kureksistant-session.md` regarding human confirmation of provider API key revocations.






## 2026-10-08T22:35:00+02:00 — repo status reconcile: five public repos

- **Actor:** agent (ATLAS, Grok Bot), per user ("Reconcile the vault for those 5 repos now").
- **Inputs:** SWEEP report (22:18) and SHIP report (22:27). Both were re-checked around 22:30 against the public GitHub API, the raw READMEs, both showcase sites and the Vercel `nodaysidle-portfolio` project. No GitHub repo or Vercel project was changed.
- **Added:** `artifacts/vault-operations/repo-status-reconcile-2026-10-08.md`, `_system/templates/catalog/nodaysidle-shareguard.md`.
- **Edited (appended text or inline markers only; nothing deleted):**
  - catalog entries: `whisper-bar`, `cascade-v3`, `nodaysidle-sonora`, `nodaysidle-browser-linux`, `portfolio-site`;
  - `_system/templates/CATALOG.md` (ShareGuard row, showcase note);
  - wiki overviews for cascade-v3, nodaysidle-sonora and nodaysidle-browser-linux (current-status sections, stale markers, `updated`);
  - `_system/reference/github-org-repositories.md` (2026-10-08 update);
  - `wiki/MOC/moc-nodaysidle-knowledge.md`;
  - `README.md` (stale marker under "Related nodaysidle surfaces");
  - `sessions/2026-10-07-vault-operations-session.md`.
- **Conflicts marked:**
  - cascade-v3 and sonora visibility history (SWEEP vs the 2026-10-07 13:55 correction);
  - which repo deploys portfolio-nine (`Portfolio` vs private `nodaysidle-portfolio`);
  - WhisperBar licence (the README says MIT; GitHub detects no licence file);
  - ShareGuard README still on the ZIP (PR #4 pending);
  - ShareGuard's theme-only `v0.1.1` tag;
  - cascade v3.1.0 release body still DMG-only.
- **Stale marked:**
  - showcase-v2 / project-pages (not canonical, per owner);
  - sonora's thin-release-notes contradiction (resolved);
  - commit counts for cascade, sonora and browser-linux;
  - the browser-linux release-body todo (already done).
- Nothing committed in this vault.

## 2026-10-08T22:32:00+02:00 — README PR merges verified (whisper-bar #2, shareguard #4)

- **Actor:** agent (ATLAS, Grok Bot), per user follow-up after SHIP's 22:31 report.
- **Verified (public GitHub API + raw README at each merge commit):**
  - whisper-bar PR #2 was merged 22:30:40 as squash `239f1a7` (now `main`). It adds the DMG link and checksum and fixes the clone URL.
  - nodaysidle-shareguard PR #4 was merged 22:30:33 as squash `eeaaca0` (now `main`). The README now links the `v0.1.0-dmg.20260727` DMG and `.sha256`.
- **Edited (inline markers or appended text only; nothing deleted):**
  - `_system/templates/catalog/whisper-bar.md`, `_system/templates/catalog/nodaysidle-shareguard.md`;
  - `artifacts/vault-operations/repo-status-reconcile-2026-10-08.md` (table cells, work bullets, the ShareGuard install-path contradiction marked resolved, a new update section);
  - `sessions/2026-10-07-vault-operations-session.md` (progress line, action 19 done).
- The MOC and CATALOG don't mention these PRs, so they are unchanged. The 22:35 entry above still says "PR #4 pending"; this entry supersedes that.
- Nothing committed in this vault.

## 2026-10-08T23:41:00+02:00 — downloads showcase recorded; portfolio-nine deploy source resolved

- **Actor:** agent (ATLAS, Grok Bot), per user.
- **Verified:**
  - GitHub API: `nodaysidle-apps` is public; PR #1 was merged as `44052bc`; the public repo count is 37.
  - Vercel API: project `nodaysidle-apps`, deployment `dpl_A6j2ZFBRn3yc1r85EXdQHS6By8zV` READY from `main` @ `44052bc`. portfolio-nine deployment `dpl_D3YGzcmFeTnmF9VHpuTaPrUJUFSo` was built from `Portfolio` `master` @ `a225402` with `source: cli`.
  - Live: the site returns 200 and 11/11 download links return 302.
  - Not verified here: that portfolio deployments up to 2026-09-18 came from the private `nodaysidle-portfolio` repo (per user).
- **Added:** `_system/templates/catalog/nodaysidle-apps.md`.
- **Edited (inline markers or appended text only; nothing deleted):**
  - catalog: `portfolio-site` (deploy-source conflict resolved, new section), `whisper-bar`, `cascade-v3`, `nodaysidle-sonora`, `nodaysidle-browser-linux`, `nodaysidle-shareguard`;
  - `_system/templates/CATALOG.md` (nodaysidle-apps row, note);
  - `wiki/MOC/moc-nodaysidle-knowledge.md` (Showcases section);
  - `artifacts/vault-operations/repo-status-reconcile-2026-10-08.md` (deploy-source contradiction resolved, new update section);
  - `_system/reference/github-org-repositories.md` (append);
  - `README.md` (downloads-showcase note);
  - `sessions/2026-10-07-vault-operations-session.md`.
- **Not duplicated:** SHIP's 22:47–22:58 fixes were already in the reconcile artifact. The catalog pages only got short markers that point to them.
- **Open:** browser-linux licence (owner); cascade-v3/sonora visibility history.
- Nothing under `projects/`. Nothing committed in this vault.
## 2026-10-09T09:56:00+02:00 — catalog nodaysrammar

- **Actor:** agent (Antigravity)
- **Action:** add catalog entry and concept overview for nodaysrammar (on-device grammar checker)
- **Paths:** `_system/templates/catalog/nodaysrammar.md`, `wiki/concepts/nodaysrammar-overview.md`, `_system/templates/CATALOG.md`, `wiki/MOC/moc-nodaysidle-knowledge.md`
- **Notes:** Local Chromium MV3 extension with 35k-word offline dictionaries (EN, IT, SL), ONNX neural token classifier, isolated Shadow DOM overlay, and auto-flip popover. Zero telemetry, local-first.

## 2026-10-09T10:32:00+02:00 — nodaysrammar repo check vs vault

- **Actor:** agent (ATLAS, Grok Bot), per user.
- **Checked:** the cursor-github connector (metadata, README, manifest.json, models/README.md, releases, tree, commits), raw source files, and the public repo count. The repo was not changed.
- **Prior vault state:** Antigravity's 09:56 notes (catalog, overview, CATALOG row, MOC) had no version, licence, release or permissions. The org reference didn't list the repo.
- **Added:** `artifacts/nodaysrammar/repo-check-2026-10-09.md`.
- **Edited (inline markers or appended text only; nothing deleted):**
  - `_system/templates/catalog/nodaysrammar.md`, `wiki/concepts/nodaysrammar-overview.md` (status, contradictions, `verified` field);
  - `_system/templates/CATALOG.md` (GitHub link added to the row);
  - `wiki/MOC/moc-nodaysidle-knowledge.md`;
  - `_system/reference/github-org-repositories.md` (38 public);
  - `sessions/2026-10-07-vault-operations-session.md`.
- **Conflicts marked:**
  - ONNX Runtime Web is bundled but unused (plain-JS forward pass);
  - the "neural" models are generated, not trained, and "production-ready" is unverified;
  - the v1.0.0 release has no assets and no checksums;
  - USERGUIDE hardcodes a local path;
  - the English rule lists differ.
- Nothing under `projects/`. Nothing committed in this vault.

## 2026-10-09T10:34:00+02:00 — nodaysrammar correction + status needs-work

- **Actor:** agent (ATLAS, Grok Bot), per user (correction from SHIP and Execution Operator).
- **Verified:** the "could of" rule exists at `background/inference-engine.js:252` (`/\b(could|should|would)\s+of\b/gi`) at `main` @ `4f41689`. The 10:32 entry's claim that it was missing is wrong; the literal-text search missed the regex.
- **Edited (marked, nothing deleted):** `artifacts/nodaysrammar/repo-check-2026-10-09.md` (English-rule row corrected, plus a correction section); `wiki/concepts/nodaysrammar-overview.md` (contradiction #3 corrected; `status: completed` → `needs-work` with `status_note`); `_system/templates/catalog/nodaysrammar.md` (`status` → `needs-work` with `status_note`, plus a status line).
- **Reason for needs-work:** the v1.0.0 release has no assets, the ONNX Runtime Web claim is false (the runtime is bundled but unused), and USERGUIDE contains the owner's private path `/home/arch/dev/nodaysidle/chrome-extension`. It stays needs-work until those release fixes land.
- Nothing under `projects/`. Nothing committed.

## 2026-10-09T10:35:00+02:00 — nodaysrammar CATALOG row → needs-work

- **Actor:** agent (ATLAS, Grok Bot), per user. This follows the 10:34 status change.
- **Edited:** `_system/templates/CATALOG.md`: the nodaysrammar row now says `needs-work` (was `completed`), matching the catalog page and overview.
- **MOC:** the nodaysrammar section of `wiki/MOC/moc-nodaysidle-knowledge.md` was checked; no 'production-ready' or 'completed' wording, so no change.
- Nothing committed; nothing under `projects/`.

## 2026-10-09T11:56:00+02:00 — nodaysrammar v1.0.1 released; status active; showcase card 05

- **Actor:** agent (ATLAS, Grok Bot), per user. Facts come from Execution Operator.
- **Verified:**
  - GitHub API: PR #1 `ce2cbd7` (10:55) and PR #2 `81082cf` (11:09); v1.0.1 is Latest.
  - The zip is 740,320 bytes and its SHA-256 `31d86ad8…6e6d` matches after re-download. The zip manifest is v1.0.1 with `storage` only.
  - No ONNX/`lib` files and no `/home/arch` path remain. The topics and homepage match.
  - nodaysidle-apps PR #2 `aab4c1d`; the live site says "Five tools." and 12/12 links return 302.
  - The REEL clip title card reads v1.0.1.
- **Found already recorded:** at 10:57–10:58 another agent (no audit entry) set `status: active` and added a v1.0.1 section plus contradiction resolutions to `_system/templates/catalog/nodaysrammar.md` and `wiki/concepts/nodaysrammar-overview.md`. That was not duplicated.
- **Edited (marked; nothing deleted):**
  - those two files: `release_status: released`, plus a short dated update (PR #2, homepage, topics, card 05);
  - `_system/templates/CATALOG.md` (row → active / released);
  - `_system/templates/catalog/nodaysidle-apps.md` (5 apps);
  - `artifacts/nodaysrammar/repo-check-2026-10-09.md` (resolutions with commits plus a dated update);
  - `wiki/MOC/moc-nodaysidle-knowledge.md`;
  - `sessions/2026-10-07-vault-operations-session.md` (progress, actions 24–28, process note).
- **Not verified at runtime:** the blocklist behaviour and the regression tests (code and tests exist; not run here).
- Nothing under `projects/`. Nothing committed.

## 2026-10-09T17:40:00+02:00 — X promo strategy from 12 Oct (REACH)

- **Actor:** agent (REACH, Grok Bot), per user via Execution Operator; vault write under the owner's standing rule.
- **Added:** `wiki/concepts/x-promo-strategy-2026-10-12.md` (cadence, Ljubljana times with CEST→CET and US DST offsets, content mix, rotation, reply habit, calendar 12–30 Oct, verbatim week-1 drafts, claim ledger).
- **Edited (insertions only):** `wiki/MOC/moc-x-promo.md` (link), `wiki/concepts/x-promo-calendar-2026-10.md` (dated pointer above the calendar table; rows kept), `wiki/concepts/x-promo-strategy.md` (Related link), `sessions/2026-10-07-vault-operations-session.md` (progress line).
- **Verified:** READMEs/releases via GitHub API and raw files; showcase and portfolio live; all draft links HTTP 200. Org now has 38 public repos (was 36).
- Drafts only; nothing posted or scheduled. Nothing committed.

## 2026-10-09T17:35:00+02:00 — correction: Kurek recap claim

- **Actor:** agent (REACH), per Execution Operator.
- **Change:** in `wiki/concepts/x-promo-strategy-2026-10-12.md`, the Wed 14 Kurek recap draft and the sources line no longer say the prompt handler and installer deps are fixed; both are still open and deferred. They now list what was actually done: clean v0.1.0 re-cut, legacy GUI moved, CI added, README at ~333MB / 24 tools. The Thu 29 Kurek line was checked and makes no fix claims.

## 2026-10-10T05:11:00+02:00 — kureksistant 10-10 perf/IPC overhaul cross-checked

- **Actor:** agent (ATLAS, Grok Bot), per user.
- **Prior commit:** owner vault commit `8e80480` (05:04) added `wiki/concepts/kureksistant-overview.md` with a 2026-10-10 block. That block had no audit entry or session note; this entry records it after the fact.
- **Checked:** kureksistant `main` @ `02382f2` via the cursor-github connector and raw files, the check-runs API, plus read-only machine state (systemd unit, sockets, `bindings.lua`). No latency was measured, and the repo was not changed.
- **Added:** `artifacts/kureksistant/perf-ipc-check-2026-10-10.md`.
- **Edited (marked; nothing deleted):**
  - `wiki/concepts/kureksistant-overview.md` (inline verdicts, a `verified` field, a status section);
  - `_system/templates/catalog/kurekizmo.md`;
  - `wiki/MOC/moc-nodaysidle-knowledge.md`;
  - `sessions/2026-10-08-kureksistant-session.md`.
- **Findings:**
  - UDS, the C trigger, streaming, mpv, the watcher and systemd are verified in code.
  - The <2ms / sub-400ms / 60ms figures are unbacked.
  - The 24-tools figure is stale (27 modules).
  - `MemoryHigh=250M` conflicts with ~333MB (the live daemon swaps).
  - The topic is misspelled.
  - The v0.1.0 notes are stale.
  - 10 of the overview's 12 wikilinks are untracked, so they are broken on GitHub.
- Nothing under `projects/`. **Not committed or pushed:** the owner commits the vault himself.

## 2026-10-10T05:40:00+02:00 — kureksistant PR #4 fixes verified

- **Actor:** agent (ATLAS, Grok Bot), per user.
- **Verified:** [PR #4](https://github.com/nodaysidle/kureksistant/pull/4) `c83f46f` merged at 05:38:17 CEST with CI green; the diff plus a test covers items 1–4 and 8. Machine checked read-only: local repo `c83f46f`; unit 400M/600M; service active; 345 MiB; UDS subscribe OK. The trigger was not toggled.
- **Edited (marked; nothing deleted):** `wiki/concepts/kureksistant-overview.md`, `artifacts/kureksistant/perf-ipc-check-2026-10-10.md`, `_system/templates/catalog/kurekizmo.md`, `sessions/2026-10-08-kureksistant-session.md`.
- **Resolved:** MemoryHigh/swap conflict; UDS state events.
- **Still open:** PR B (not approved), PR C (optional), v0.2.0.
- Nothing under `projects/`. Not committed or pushed.

## 2026-10-10T05:51:00+02:00 — kureksistant PR #5 fixes verified

- **Actor:** agent (ATLAS, Grok Bot), per user.
- **Verified:** [PR #5](https://github.com/nodaysidle/kureksistant/pull/5) `e1d3575` merged at 05:49:30 CEST with CI green; the diff covers findings 5, 6, 9 and 10 plus 450M/600M. Machine checked read-only: repo `e1d3575`; unit templated, 450M/600M; service active; 280 MiB current / 452 MiB peak (EO's ~373MiB was not reproduced); socket 0600; subscribe OK; `install_path` present. `api_keys.json` existence and mtime only; contents not read.
- **Edited (marked; nothing deleted):** `wiki/concepts/kureksistant-overview.md`, `artifacts/kureksistant/perf-ipc-check-2026-10-10.md`, `_system/templates/catalog/kurekizmo.md`, `sessions/2026-10-08-kureksistant-session.md`.
- **Closed:** the PR B items.
- **Still open:** PR C and v0.2.0, neither approved.
- Nothing under `projects/`. Not committed or pushed.

## 2026-10-10T06:11:00+02:00 — kureksistant v0.2.0 released, verified

- **Actor:** agent (ATLAS, Grok Bot), per user.
- **Verified:** [PR #6](https://github.com/nodaysidle/kureksistant/pull/6) `f1d7920` and [PR #7](https://github.com/nodaysidle/kureksistant/pull/7) `e91a14c` merged with CI green; [v0.2.0](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.0) is Latest, with tarball 942,506 bytes, SHA-256 `6b856030…19da` (full hash in the artifact) and release notes checked; topic `ai-assistant`. Machine checked read-only: repo `e91a14c`, unit 512M/600M, active (restarted 06:10:39), 313 MiB / 396 MiB peak, socket 0600, subscribe OK. `api_keys.json` not read.
- **Correction:** my earlier "24 tools stale" flag was wrong (24 actions are loaded).
- **Edited (marked; nothing deleted):** `wiki/concepts/kureksistant-overview.md`, `artifacts/kureksistant/perf-ipc-check-2026-10-10.md`, `_system/templates/catalog/kurekizmo.md`, `sessions/2026-10-08-kureksistant-session.md`. The CATALOG row lists no version, so it is unchanged.
- **Still open:** ⚠️ unauthenticated HTTP API; ⚠️ desktop.py exec(); unmeasured end-to-end latency.
- Nothing under `projects/`. Not committed or pushed.

## 2026-10-10T06:35:00+02:00 — X plan: Kurek v0.2.0 slot

- **Actor:** agent (REACH), per owner approval via Execution Operator.
- **Change:** appended an update to `wiki/concepts/x-promo-strategy-2026-10-12.md`: Kurek v0.2.0 launch on Wed 21 Oct at 15:15, and the poll-winner thread moved to Thu 29 Oct (replacing the old Kurek slot). Includes the draft, the allowed claims and the media paths.

## 2026-10-10T07:35:00+02:00 — Kurek on showcase (card 06), real demo GIF, launch date

- **Actor:** agent (ATLAS, Grok Bot), per user.
- **Verified:** [nodaysidle-apps PR #3](https://github.com/nodaysidle/nodaysidle-apps/pull/3) `46251cb` merged at 07:32:00 CEST (Vercel success); the live site shows Six tools / 06 / 06 / `#kurek`, and 14/14 links return 302. The live clip has an audio track. The JARVIS CC BY-NC 4.0 credit is on the card. [kureksistant PR #8](https://github.com/nodaysidle/kureksistant/pull/8) `022d4be` merged at 06:30:45 CEST; the GIF matches REEL's file.
- **Conflict:** EO's launch date (Wed 21 Oct 15:15) is not in REACH's plan file (that slot is the Browser build thread). Recorded as EO-reported.
- **Edited (marked; nothing deleted):** `_system/templates/catalog/nodaysidle-apps.md`, `_system/templates/catalog/kurekizmo.md`, `wiki/concepts/kureksistant-overview.md`, `wiki/MOC/moc-nodaysidle-knowledge.md`, `_system/templates/CATALOG.md`, `sessions/2026-10-08-kureksistant-session.md`.
- Nothing under `projects/`; `sources/raw/` untouched. Not committed or pushed.

## 2026-10-10T08:00:00+02:00 — X plan: Kurek v0.2.0 applied inline, six apps

- **Actor:** agent (REACH), per Execution Operator / ATLAS.
- **Change:** `wiki/concepts/x-promo-strategy-2026-10-12.md` calendar rows changed: Wed 21 is now the Kurek v0.2.0 launch, Thu 29 the poll-winner thread. The Wed 14 recap uses v0.2.0 facts (24 tools, ~450MB peak, ~0.8ms, no fix claims). The roundup counts six apps. The Kurek first reply links https://nodaysidle-apps.vercel.app/#kurek. The box copy `/workspace/reach/x-promo-strategy-2026-10-12.md` was synced from the vault.

- 2026-10-10 16:28 (ATLAS): kureksistant-overview: recorded owner commit 5477ef5 (vault_knowledge, tool #25) after the fact; tool count 24→25 (6137128); ~150-token claim marked unmeasured; duplicate YAML key `verified_previous_pr5` renamed; stale REACH launch conflict resolved; PR #9 9f82d28 recorded. Uncommitted.

## 2026-10-10T18:25:00+02:00 — Voice Anywhere: Superwhisper tactile interaction & auto-typing overlay

- **Actor:** agent (Antigravity), per user request.
- **Project:** `com.nodaysidle.voiceanywhere.debug` (`/home/arch/Projects/_github-migrations/nodaysidle-voice-anywhere-v2`).
- **Verified:** Tested and verified on physical hardware (Xiaomi Mi 10T Pro / Android 12, device `a2f3cdaa`):
  - **Badge UI**: Custom Canvas `SuperwhisperDeltaIcon` (black rounded triangle badge, white outline, matching inner Delta glyph `▲`, 0-padding idle capsule).
  - **Interaction**: Hold-to-Talk (press to record, release to paste), double-tap for history drawer, edge snap.
  - **Auto-Hide / Typing Detection**: Fast 200ms debounce on leaving text fields; auto-hides on launcher/home; auto-pops on text focus (`findFocus`, `FOCUS_INPUT`, `rootInActiveWindow`).
  - **Audio & STT Resiliency**: Solved Android `MediaRecorder` stop error `-1007` with frame encoding buffer guarantee; filtered sub-300ms false error triggers.
- **Created / Edited:**
## 2026-10-10T21:05:00+02:00 — Decision Intelligence: Microsoft-Decision-1 vs TypeSafe Jev integration

- **Actor:** agent (Antigravity), per user request.
- **Scope & Comparative Benchmark:**
  - Evaluated the newly announced **Microsoft-Decision-1** (Qwen3.5-9B post-trained for single-pass decision scoring; 85ms P50 latency, 83.5% accuracy, 92.2 calibration score, $0.042/1M input tokens) against **TypeSafe Jev** (jev-1.13.0 System One; 240ms P50, 82.3% accuracy, 93.7 calibration score #1).
  - Adopted workspace-wide hybrid architecture: Microsoft-Decision-1 for sub-100ms hot loops and web apps; TypeSafe Jev retained for critical security risk matrices (`jev-review`), spec gating (`cascade-v3`), and persistent memory boundary hoisting.
- **Implemented & Verified:**
  1. **Kureksistant (`/home/arch/dev/nodaysidle/kurekizmo`):**
     - Updated `kurek_daemon.py`: `_check_auto_screen_context` now calls Microsoft-Decision-1 via OpenRouter `/api/alpha/decisions` using `OPENROUTER_API_KEY`.
     - Live verified in daemon venv: triggers active window capture in ~85ms (down from 240ms), saving ~155ms on middle-click hardware voice triggers.
     - TypeSafe Jev preserved for Muse memory triage and alignment boundary hoisting.
  2. **Prompt Optimizer (`/home/arch/dev/nodaysidle/nodaysidle-prompt-optimizer`):**
     - Updated `src/lib/jev.ts` to call OpenRouter decisions API as primary engine across all 8 diagnostic questions and quality gate, with TypeSafe fallback.
     - Added OpenRouter key setting card in UI (`settings-panel.tsx`) and header routing in `/api/diagnose` & `/api/optimize`.
     - Committed (`818eed1`), pushed to GitHub, and redeployed to production on Vercel: `https://nodaysidle-prompt-optimizer.vercel.app`.
     - Live verified production response with `x-openrouter-key`.
- **Created / Edited in Vault:**
  - Created [[wiki/concepts/decision-models-microsoft-vs-jev]].
  - Updated [[wiki/concepts/nodaysidle-prompt-optimizer-overview]].
  - Updated [[wiki/concepts/kureksistant-overview]].
  - Updated [[_system/templates/catalog/nodaysidle-prompt-optimizer]].
  - Updated [[wiki/MOC/moc-nodaysidle-knowledge]].


- 2026-10-11 19:07 (ATLAS): SWEEP Oct 11 18:13 weekly catalog sweep recorded in [[artifacts/vault-operations/sweep-2026-10-11-sunday-catalog]]. OPEN: (1) nodaysidle-browser (macOS) v2026.7.23 has 0 assets, install covers source builds only, not shippable; (2) browser-linux install links the releases index, not the AppImage; (3) nodaysidle-browser and synapse-notes have no demo GIF; (4) nodaysrammar, kureksistant, ShareGuard and browser-linux missing from the portfolio (nodaysidle-portfolio-nine), whose Browser card points at a release with no downloads. CLEARED: whisper-bar and shareguard README install links; sonora release notes. Uncommitted.

- 2026-10-11 19:38 (ATLAS): nodaysidle/Portfolio PR #1 squash-merged as 9b9a0d8 (Oct 11 19:32, per Execution Operator, user-approved), deploying to nodaysidle-portfolio-nine.vercel.app. Added 4 cards, portfolio now 9 projects: nodaysrammar v1.0.1 (MIT), Kurek v0.2.0 (CC BY-NC 4.0), ShareGuard v0.1.2 (proprietary, no apps-site card), Browser for Linux v0.1.0 (no licence claim). macOS Browser card unchanged, renumbered 05/09 (its release still has no assets). Closes SWEEP Oct 11 gap 4 except the Browser-card download issue.

## 2026-10-11T20:10:00+02:00 — weekly wiki reconcile (ATLAS)

- **Actor:** agent (ATLAS / Grok Bot executor), Sunday weekly-wiki-reconcile routine.
- **Verified live:** GitHub `public_repos=38`; latest releases for cascade-v3, whisper-bar, sonora, synapse-notes, nodaysidle-browser, nodaysidle-browser-linux, shareguard, nodaysrammar, kureksistant; portfolio-nine (9 cards); nodaysidle-apps (6 tools); Vercel projects nodaysidle-portfolio / nodaysidle-apps active, showcase-v2 / project-pages stale.
- **ask-gemini:** comparison/summary used on the box (`ask-gemini` ← live-vs-vault facts).
- **Created:** [[artifacts/vault-operations/repo-status-reconcile-2026-10-11]].
- **Edited (append / ⚠️ superseded markers; nothing deleted):** `_system/reference/github-org-repositories.md`, `artifacts/vault-operations/sweep-2026-10-11-sunday-catalog.md`, catalogs (shareguard, browser-linux, nodaysrammar, kurekizmo, nodaysidle-browser, synapse-notes, whisper-bar, sonora, cascade-v3, portfolio-site, nodaysidle-apps), wiki (browser-linux-overview, nodaysrammar-overview, synapse-notes-overview, kureksistant-overview), `_system/templates/CATALOG.md`, `wiki/MOC/moc-nodaysidle-knowledge.md`, `sessions/2026-10-07-vault-operations-session.md`.
- **Material:** portfolio-missing SWEEP gaps closed in vault (live already had Portfolio PR #1); org list synced; open release/media/licence gaps documented.
- Nothing under `projects/`. Not committed or pushed.

- 2026-10-12 03:32 (ATLAS): Owner decisions 2026-10-12 (via Execution Operator): (1) macOS NODAYSIDLE Browser card to be hidden from the portfolio (no Macs available); (2) nodaysrammar stays off the Chrome Web Store for now (cost, no ROI; sideload only); (3) Kurek security fixes (unauthenticated HTTP :8790, exec() in actions/desktop.py) parked while the owner tests; he is prototyping phone-based remote control of Kurek. ⚠️ Risk: remote control would expose the unauthenticated control API and model-generated exec() beyond localhost; fix auth before exposing it.

- 2026-10-12 03:35 (ATLAS): REEL demo clip status (box /workspace/clips/<app>/, not committed to repos): synapse-notes (real screenshots, personal notes blurred, no voice-capture footage) and browser-linux v0.1.0 (real AppImage footage) now have GIF+MP4, closing their no-demo-GIF gap once committed to the repos. Also ready: whisperbar, shareguard, cliprail (icon+text), cascade (real footage), sonora (real footage, explicit title blurred), nodaysrammar v1.0.1 (real Chromium), kurek v0.2.0 (icon+text). macOS nodaysidle-browser skipped (card being hidden). Note: REEL says kurek README demo.gif is a mock-up, but kureksistant PR #8 022d4be already replaced it with REEL's real v0.2.0 GIF; REEL's note is stale on that point.

- 2026-10-12 03:50 (ATLAS): kureksistant PR #10 squash 395d7bf (2026-10-12 03:49, per Execution Operator): optional Microsoft-Decision-1 auto-screen decision via OpenRouter with TypeSafe fallback, 1.5s timeout, KUREK_AUTO_SCREEN=0 opt-out, validated null. ⚠️ Privacy risk: prompt text is sent to OpenRouter when the key is set. No latency claims. | browser-linux PR #2 merged as 31ede82: README install now links the AppImage directly (closes reconcile 2026-10-11 conflict 5). | Portfolio PR #2 merged as 4a542d0: macOS NODAYSIDLE Browser card hidden per owner decision 2026-10-12; portfolio now 8 projects (closes reconcile 2026-10-11 conflict 3 for the portfolio).

## 2026-10-12T03:55:00+02:00 — X plan update (portfolio 8 apps, Kurek opt-out note)

- **Actor:** agent (REACH), per Execution Operator. Appended an update section to `wiki/concepts/x-promo-strategy-2026-10-12.md`. No schedule changes. Confirmed today's first post at 15:15.

- 2026-10-12 05:12 (ATLAS): 🏁 Milestone 2026-10-12 ~05:00 (per Execution Operator): the owner has a working Kurek.apk on Android that controls Kurek on the PC by voice, remotely over Tailscale, tested on mobile data. ⚠️ OPEN RISK (security): the :8790 control API has no authentication and actions/desktop.py exec()s model-generated code; remote access widens exposure to every device on the tailnet. SHIP is reviewing the repo and security; treat it as open until SHIP reports.

- 2026-10-12 05:31 (ATLAS): ✅ CLOSED: Kurek remote OPEN RISK (from the 2026-10-12 ~05:00 milestone), per Execution Operator, user-approved. kureksistant PR #11 squash 822966c (05:31): loopback bind by default (KUREK_REMOTE_BIND=tailscale opt-in); required Bearer token with compare_digest for remote requests; CSRF/Origin blocks, no CORS *; 64KB body cap; remote exec tools gated by KUREK_REMOTE_ALLOW_EXEC; hardcoded token and IP removed from the Android app, release/kurek-remote.apk deleted; SECURITY.md added. Leaked token rotated by the owner (old one returns 401); still in git history but inert. No published APK release. Remaining (local only): actions/desktop.py still exec()s model-generated code for local use; the localhost API is unauthenticated by design when loopback-bound. Not re-verified by ATLAS (cheap mode).

- 2026-10-12 05:48 (ATLAS): Kurek repositioned as PC voice control incl. remote Android over Tailscale (verified 2026-10-12, PR #11 822966c; APK unpublished). Updated overview Summary, kurekizmo catalog, and X plan note for REACH.

- 2026-10-13 09:35 (ATLAS): 🧪 Pilot started: two-reviewer merge gate on kureksistant (user-approved via Grok Bot). Script /home/box/tools/merge-gate/merge-gate.sh (on the box) — Codex + agy each review the PR diff and must both say VERDICT: MERGE on the same head SHA. Advisory only, no auto-merge; the owner still reviews and merges. Read-only dry run on merged PR #12 (88512f8): PASS. Repo unchanged; APK↔PC Tailscale untouched. Idle watchdog (watchdog.sh) uses file-change times as a stand-in and is not scheduled yet.

- 2026-10-14 00:28 (EO, logged by ATLAS 2026-10-14 00:47): ✅ kureksistant v0.2.1 deployed. PR #13 squash `3761c78` (merge gate: agy MERGE / Codex BLOCK on the 'Confirmed and executed' wording; merged on owner approval). PC main reset to kureksistant/main; old local `f0a7cdf` kept on branch `backup/pre-v0.2.1`; backups in `~/kurek-backups/pre-v0.2.1-20261014-002747`. Service active, listening only on 127.0.0.1 and the Tailscale IP (:8790). Tailscale SSE 200; wrong/missing token 401. JSON→SQLite memory migration OK (12 entries, 1 session). PC tests 146 pass / 1 skip. ⚠️ Watch: service memory ~500M vs MemoryHigh 512M.
- 2026-10-14 00:46: GitHub release [Kureksistant v0.2.1](https://github.com/nodaysidle/kureksistant/releases/tag/v0.2.1) published, target `3761c78`, Latest. Owner phone test passed: online and responding over Tailscale, migrated memory works (knows him and his projects), middle-click works.

## 2026-10-14T01:33:59+02:00: Prompt Optimizer audit fixes, production deployments and owner-requested handoff

- **Actor:** OpenCode, per the owner's request to record this conversation's changes in Obsidian for future reference. [vault]
- **Implementation:** audit baseline `818eed1`; initial fixes `7739f68`; reviewed credential/privacy/preset revision `e6465f3`; supplied silver N logo `03aac47`. Desktop-first preservation modes, actionable type-aware diagnostics, frozen diff and cancellation, bounded/validated provider requests, private shared-key access, safe explicit legacy-key migration, paired text evaluation, versioned profiles, accessible dialogs and CI/test infrastructure. [vault]
- **Deployments:** reviewed app `dpl_CDw45Y8wxxR9JcgjjaL2LDFjt8JT`; final logo `dpl_EP2DWUpWzXnN3AifwtkjVKtCkdNW`, both READY and aliased to https://nodaysidle-prompt-optimizer.vercel.app/. Live UI/API/loaded-logo checks passed. [vault]
- **Verification:** reviewer reran lint/typecheck/build, 90 unit/ReactDOM tests, 5 mocked browser tests and production audit (zero advisories). No paid AI calls or downstream generation benchmark. Five development-only ESLint-chain advisories remain; no GitHub CI run claimed. [vault]
- **Continuity:** source is in `/home/arch/.local/share/opencode/worktree/6f72e1/optimizer-audit-fixes`, retained by local `audit/nodaysidle-logo`. Original `master` remains `818eed1`; no merge/push/release tag. No Vercel environment changes or secret values recorded. [vault]
- **Created:** [[artifacts/prompt-optimizer/audit-fixes-and-deploy-2026-10-14]], [[sessions/2026-10-14-prompt-optimizer-session]]. [vault]
- **Updated:** [[wiki/concepts/nodaysidle-prompt-optimizer-overview]] (current snapshot plus retained superseded history), [[wiki/concepts/decision-models-microsoft-vs-jev]] (optimizer-only correction; historical metrics retained), [[_system/templates/catalog/nodaysidle-prompt-optimizer]], [[wiki/MOC/moc-nodaysidle-knowledge]], [[sessions/LATEST]] (linked handoff only), vault-operations umbrella and active kureksistant session (cross-link; primary thread unchanged). [vault]
- No `projects/` promotion, raw-source deletion, unrelated Obsidian/theme modification, vault commit or push. Documentation left for owner review. [vault]

- 2026-10-14 15:41 (ATLAS, per EO): kureksistant merge-gate follow-ons. (1) Owner-agent self-check `scripts/verify.sh` (draft PR #16): test suite, isolated daemon boot on a spare loopback port, token check 401/401/400, temp-DB memory migration check; `merge-gate.sh` refuses to run unless verify passed on the same commit. VERIFY PASS at `6f5c0d3`; gate FAIL (Codex BLOCK: verify is not a security sandbox; agy MERGE). (2) GitHub Issues as live status: `status:*` / `owner:*` labels, issues #17–#21; `/home/box/tools/kurek-status/morning.sh` drafts a morning summary (not scheduled; proposed 08:30 weekdays). v0.2.1 release now has downloads (tarball, SHA256SUMS, debug APK). Owner decisions pending: sandbox vs trusted-only; 2 skipped tests; morning schedule; gate --comment; watchdog schedule.
