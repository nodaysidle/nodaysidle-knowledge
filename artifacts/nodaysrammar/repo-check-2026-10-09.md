---
type: artifact
artifact_kind: audit
topic_slug: nodaysrammar
generated: 2026-10-09
generator_agent: auditor
repo_ref: main @ 4f41689
verified_at: 2026-10-09T10:32:00+02:00
tags:
  - artifact
  - audit
  - nodaysrammar
---

# Audit: nodaysrammar vault notes vs GitHub repo (2026-10-09)

Read-only check by Grok Bot (ATLAS), run 2026-10-09 10:32 (UTC+2), per user. It compares the vault notes written by Antigravity at 09:56 ([[_system/templates/catalog/nodaysrammar]], [[wiki/concepts/nodaysrammar-overview]]) with [nodaysidle/nodaysrammar](https://github.com/nodaysidle/nodaysrammar) at `main` @ `4f41689`. Sources: the cursor-github connector (repo metadata, README, manifest.json, models/README.md, releases, file tree, commits) and raw source files. The repo was not changed. Labels: **observed** means seen in the repo or API; **inferred** means deduced from it.

## Repo facts (verified)

| Field | Value |
|---|---|
| Visibility | public (created 2026-10-09 10:02) |
| Default branch / HEAD | `main` / `4f41689` "fix: correct screenshot asset paths in README and codemap" (10:22). 2 commits; the first is `c059c6c` "initial release of nodaysrammar v1.0.0" (10:08). |
| Description | "On-device, zero-telemetry multilingual grammar and spell checker for Chromium (Manifest V3)" |
| Topics | chrome-extension, grammar-checker, local-first, manifest-v3, onnx, privacy, spell-checker, webassembly |
| Homepage | none |
| Licence | MIT (`LICENSE`; the GitHub API detects MIT; `package.json` `license: MIT`; README badge MIT) |
| Version | 1.0.0 (`manifest.json` and `package.json`) |
| Manifest name | "nodaysrammar - On-Device Multilingual Grammar Checker" (action title `nodaysrammar`) |
| Permissions | `storage`, `activeTab`, `scripting`; `host_permissions: <all_urls>`; content script on `<all_urls>` (`all_frames: false`, `document_idle`); `web_accessible_resources` `models/*`, `assets/*`, `lib/*` exposed to `<all_urls>`; options page in a tab; popup |
| Release | [v1.0.0](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.0) "nodaysrammar v1.0.0", published 2026-10-09 10:08, Latest, **0 assets** |
| Install | clone, then `chrome://extensions` → Developer mode → Load unpacked. No Chrome Web Store listing is mentioned anywhere. |
| Browsers (repo docs) | README: Chrome, Brave, Edge, Arc, Chromium. USERGUIDE: Chrome, Edge, Brave, Arc, Vivaldi. |
| Tests | `tests/test-live.js` (Puppeteer, `npm test`) and `tests/test-autofix.js` (`npm run test:autofix`). Not run in this check. |
| Local clone | `../chrome-extension` (origin = nodaysidle/nodaysrammar, HEAD `4f41689`) |

## Contradictions

| Topic | Vault | Repo | Resolution |
|-------|-------|------|------------|
| ONNX Runtime Web / WASM inference | Catalog stack and architecture "WebAssembly ONNX inference"; overview "Local ONNX Models … loaded … via `ModelLoader`" | `lib/ort.bundle.min.mjs` (468 KB) is bundled, but no background, content, options, popup or onboarding script imports it (no `ort.bundle`, `InferenceSession` or `importScripts`). `NeuralModelSession` (`background/model-loader.js`) runs the forward pass in plain JS with weights from `models/vocab-*.json`. The `.onnx` file is fetched and only its byte length is kept (observed). The README makes the same claim as the vault. | ✅ **Resolved 2026-10-09 10:55 by [PR #1](https://github.com/nodaysidle/nodaysrammar/pull/1) `ce2cbd7`:** ONNX/WASM was removed (no `.onnx` files and no `lib/ort.bundle.min.mjs`), and the README describes the engine honestly. ~~**Open, owner.**~~ The vault claim is marked ⚠️. ONNX Runtime Web is shipped but appears unused (inferred from the scripts checked). |
| "Neural models" / "production-ready" | Overview: "production-ready", "ONNX neural token classifier"; catalog: "ONNX neural models" | `scripts/generate_real_models.py` draws random weights (`np.random.seed(42)`), then sets each known token's embedding by pseudo-inverse so it outputs a preset label (OK / SPELL / GRAMMAR / PREP / PUNCT). There is no training data or training loop, and unknown words map to `<unk>` (observed). The model is a fixed lookup table in neural-network form (inferred). README: "trained with opset 17"; models/README: "production-grade". | ✅ **Resolved 2026-10-09 10:55 (`ce2cbd7`):** the ONNX models and "neural" claims are gone from the README; the engine is documented as dictionaries plus rules. (`scripts/generate_real_models.py` and `models/vocab-*.json` remain in the repo.) ~~**Open, owner.**~~ The vault claims are marked ⚠️ unverified. Detection quality comes from the dictionaries, rules and the fixed label table, not from learned weights. |
| Release download / checksums | Vault: no release record | v1.0.0 has no assets (no `.zip`/`.crx`). The release body's "Included Assets & Checksums" table lists repo files with sizes but no checksums, while the README calls `docs/RELEASE-NOTES-v1.0.0.md` "Release notes and checksums" (observed) | ✅ **Resolved 2026-10-09 10:55:** [v1.0.1](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.1) (Latest, tag at `ce2cbd7`) ships `NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip` (740,320 bytes, SHA-256 `31d86ad88491798dbc7a891793cf4824681244e734ab4fb4935db9567a5a6e6d`) plus a `.sha256` file, built by `release.yml`, which checks that the manifest and package versions match the tag. v1.0.0 is unchanged (0 assets). ~~**Open.**~~ Recorded. A packaged zip with a SHA-256 would match the other nodaysidle releases. |
| Local install path in public docs | Vault: `local_path: ../chrome-extension` | `USERGUIDE.md` line 75 tells users to load `/home/arch/dev/nodaysidle/chrome-extension`, the owner's local path (observed) | ✅ **Resolved 2026-10-09 10:55 (`ce2cbd7`):** no `/home/arch` path remains in README, USERGUIDE, AGENTS.md or codemap.md. ~~**Open, owner**~~ (docs fix). |
| Naming / index link | CATALOG row links only `[chrome-extension](../chrome-extension)` | The repo is `nodaysrammar`; the local folder is `chrome-extension` (like `kurekizmo` → `kureksistant`) | Marked: the CATALOG row now also links the GitHub repo. ✅ 2026-10-09 10:55 (`ce2cbd7`): the display name is now "NODAYSIDLE nodaysrammar - On-Device Multilingual Grammar Checker". The name has no "g" on purpose. The local folder is still `chrome-extension`. |
| English rule list | Overview/catalog: a/an, linking-verb adjectives, "could of", "he don't" | README: subject-verb agreement, a/an, homophones (there/their/they're, its/it's), double negatives. `inference-engine.js` has linking-verb and homophone rules; ~~"could of" is not in `inference-engine.js` (observed; not searched elsewhere)~~ ✅ **Corrected 2026-10-09 10:34** (SHIP and Execution Operator; re-checked): the rule is implemented at `background/inference-engine.js:252` (`/\b(could|should|would)\s+of\b/gi`) at `main` @ `4f41689`. The earlier search looked for the literal text and missed the regex. | Minor. Both lists are recorded. The vault's "could of" claim is correct. |
| Browsers | Catalog: Chrome, Brave, Edge | README adds Arc and Chromium; USERGUIDE adds Arc and Vivaldi | Minor, no conflict. |

## Not previously in the vault

- Version 1.0.0, MIT licence, `main` branch, public visibility, created 2026-10-09, release v1.0.0 with no assets, topics, no homepage.
- Manifest permissions and the `<all_urls>` reach, including web-accessible `models/*`, `assets/*` and `lib/*`.
- Docs set: README, USERGUIDE, codemap, AGENTS.md (CLAUDE.md = `@AGENTS.md`), `docs/RELEASE-NOTES-v1.0.0.md`, 12 screenshots.
- Not in [[_system/reference/github-org-repositories]] before this check. The public API now returns **38** repos; `nodaysrammar` is the one added since the 2026-10-08 23:41 count of 37.
- No session-note or showcase entry. It is not on portfolio-nine or nodaysidle-apps. ✅ 2026-10-09 11:55: now card 05 on nodaysidle-apps (`aab4c1d`). Still not on portfolio-nine.

## Recommended next research

- Owner: either wire ONNX Runtime Web in or drop it (and the `.onnx`/WASM claims); decide how to describe the models honestly. ✅ Done `ce2cbd7` (dropped).
- Owner: attach a packaged extension zip + SHA-256 to v1.0.0, or remove the "Checksums" wording. ✅ Done: v1.0.1 zip + `.sha256`.
- Owner: replace the hardcoded `/home/arch/...` path in USERGUIDE. ✅ Done `ce2cbd7`.
- Optional: run `npm test` locally and record the result; ingest README, USERGUIDE and AGENTS.md as sources.

## Correction 2026-10-09 10:34 (UTC+2)

- The "could of" rule **is implemented**: `background/inference-engine.js:252` (`/\b(could|should|would)\s+of\b/gi`) at `main` @ `4f41689`. It was confirmed on GitHub at that commit. The English-rule row above is corrected. The two rule lists still differ only in emphasis.
- Status changed to **needs-work** in [[_system/templates/catalog/nodaysrammar]] and [[wiki/concepts/nodaysrammar-overview]]. Reason: the v1.0.0 release has no assets, the ONNX Runtime Web claim is false (the runtime is bundled but unused), and USERGUIDE contains the owner's private path `/home/arch/dev/nodaysidle/chrome-extension`. It stays needs-work until those release fixes land.

## Update 2026-10-09 11:55 (UTC+2): v1.0.1 released, audit items fixed, on the showcase

Verified by Grok Bot (ATLAS) against the GitHub API, the downloaded release zip and the live site. Facts come from Execution Operator; the repo was not changed by this agent.

- **[PR #1](https://github.com/nodaysidle/nodaysrammar/pull/1)** "Release-ready v1.0.1: drop ONNX/WASM, REEL fixes, CI + release zip", merged 10:55 as `ce2cbd7`. It covers audit items 1–12 (per Execution Operator). Checked:
  - ONNX/WASM is gone: no `.onnx` files and no `lib/` in the tree or the zip.
  - Manifest permissions are `storage` only; there are no `host_permissions` and no `web_accessible_resources`. The content script still matches `<all_urls>` (`all_frames: false`).
  - The README has a "Per-site blocklist" and a Privacy section (on-device; settings sync only through Chrome Sync, `chrome.storage.sync`). The content script has blocklist detach logic (`applyBlocklistState`). The blocklist was not tested at runtime.
  - The display name is "NODAYSIDLE nodaysrammar - On-Device Multilingual Grammar Checker".
  - No `/home/arch` path remains in the docs.
  - REEL's bug fixes come with `tests/test-regressions.js` ("Regression tests for REEL-reported bugs"). The tests were not run by this agent.
  - The demo GIF `docs/media/nodaysrammar.gif` (1.8 MB) is shown in the README.
- **[PR #2](https://github.com/nodaysidle/nodaysrammar/pull/2)** "ci: read-only permissions and fail on browser install errors", merged 11:09 as `81082cf` (now `main` HEAD). `ci.yml` sets `permissions: contents: read` and exits 1 when no Chrome/Chromium is available.
- **Release:** [v1.0.1](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.1) is Latest (published 10:55, tag → `ce2cbd7`). It ships `NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip` (740,320 bytes, SHA-256 `31d86ad88491798dbc7a891793cf4824681244e734ab4fb4935db9567a5a6e6d`). I re-downloaded the zip and the SHA-256 matches. There is also a `.sha256` file. The zip manifest says version `1.0.1`. `release.yml` runs on tags and fails on a version mismatch. v1.0.0 is unchanged.
- **Repo settings:** topics are chrome-extension, grammar-checker, local-first, manifest-v3, privacy, spell-checker (`onnx` and `webassembly` were dropped). Homepage: https://nodaysidle-apps.vercel.app. MIT.
- **Showcase:** [nodaysidle-apps PR #2](https://github.com/nodaysidle/nodaysidle-apps/pull/2) was merged 11:52:59 as `aab4c1d`. The live site shows "Five tools." with card 05, "Chrome / Chromium (MV3)". 12/12 download links return 302, including the nodaysrammar zip.
- **REEL demo clip:** on the agent box at `/workspace/clips/nodaysrammar/nodaysrammar.mp4` and `.gif`. The title card reads "v1.0.1 · Chrome MV3 · MIT". Not in this vault.
- **Status:** active and released; the name has no "g" on purpose. Still open:
  - Not on the Chrome Web Store (sideload only).
  - The owner's local clone `../chrome-extension` is at `4f41689` and needs a `git pull`.
