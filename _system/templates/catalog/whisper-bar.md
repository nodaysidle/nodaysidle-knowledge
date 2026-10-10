---
type: catalog-entry
name: WhisperBar
status: completed
short_description: macOS menu-bar dictation—voice input into any application.
repo_url: https://github.com/nodaysidle/whisper-bar
site_url: https://github.com/nodaysidle/whisper-bar
local_path: "[PLACEHOLDER: ../whisper-bar when cloned locally]"
stack:
  - macOS native
tags:
  - catalog
  - native
  - macos
---

# WhisperBar

Portfolio group: **Native apps**. Research angles: speech APIs, privacy, on-device vs cloud transcription.

- **Repo:** [github.com/nodaysidle/whisper-bar](https://github.com/nodaysidle/whisper-bar)

- **Status 2026-10-08 (verified 22:30 UTC+2):** public, `main` = `becc15a` (README demo GIF, PR #1). Latest release [v1.1.2](https://github.com/nodaysidle/whisper-bar/releases/tag/v1.1.2) with `WhisperBar.dmg`. No GitHub homepage set. Listed on the official portfolio (portfolio-nine).
  - **Open:** [PR #2](https://github.com/nodaysidle/whisper-bar/pull/2) (draft, awaiting owner review) adds the v1.1.2 DMG download, SHA-256 and Gatekeeper note to README Installation. It also fixes the clone URL; `main` still says `your-username`. ✅ **Merged 2026-10-08 22:30 (UTC+2):** the owner approved it and it was squash-merged as `239f1a7`, so `main` = `239f1a7` (the earlier `becc15a` HEAD is stale). Verified at 22:32: README Installation links the v1.1.2 `WhisperBar.dmg` with expected SHA-256 `7db0c6d5…84da`, matching the release digest, and the clone URL is `github.com/nodaysidle/whisper-bar.git`.
  - ⚠️ **Conflict:** the README says MIT, but GitHub detects no licence file. ✅ Resolved 2026-10-08 22:58: an MIT `LICENSE` was added via [PR #3](https://github.com/nodaysidle/whisper-bar/pull/3) (`2108144`), recorded by SHIP in the reconcile artifact.
  - **Downloads showcase (2026-10-08 23:41):** listed on https://nodaysidle-apps.vercel.app (v1.1.2, macOS Apple Silicon DMG). See [[_system/templates/catalog/nodaysidle-apps]].
  - Details: [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].
