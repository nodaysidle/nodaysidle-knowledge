---
type: catalog-entry
name: Cascade v3
status: in-progress
short_description: Spec-driven architecture engine—turns ambiguous ideas into agent-ready software plans with verified contracts.
repo_url: https://github.com/nodaysidle/nodaysidle-cascade-v3
site_url: https://github.com/nodaysidle/nodaysidle-cascade-v3
local_path: ../nodaysidle-cascade-v3
stack:
  - "[PLACEHOLDER: see upstream README]"
tags:
  - catalog
  - ai-tools
updated: 2026-10-17
---

# Cascade v3

Featured on the portfolio as “Cascade”. Use this catalog entry when researching spec pipelines and multi-agent planning.

- **Repo:** [github.com/nodaysidle/nodaysidle-cascade-v3](https://github.com/nodaysidle/nodaysidle-cascade-v3)
- **Portfolio blurb:** `../Portfolio/data/presentation.json` → `cascade-v3`

- **Status 2026-10-08 (verified 22:30 UTC+2):** public, `main` = `9e38b03` (README promo GIF, PR #2). Latest release [v3.1.0](https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/tag/v3.1.0) (2026-09-27): aarch64 DMG + Linux tar.gz, AppImage and deb. No open PRs, no GitHub homepage. Listed on the official portfolio (portfolio-nine).
  - ⚠️ **Stale elsewhere:** the non-canonical showcase-v2 still links the v3.0.0 DMG and says "Not … Linux". The v3.1.0 release body is still DMG-only. ✅ Release body fixed 2026-10-08 22:48: it covers macOS + Linux and names no keys. Key names were removed from the README ([PR #3](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/3), `def99ca`) and USERGUIDE ([PR #4](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/4), `f8f6850`). Recorded by SHIP in the reconcile artifact.
  - ⚠️ **Conflict:** SWEEP says the repo was private on 2026-10-07; the vault recorded it public at 2026-10-07 13:55.
  - **Downloads showcase (2026-10-08 23:41):** listed on https://nodaysidle-apps.vercel.app (v3.1.0, macOS arm64 + Linux). See [[_system/templates/catalog/nodaysidle-apps]].
  - Details: [[wiki/concepts/cascade-v3-overview]] · [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].

- ## Update 2026-10-11 20:10 (UTC+2) — weekly reconcile (ATLAS)
  - Live re-check: v3.1.0 still Latest with 4 assets; on portfolio (01/09) and apps (card 01). Visibility-history conflict remains **open**.
  - [[artifacts/vault-operations/repo-status-reconcile-2026-10-11]]
- 2026-10-15 01:55 (ATLAS): v3.1.0 X post Thu 2026-10-15 17:30 (drafts by REACH). README gaps: no DMG checksum; the Linux links go to the tag page, not direct URLs. ⚠️ **Media pointer corrected 2026-10-15 12:42 UTC (ATLAS):** this line named the v1 clip `/workspace/clips/cascade/cascade.mp4`, which no longer resolves — no `cascade.mp4`/`cascade.gif` exists in the clip tree (first-hand `find`, 12:40 UTC; same class as [[sessions/handoffs/2026-10-15-REEL]] lines 96–105). The media for the post is **`cascade-v2.mp4`**, 2,184,964 B, sha256 `11f8d9a5…` — re-hashed first-hand at 12:40 UTC.
- 2026-10-15 12:42 UTC (ATLAS, correction pass): **the clip pointer above is stale** — `/workspace/clips/cascade/cascade.mp4` (v1) does not exist at that path; the file for the post is **`cascade-v2.mp4`** (2,184,964 B, sha256 `11f8d9a5…`), and no v1 `cascade.mp4`/`cascade.gif` exists under `/home/arch` (`find`, 2026-10-15 12:38 UTC). The v3.1.0 X package is **locked and owner-approved** (Alan's words relayed by MASTER_ALAN at 12:20 UTC), nothing posted; slot 17:30 Europe/Ljubljana = 15:30 UTC. See [[briefs/x-drafts/2026-10-15-cascade]].
- 2026-10-15 02:30 (ATLAS, README sweep batch 1): README #5 merged as `3edd3cc` (DMG SHA-256 + direct Linux links). README gaps closed.
- 2026-10-15 12:42 UTC (ATLAS, correction pass): launch package **locked and owner-approved** — 14:10 Europe/Ljubljana = 12:10 UTC. The verbatim owner words ("Approved. Proceed with the Cascade v3.1.0 launch package and sync the vault.") reached the vault only as MASTER_ALAN's 12:20 UTC **relay**, with no first-hand copy, and are recorded as relayed in [[sessions/LATEST]]. **Nothing posted** — the slot is Thu 15 Oct 17:30 Europe/Ljubljana = 15:30 UTC; media `cascade-v2.mp4`, caption "Five doc tabs", pipeline 0/11, no generation claim. Variant A stays gated. Vault commit/push still open (`origin/main` `e9f67db`).
- 2026-10-17 (Claude Opus, catalog reconcile against [[sessions/LATEST]] and [[artifacts/2026-10-17-vault-and-grokbot-audit]]): v3.1.0 is **released, not promoted**. The Thu 15 Oct 17:30 post did **not** go live (owner 2026-10-16 10:26), so the 2026-10-15 approval line above is **stale**. Cascade is held for the **big launch** (plan: [[briefs/launch/cascade-big-launch-PLAN]]); no Reddit post. `local_path` set (cloned on arch).
