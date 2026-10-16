---
type: source-readme
repo: "nodaysidle/nodaysrammar"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc"
source_commit_date: "2026-10-15T02:29:28+02:00"
readme_path: "README.md"
readme_blob_sha: "191a60a11ec0d7abe581c0a0a3c01b39ac0e2086"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/nodaysrammar/blob/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/README.md"
tags: [source, readme, nodaysrammar]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/nodaysrammar` at `1de303b` (2026-10-15T02:29:28+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<p align="center">
  <img src="https://raw.githubusercontent.com/nodaysidle/nodaysrammar/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/assets/icons/icon-128.png" width="128" height="128" alt="NODAYSIDLE nodaysrammar icon">
</p>

<h1 align="center">NODAYSIDLE nodaysrammar</h1>

<p align="center">
  <strong>On-device, zero-telemetry multilingual grammar and spell checker for Chromium.</strong><br>
  A small JS classifier, ~35,000-word offline dictionaries, and grammar rules — your keystrokes never leave the browser.
</p>

<p align="center">
  <img alt="Chrome MV3" src="https://img.shields.io/badge/Chrome-MV3-4285F4?style=flat-square&logo=google-chrome&logoColor=white">
  <img alt="Languages" src="https://img.shields.io/badge/Languages-EN%20%7C%20IT%20%7C%20SL-0B3D91?style=flat-square">
  <img alt="Privacy" src="https://img.shields.io/badge/Privacy-100%25%20On--Device-success?style=flat-square">
  <img alt="Telemetry" src="https://img.shields.io/badge/Telemetry-None-4c8c6b?style=flat-square">
  <img alt="Not on CWS" src="https://img.shields.io/badge/Chrome%20Web%20Store-not%20listed-lightgrey?style=flat-square">
  <img alt="License" src="https://img.shields.io/badge/License-MIT-green?style=flat-square">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/nodaysidle/nodaysrammar/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/docs/media/nodaysrammar.gif" alt="NODAYSIDLE nodaysrammar demo">
</p>

<p align="center">
  <a href="https://github.com/nodaysidle/nodaysrammar/releases"><strong>Download Releases</strong></a>
  ·
  <a href="USERGUIDE.md"><strong>User Guide</strong></a>
  ·
  <a href="codemap.md"><strong>Architecture Map</strong></a>
</p>

<p align="center">
  <a href="#why">Why</a> ·
  <a href="#features">Features</a> ·
  <a href="#privacy">Privacy</a> ·
  <a href="#install">Install</a> ·
  <a href="#usage">Usage</a> ·
  <a href="#architecture">Architecture</a> ·
  <a href="#development">Development</a> ·
  <a href="#license">License</a>
</p>

---

## Why

Cloud writing assistants send drafts and keystrokes to remote servers. **NODAYSIDLE nodaysrammar** keeps every check inside your browser process: a small JS token classifier over fixed label tables, ~35k-word frequency dictionaries, and deterministic grammar rules for English, Italian, and Slovenian.

It is **not** listed on the Chrome Web Store. Install from [GitHub Releases](https://github.com/nodaysidle/nodaysrammar/releases) (or build from source) via Load unpacked.

---

## Features

- **100% on-device**: no analytics, no remote inference, works offline.
- **English rules** (exact): a/an (including silent-h vowel sounds such as *honest* / *hour*), linking verb + adverb, their/there, its/it's, could/should/would of, he don't / they doesn't, I has / he has agreement, repeated words — plus dictionary + label-table spelling.
- **Italian**: accents (`perché`, `è`), elision (`un'` / `un`, `qual è`), common orthography.
- **Slovenian**: preposition phonetics (`s`/`z`, `k`/`h`), commas before `ki`/`ko`/`ker`/`da`/`če`.
- **Isolated Shadow DOM** overlays (badge, underlines, auto-flipping suggestion card).
- **Safe replacement** with caret/undo preservation and synthetic `input`/`change` events.
- **Fix All** and optional auto-fix on Space/Enter.
- **Per-site blocklist** synced via `chrome.storage.sync`.

---

## Privacy

All grammar and spell checking runs **on-device** in the extension service worker and content script. Text is never sent to a server. Preferences — including the site blocklist, language, and toggles — sync through **Chrome Sync** (`chrome.storage.sync`) when you are signed into Chrome; they are not uploaded to nodaysidle.

Manifest permissions: **`storage` only**. Content scripts match `<all_urls>` so checking works on normal websites; blocked domains disable listeners on those hosts.

---

## Install

### Download from Releases (recommended)

1. Download [`NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip`](https://github.com/nodaysidle/nodaysrammar/releases/download/v1.0.1/NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip) and its [`.sha256`](https://github.com/nodaysidle/nodaysrammar/releases/download/v1.0.1/NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip.sha256) file (SHA-256 `31d86ad88491798dbc7a891793cf4824681244e734ab4fb4935db9567a5a6e6d`), or any version from [Releases](https://github.com/nodaysidle/nodaysrammar/releases).
2. Verify the archive: `shasum -a 256 -c NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip.sha256`
3. Unzip the archive.
4. Open `chrome://extensions` (or the equivalent page in Brave / Edge / Arc).
5. Enable **Developer mode**.
6. Click **Load unpacked** and select the unzipped `nodaysrammar` folder.

Checksums and release notes for each version live on the [Releases](https://github.com/nodaysidle/nodaysrammar/releases) page.

### Build from source

```bash
git clone https://github.com/nodaysidle/nodaysrammar.git
cd nodaysrammar
# Load the repo root as an unpacked extension (no build step required)
```

Then Load unpacked as above, pointing at the clone root.

---

## Usage

1. Focus any `input`, `textarea`, or `contenteditable` field.
2. After a short debounce, squiggly hints and a corner badge appear when issues are found.
3. Click the badge (or an underline) for replacements, or **Fix All**.
4. Use the toolbar popup to toggle the engine, pick a language, or open Settings for the blocklist.

---

## Architecture

```mermaid
flowchart TD
    A["Editable field"] -->|debounce 350ms| B["Content script"]
    B -->|chrome.runtime.sendMessage| C["Service worker"]
    subgraph OnDevice ["On-device pipeline"]
      C --> D["Language detector"]
      D --> E["~35k-word dictionaries"]
      D --> F["JS token classifier (vocab-*.json)"]
      D --> G["Grammar regex rules"]
      E --> H["Suggestions"]
      F --> H
      G --> H
    end
    H --> I["Shadow DOM overlay"]
    I --> J["Caret-preserving replace"]
```

Assets: `models/vocab-*.json` (fixed per-token label tables generated with seed 42 — **not trained**), `models/dict-*.json`, and plain JS in `background/`.

---

## Development

```bash
npm install
npm run test:regressions   # unit / REEL regressions (no browser)
npm test                   # live Puppeteer suite (set NODAYSRAMMAR_BROWSER if needed)
npm run test:autofix
python3 scripts/generate_real_models.py   # regenerate vocab-*.json label tables
```

Browser binary resolution: `NODAYSRAMMAR_BROWSER`, then `CHROME_PATH` / `CHROMIUM_PATH`, then common Chrome/Chromium paths (defaulting away from a hard-coded Brave Origin path).

See [`USERGUIDE.md`](https://github.com/nodaysidle/nodaysrammar/blob/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/USERGUIDE.md), [`codemap.md`](https://github.com/nodaysidle/nodaysrammar/blob/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/codemap.md), [`AGENTS.md`](https://github.com/nodaysidle/nodaysrammar/blob/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/AGENTS.md), and [`CHANGELOG.md`](https://github.com/nodaysidle/nodaysrammar/blob/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/CHANGELOG.md).

---

## License

[MIT License](https://github.com/nodaysidle/nodaysrammar/blob/1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc/LICENSE) © 2026 [nodaysidle](https://github.com/nodaysidle)
