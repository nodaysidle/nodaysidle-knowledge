---
type: catalog-entry
name: ShareGuard
status: completed
short_description: Local-first macOS privacy scanner that checks files for secrets, contact details and local paths before you share them.
github_status: published
repo_url: https://github.com/nodaysidle/nodaysidle-shareguard
site_url: https://github.com/nodaysidle/nodaysidle-shareguard/releases
local_path: "[PLACEHOLDER: ../nodaysidle-shareguard when cloned locally]"
stack:
  - macOS native
tags:
  - catalog
  - native
  - macos
---

# ShareGuard

Portfolio group: **Native apps** (`nodaysidle-shareguard`). Research angles: secret detection, redaction, local-first scanning. Licence: proprietary (GitHub shows NOASSERTION), so promo says "DMG on GitHub", never "MIT" ([[wiki/concepts/x-promo-strategy]]).

- **Repo:** [github.com/nodaysidle/nodaysidle-shareguard](https://github.com/nodaysidle/nodaysidle-shareguard)
- **Created:** 2026-10-08 by Grok Bot (ATLAS) during the repo-status reconcile. `status: completed` was set by the agent because a release has shipped; the owner should confirm it.
- **Status 2026-10-08 (verified 22:30 UTC+2):** public, `main` = `fc8bb3d` (README promo GIF, PR #3). Latest release [v0.1.0-dmg.20260727](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.0-dmg.20260727) (2026-07-27) with `ShareGuard-0.1.0.dmg` + `.sha256`. The older [v0.1.0](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.0) has the macOS ZIP. No GitHub homepage set. **Not** on the official portfolio (portfolio-nine).
  - **Open:** [PR #4](https://github.com/nodaysidle/nodaysidle-shareguard/pull/4) (draft, awaiting owner review) points README Installation at the DMG. `main` still links only the v0.1.0 ZIP. ✅ **Merged 2026-10-08 22:30 (UTC+2):** the owner approved it and it was squash-merged as `eeaaca0`, so `main` = `eeaaca0` (the earlier `fc8bb3d` HEAD is stale). Verified at 22:32: README Installation links `ShareGuard-0.1.0.dmg` + `.sha256` from `v0.1.0-dmg.20260727`, with SHA-256 `590bd3e0…84fd` matching the release digest. The README-links-ZIP conflict is resolved.
  - ⚠️ **Conflict:** tag `v0.1.1` ("NODAYSIDLE theme fleet v0.1.1", 2026-07-24) is a theme-only release with no assets. By version number it looks newer than the real app build.
  - **Update 2026-10-08 22:47–22:54 (recorded by SHIP in the reconcile artifact):** [v0.1.2](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.2) is now Latest and carries the same 0.1.0 DMG. `v0.1.1` is a pre-release, which resolves the tag conflict above. The README was updated via [PR #5](https://github.com/nodaysidle/nodaysidle-shareguard/pull/5) (`4332029`). ShareGuard is **not** on the new downloads showcase ([[_system/templates/catalog/nodaysidle-apps]]).
  - Details: [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].
