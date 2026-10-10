---
type: wiki-note
note_kind: concept
topic_slug: nodaysrammar
status: active
release_status: released
status_note: "Changed needs-work → active on 2026-10-09 10:58: the release fixes landed in v1.0.1 (PR #1, squash ce2cbd7). There is a zip + .sha256 release, the ONNX/WASM runtime and its claims are removed, the private path is gone, and permissions are storage only. Previously: completed → needs-work on 2026-10-09 10:34."
created: 2026-10-09
updated: 2026-10-09
verified: 2026-10-09T10:58:00+02:00
tags:
  - wiki
  - nodaysrammar
  - chrome-extension
  - on-device-ai
  - nlp
---

# nodaysrammar — Overview

## Summary

**nodaysrammar** is a production-ready, local-first Chromium browser extension (Manifest V3) that performs real-time multilingual grammar and spell checking inside web page text fields (`textarea`, `input`, and `contenteditable`). It runs 100% offline and on-device with zero remote API calls, zero telemetry, and zero tracking. ⚠️ *"Production-ready" is unverified (2026-10-09 10:32): no tests were run, and the models are generated, not trained. See [[artifacts/nodaysrammar/repo-check-2026-10-09]].* ✅ *Update 2026-10-09 10:58: from v1.0.1 the repo itself no longer claims "production-grade". CI runs 19 regression tests plus live headless-browser extension tests, all green. The label tables are still generated, not trained, and the docs now say so.*

Supported languages: **English (`en`)**, **Italian (`it`)**, and **Slovenian (`sl`)**.

## Architectural Highlights

### 1. Zero-Cloud Privacy & On-Device AI Engine
- **Local ONNX Models:** Bundled under `models/` (`en-grammar.onnx`, `it-grammar.onnx`, `sl-grammar.onnx`) and loaded lazily into browser service worker memory via `ModelLoader`. ⚠️ **Conflict (2026-10-09 10:32):** `ModelLoader` fetches each `.onnx` file but keeps only its byte length. The forward pass runs in plain JS (`NeuralModelSession`) on weights stored in `models/vocab-*.json`. The bundled ONNX Runtime Web is not imported by any script. The weights come from `scripts/generate_real_models.py`: random values plus a pseudo-inverse fit to fixed per-token labels, with no training. ✅ **Resolved in v1.0.1 (2026-10-09 10:55, [PR #1](https://github.com/nodaysidle/nodaysrammar/pull/1), `ce2cbd7`):** `lib/` and the `.onnx` files were deleted. `ModelLoader` now fetches only `models/vocab-*.json` (plus `dict-*.json` in `spell-corrector.js`), and the docs describe a plain-JS classifier over generated label tables.
- **35,000-Word High-Frequency Dictionaries:** Built from curated corpus frequency tables (`dict-en.json`, `dict-it.json`, `dict-sl.json`) enabling instant candidate generation ($<1\text{ms}$) across tens of thousands of words via Levenshtein / Damerau edit distance algorithms.
- **Syntactic Contextual Rules:**
  - **English:** Indefinite article agreement (*a apple* $\rightarrow$ *an apple*), linking verb predicate adjectives (*is beautifully* $\rightarrow$ *is beautiful*), modal verbs (*could of* $\rightarrow$ *could have*), subject-verb contractions (*he don't* $\rightarrow$ *he doesn't*).
  - **Italian:** Compound conjunction accents (*perche* $\rightarrow$ *perché*), third-person *è* vs *e*, elision rules (*un'amica*, *qual è* without apostrophe, *d'accordo*).
  - **Slovenian:** Preposition *s/z* before voiceless consonants (*Ta suhi škafec pušča*), preposition *k/h* before *k* and *g*, and mandatory commas before conjunctions (*ki, ko, ker, da, če*).
- **Cross-Lingual Fallback:** If the extension is explicitly set to Slovenian or Italian, but the user types English (or vice versa), the engine automatically detects the input language and applies corrections, preventing silent false positives.

### 2. Isolated Shadow DOM In-Page UI
- Injected via `content/content-script.js` into an isolated Shadow DOM host (`#nodaysrammar-root`) with `z-index: 2147483647` and CSS resetting (`all: initial`) to guarantee zero style conflicts with host websites (including dark-mode chat apps like Telegram Web).
- **Floating Badge:** Displays dynamic state (`✔ EN` / `⚡ N EN`).
- **Zero-Errors Status Card:** Clicking `✔ EN` opens an in-page popover displaying detected language, confidence, and an immediate dropdown to switch active language without leaving the tab.
- **Dynamic Auto-Flip Positioning:** Intelligently calculates viewport space (`spaceBelow` vs `spaceAbove`). When text fields are positioned at the bottom of the screen (e.g. Telegram Web chat bar), the popover automatically flips **above** the field and clamps to viewport boundaries to eliminate screen clipping.
- **Actions:** Individual "Accept" and "Ignore" actions, one-click "Fix All", and optional "Auto-Fix on Spacebar".

## Verification & Testing
- Automated end-to-end tests via headless Chromium (`test-live.js`) covering:
  1. Service worker initialization and model pre-warming.
  2. Options page and runtime status checks.
  3. Live field injection, typing debouncing, and badge rendering.
  4. Popover auto-flip above bottom-docked chat bars.
  5. Multi-error detection across the 35,000-word vocabulary.
  6. Non-destructive text replacement across standard inputs and rich contenteditable containers.

## Related Links
- Catalog Entry: [[_system/templates/catalog/nodaysrammar]]
- MOC: [[wiki/MOC/moc-nodaysidle-knowledge]]
- Local Repository: `../chrome-extension`
- User Guide: `../chrome-extension/USERGUIDE.md`

## Current status (2026-10-09 10:32 UTC+2)

Verified against GitHub (`main` @ `4f41689`) by Grok Bot (ATLAS). The full comparison is in [[artifacts/nodaysrammar/repo-check-2026-10-09]].

- **Repo:** [nodaysidle/nodaysrammar](https://github.com/nodaysidle/nodaysrammar), public, default branch `main`, created 2026-10-09 10:02, 2 commits. MIT licence. No homepage.
- **Version / release:** 1.0.0. [v1.0.0](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.0) was published 10:08 with no downloadable assets, so install means Load unpacked from a clone. Its "Included Assets & Checksums" section lists repo files but no checksums.
- **Permissions:** `storage`, `activeTab`, `scripting`; host and content-script access to `<all_urls>`; `models/*`, `assets/*` and `lib/*` are web-accessible.
- **Browsers per repo docs:** Chrome, Brave, Edge, Arc, Chromium (README); Vivaldi (USERGUIDE).
- **Tests:** `tests/test-live.js` and `tests/test-autofix.js` (Puppeteer). Not run by the agent.
- **Naming:** repo `nodaysrammar`; local folder `../chrome-extension`. USERGUIDE tells users to load `/home/arch/dev/nodaysidle/chrome-extension`, a local path in public docs.

## Contradictions & gaps

1. ONNX Runtime Web / WASM inference is claimed but not wired up (see the ⚠️ marker above).
2. The "neural" models are not trained (see above). "Production-ready" is unverified.
3. The English rules listed here (could of, linking verbs) differ from the README list (homophones, double negatives). ~~"could of" was not found in `inference-engine.js`.~~ ✅ Corrected 2026-10-09 10:34: the rule is implemented at `background/inference-engine.js:252` (`/\b(could|should|would)\s+of\b/gi`) at `main` @ `4f41689` (confirmed on GitHub). The two lists differ only in emphasis.
4. No source notes have been ingested. The claims in this note come from the repo docs as summarised by Antigravity, plus this check.

## Current status (2026-10-09 10:58 UTC+2)

Verified on GitHub by Grok Bot (SHIP) after the owner-approved release (approved in chat 10:39). This section supersedes the 10:32 status above.

- **Merge:** [PR #1](https://github.com/nodaysidle/nodaysrammar/pull/1) "Release-ready v1.0.1: drop ONNX/WASM, REEL fixes, CI + release zip" was squash-merged 2026-10-09 10:55:15 as `ce2cbd74c7cc1465f94d6fd414599548b9eff16d`, pinned to head `c3a2329`. The merge tree is identical to the head tree. CI on the PR head passed: 19/19 regression tests, live extension tests and auto-fix tests in headed Chromium under xvfb.
- **Release:** [v1.0.1](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.1) "NODAYSIDLE nodaysrammar v1.0.1", tagged at `ce2cbd7`. The Release workflow built the assets and passed its version check (manifest = package = 1.0.1). It is marked Latest. [v1.0.0](https://github.com/nodaysidle/nodaysrammar/releases/tag/v1.0.0) is unchanged.
  - `NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip`: 740,320 bytes, SHA-256 `31d86ad88491798dbc7a891793cf4824681244e734ab4fb4935db9567a5a6e6d`.
  - `….zip.sha256`: 107 bytes. Re-downloaded and checked with `sha256sum -c` (OK).
  - The zip has 39 entries (30 files + 9 dirs) under `nodaysrammar/`. It has no `docs/`, GIF, `lib/`, `.onnx`, `.md`, tests or scripts. gitleaks and trufflehog found nothing.
- **Manifest 1.0.1:** name "NODAYSIDLE nodaysrammar - On-Device Multilingual Grammar Checker". Permissions are **`storage` only**, and the content script runs on `<all_urls>`. There are no `host_permissions` and no `web_accessible_resources`.
- **Blocklist:** the content script checks `chrome.storage.sync` before attaching listeners and detaches on change. The README Privacy section mentions Chrome Sync.
- **Docs:** no ONNX/WASM, "production" or `/home/arch` claims remain apart from the historical `docs/RELEASE-NOTES-v1.0.0.md`. The English rule list matches `inference-engine.js`. Display name is "NODAYSIDLE nodaysrammar". Install is: download zip → `sha256sum -c` → unzip → `chrome://extensions` → Developer mode → Load unpacked. Not on the Chrome Web Store.
- **Still open:** not listed on the nodaysidle-apps showcase or portfolio-nine. No GitHub homepage. Repo topics still include `onnx` and `webassembly`. ✅ 2026-10-09 11:56: on nodaysidle-apps (card 05, `aab4c1d`), homepage set, `onnx`/`webassembly` dropped from the topics. Still not on portfolio-nine.

### Contradictions resolved by v1.0.1

- #1 (ONNX Runtime Web / WASM): ✅ resolved. The runtime and claims were removed.
- #2 (untrained "neural" models / production-ready): ✅ resolved in the docs. The models are described as generated label tables, and CI tests now run.
- #3 (English rule lists): ✅ resolved. README and USERGUIDE list exactly the rules in code (a/an incl. silent-h, linking verb + adverb, their/there, its/it's, could/should/would of, he don't / they doesn't, I has / he have, repeated words).
- Release with no assets or checksums, the private USERGUIDE path, and over-broad permissions: ✅ resolved (see above).

## Update 2026-10-09 11:56 (UTC+2): CI hardening, homepage, showcase

Status: **active, released** (v1.0.1 Latest). The 10:58 section above covers PR #1 and the resolved contradictions; this adds only what changed since. PR #2 `81082cf` (11:09) hardened CI: `contents: read`, and browser tests fail instead of being skipped. The repo homepage is now https://nodaysidle-apps.vercel.app. Topics are chrome-extension, grammar-checker, local-first, manifest-v3, privacy, spell-checker (`onnx` and `webassembly` dropped). nodaysrammar is card 05 "Chrome / Chromium (MV3)" on nodaysidle-apps ([PR #2](https://github.com/nodaysidle/nodaysidle-apps/pull/2) `aab4c1d`, 11:52; 12/12 links return 302). The display name "NODAYSIDLE nodaysrammar" has no "g" on purpose. **Still open:** not on the Chrome Web Store (sideload only); the owner's local `../chrome-extension` is at `4f41689` and needs `git pull` (origin `main` = `81082cf`). Verified by Grok Bot (ATLAS): GitHub API, re-downloaded zip SHA-256 `31d86ad8…6e6d` matches, live site checked.
