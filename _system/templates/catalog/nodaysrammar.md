---
type: catalog-entry
name: nodaysrammar
status: active
release_status: released
status_note: "Changed needs-work → active on 2026-10-09 10:58: the release fixes landed in v1.0.1 (PR #1, squash ce2cbd7). There is a zip + .sha256 release, the ONNX/WASM runtime and its claims are removed, the private path is gone, and permissions are storage only. Previously: completed → needs-work on 2026-10-09 10:34."
short_description: Real-time, private, on-device multilingual grammar & spell checker for Chromium (MV3), using a plain-JS classifier over generated label tables, 35k-word local dictionaries and grammar rules (EN, IT, SL).
repo_url: https://github.com/nodaysidle/nodaysrammar
site_url: https://github.com/nodaysidle/nodaysrammar
local_path: ../chrome-extension
stack:
  - Chrome Manifest V3
  - Plain-JS token classifier over generated label tables (no ONNX/WASM since v1.0.1)
  - Content Scripts (Isolated Shadow DOM)
  - Service Worker Background Engine
  - 35,000-word offline frequency dictionaries (EN, IT, SL)
  - Levenshtein / Damerau edit-distance candidate generator
  - Dynamic viewport boundary detection (auto-flip popover)
tags:
  - catalog
  - chrome-extension
  - on-device-ai
  - nlp
  - privacy
---

# nodaysrammar

Real-time, private, zero-cloud multilingual grammar and spell checker browser extension for Chromium (Chrome, Brave, Edge).

- **Local Path:** `../chrome-extension`
- **Architecture:** Chrome Manifest V3, WebAssembly ONNX inference, isolated Shadow DOM injection, 100% offline. ⚠️ **Conflict (2026-10-09 10:32):** ONNX Runtime Web (`lib/ort.bundle.min.mjs`) is bundled but no script imports it. Inference is a plain-JS forward pass over weights in `vocab-*.json`. See [[artifacts/nodaysrammar/repo-check-2026-10-09]]. ✅ **Resolved in v1.0.1** ([PR #1](https://github.com/nodaysidle/nodaysrammar/pull/1), `ce2cbd7`): the ONNX runtime and `.onnx` files were removed, and the docs now describe plain-JS inference.
- **Languages Supported:** English (`en`), Italian (`it`), Slovenian (`sl`).
- **Core Capabilities:**
  - ~~On-device ONNX token classification models (`en-grammar.onnx`, `it-grammar.onnx`, `sl-grammar.onnx`).~~ Since v1.0.1: on-device plain-JS token classifier over generated per-token label tables (`models/vocab-*.json`).
  - 35,000-word offline local frequency dictionaries for English, Italian, and Slovenian with sub-millisecond candidate generation.
  - Contextual syntax rules (article agreement, linking verb predicate adjectives, Italian elision/accents, Slovenian *s/z* and *k/h* prepositions, conjunction commas).
  - Floating status badge (`✔ EN`, `⚡ N EN`) with one-click in-page language switcher.
  - Intelligent auto-flipping popover that repositions above bottom-docked chat bars (Telegram Web, Discord, Slack) to prevent viewport clipping.
  - One-click "Fix All" and optional "Auto-Fix on Spacebar".
- **Documentation:** See [[wiki/concepts/nodaysrammar-overview]] and `../chrome-extension/USERGUIDE.md`.

- **Status 2026-10-09 10:32 (verified with GitHub; repo not changed):** public, `main` = `4f41689`, created 2026-10-09 10:02. Latest release [v1.0.0](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.0) (10:08), **no downloadable assets**; install by cloning and using Load unpacked. Version 1.0.0 (`manifest.json`, `package.json`). Licence **MIT**. No GitHub homepage. Not on portfolio-nine or the nodaysidle-apps showcase.
  - **Permissions:** `storage`, `activeTab`, `scripting`, `host_permissions: <all_urls>`. The content script runs on all URLs.
  - **Naming:** repo `nodaysrammar`; local folder `../chrome-extension`; manifest name "nodaysrammar - On-Device Multilingual Grammar Checker".
  - ⚠️ **Unverified:** "ONNX neural models". The weights are generated (random seed plus a pseudo-inverse fit to fixed token labels), not trained.
  - ⚠️ **Open:** the release says "Checksums" but has none; USERGUIDE hardcodes `/home/arch/dev/nodaysidle/chrome-extension`.
  - Details: [[artifacts/nodaysrammar/repo-check-2026-10-09]].

- **Status changed 2026-10-09 10:34: completed → needs-work.** Reason: the v1.0.0 release has no assets, the ONNX Runtime Web claim is false (the runtime is bundled but unused), and USERGUIDE contains the owner's private path `/home/arch/dev/nodaysidle/chrome-extension`. It stays needs-work until those release fixes land. Also corrected: the "could of" rule is implemented at `background/inference-engine.js:252` (`/\b(could|should|would)\s+of\b/gi`) at `main` @ `4f41689`.

- **Status 2026-10-09 10:58 (verified with GitHub after the owner-approved release): needs-work → active.** [PR #1](https://github.com/nodaysidle/nodaysrammar/pull/1) was squash-merged 10:55 as `ce2cbd7`. The latest release is now [v1.0.1](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.1), marked Latest, with `NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip` (740,320 bytes, SHA-256 `31d86ad88491798dbc7a891793cf4824681244e734ab4fb4935db9567a5a6e6d`) + `.sha256`. `sha256sum -c` passed. The zip has 39 entries and no docs, GIF, `lib/` or `.onnx`. Version 1.0.1 (`manifest.json`, `package.json`). CI and Release workflows are green. v1.0.0 is untouched.
  - **Permissions:** `storage` only; content script on `<all_urls>`; no `host_permissions` or `web_accessible_resources`. ✅ The over-broad permissions are resolved.
  - **Naming:** display name "NODAYSIDLE nodaysrammar" (manifest, README, popup/options/onboarding); package and repo name `nodaysrammar`.
  - ✅ **Resolved:** "Checksums" with no checksums (real SHA-256s are in the release notes); the USERGUIDE private path (removed); "ONNX neural models" (docs now say generated label tables, not trained).
  - **Still open:** not on the nodaysidle-apps showcase or portfolio-nine; no GitHub homepage; repo topics still include `onnx` and `webassembly`. ✅ 2026-10-09 11:56: on nodaysidle-apps (card 05), the homepage is set, and `onnx`/`webassembly` were dropped from the topics. Still not on portfolio-nine.

- **Status 2026-10-09 11:56: active, released (v1.0.1 Latest).** PR #2 `81082cf` (11:09) hardened CI: `contents: read`, and browser tests fail instead of being skipped. The repo homepage is now https://nodaysidle-apps.vercel.app. Topics are chrome-extension, grammar-checker, local-first, manifest-v3, privacy, spell-checker (`onnx` and `webassembly` dropped). nodaysrammar is card 05 "Chrome / Chromium (MV3)" on nodaysidle-apps ([PR #2](https://github.com/nodaysidle/nodaysidle-apps/pull/2) `aab4c1d`, 11:52; 12/12 links return 302). The display name "NODAYSIDLE nodaysrammar" has no "g" on purpose. **Still open:** not on the Chrome Web Store (sideload only); the owner's local `../chrome-extension` is at `4f41689` and needs `git pull` (origin `main` = `81082cf`). Verified by Grok Bot (ATLAS): GitHub API, re-downloaded zip SHA-256 `31d86ad8…6e6d` matches, live site checked.
