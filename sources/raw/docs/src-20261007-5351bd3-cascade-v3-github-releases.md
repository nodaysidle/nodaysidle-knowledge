# GitHub releases — nodaysidle/nodaysidle-cascade-v3

Fetched 2026-10-07 from https://api.github.com/repos/nodaysidle/nodaysidle-cascade-v3/releases (verbatim release bodies).

## v3.1.0 — Cascade v3.1.0

- published_at: 2026-09-27T05:11:31Z
- prerelease: false
- assets: NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg (sha256:1aec1ffd45ce4dde171210a3ad1a0b195da0214316b2d1adb27e2657979ed3d9), NODAYSIDLE-Cascade-V3-3.1.0-linux-x86_64.tar.gz (sha256:f3e7693d2d9ed9657fca75f4168295c4283ca280a0636537ce606990419b83b3), NODAYSIDLE.Cascade.V3_3.1.0_amd64.AppImage (sha256:fe784421f37d6148e1c8f13639ad261cbe930ab6357f8d25528e9c8ed120eac4), NODAYSIDLE.Cascade.V3_3.1.0_amd64.deb (sha256:5dddd77aef0f4c5156cd1987547ebda5f3e06f795ba11d6809a87c08dedb297e)

# Cascade V3 3.1.0

Cascade turns one software idea and one tech stack into five build documents (PRD, ARD, TRD, TASKS, AGENTS) that a coding agent can build a working app from. This release makes that true for three stacks, each proven by real apps built from Cascade packets and checked by using them, not only by their tests.

## Verified stacks

- **Native macOS desktop (SwiftUI):** ReceiptShelf.
- **Native macOS menu bar (SwiftUI):** PinBoard and Murmur, a speech-to-text app with a global shortcut, auto-paste, and several providers.
- **Tauri 2 (Rust + TypeScript):** PromptShelf, a prompt library with a quick picker, a menu-bar menu, DeepSeek improvement, and import and export. Every feature was verified live.

Android (Kotlin/Compose) and Astro are still available but are not verified yet.

## What's new

### Starter kits
- Every verified stack now exports a tested **starter kit** under `kit/` next to the five documents: the app skeleton, visible errors, safe settings and database storage, keys in the macOS keychain, launch at login, a menu-bar or tray setup, and an install script. The agent starts from code that already builds and passes its tests, instead of rewriting the tricky parts.
- Kit files are chosen from what the idea declares, so an app only gets the storage, keychain, plugins, and permissions it needs.
- The Tauri kit pins exact, tested versions, including Tauri's internal crates, so a new upstream release cannot break a build that worked yesterday.
- Kits include UI building blocks (native-looking menus, settings rows, empty states, disabled actions, clamped long text), so built apps look finished, not just functional.

### Better documents
- The provider answers each fact once, as a required field: which features show file panels, every option in a choice list, and which sentence of your idea asks for each feature. A feature your idea never asked for is rejected.
- Every packet requires the final launch check to look at the app, with screenshots of every screen, and to leave no test data behind. "It opens" no longer counts as "it works".
- Clearer rules for the traps real builds hit: clipboard apps that only copy never watch the clipboard; single-key shortcuts such as Right Option; Tauri windows that need permission to call commands; windows that must reopen with fresh data.
- One repair request when the provider's answer fails a check, with messages that say exactly what to change. A harmless duplicate entry no longer fails a run.
- Exports can include `blueprint.json`, the provider's validated answer, to see exactly what was declared.

### The app
- A new dark look with a teal accent, fitting the window without scrolling; the pipeline shows as one row of steps.

## Install

1. Download `NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg` (Apple Silicon).
2. Open it and drag **NODAYSIDLE Cascade V3** to Applications.
3. The app is signed ad hoc, not notarized. On first launch, Control-click it and choose **Open**.

You need your own DeepSeek API key; keys are kept in memory only and are never saved or exported.

**SHA-256:** `1aec1ffd45ce4dde171210a3ad1a0b195da0214316b2d1adb27e2657979ed3d9`


**Full Changelog**: https://github.com/nodaysidle/nodaysidle-cascade-v3/compare/v3.0.1...v3.1.0

## v3.0.1 — Cascade v3.0.1

- published_at: 2026-09-23T09:04:59Z
- prerelease: false
- assets: NODAYSIDLE-Cascade-V3-3.0.1-aarch64.dmg (sha256:09cb04a90d1f2de9496192cfb64377570d7c7beff77dac42c22334ae6e657ff3)

## NODAYSIDLE Cascade V3 3.0.1

Local-first macOS app (Tauri 2) — one software idea into five agent-ready markdown contracts.

### Download
- `NODAYSIDLE-Cascade-V3-3.0.1-aarch64.dmg` — Apple Silicon, **ad-hoc signed** (not notarized). First open: right-click → Open if Gatekeeper blocks.

### Compiler fixes
- **Tighter traceability:** features link to data, permissions and categories only through affirmed text (negated clauses are ignored), so save scratch files, keybindings and filesystem permissions no longer attach to unrelated features.
- **Recovery text follows the stated failure:** exit, automatic fallback or explicit retry, as the blueprint says; memory-only data reports that the last in-memory state stays valid.
- **Leaner locked stack:** Application Support is dropped when no persistence placement uses it.
- **Correct macOS floor:** SwiftUI presets now declare `LSMinimumSystemVersion = 14.0`, matching the `@Observable` stack they lock (previously 13.0).
- **Jev guardrails:** viability and preset-fit preflight before DeepSeek, platform-needs healing, and a stack-leakage integrity gate.
- **Provider cleanup:** removed the Deepgram and OpenRouter provider paths.

## What's Changed
* ci: hybrid release — tag notes in CI, attach DMG locally by @nodaysidle in https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/1

## New Contributors
* @nodaysidle made their first contribution in https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/1

**Full Changelog**: https://github.com/nodaysidle/nodaysidle-cascade-v3/compare/v3.0.0...v3.0.1


## v3.0.0 — Cascade V3 3.0.0

- published_at: 2026-09-06T03:02:51Z
- prerelease: false
- assets: NODAYSIDLE-Cascade-V3-3.0.0-aarch64.dmg (sha256:ecfe1b6933a06c3b4eef5a7094c86cb616575537f5da4124052e74f70ae8504a)

## NODAYSIDLE Cascade V3 3.0.0

Local-first macOS app (Tauri 2) — one software idea into five agent-ready markdown contracts.

### Download
- `NODAYSIDLE-Cascade-V3-3.0.0-aarch64.dmg` — Apple Silicon, **ad-hoc signed** (not notarized). First open: right-click → Open if Gatekeeper blocks.

### Notes
- Version 3.0.0 from `main`.
- No accounts, no cloud product claims in this release.

