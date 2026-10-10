---
type: wiki-note
note_kind: concept
topic_slug: cascade-v3
status: draft
created: 2026-10-07
updated: 2026-10-08
tags:
  - wiki
  - cascade-v3
---

# NODAYSIDLE Cascade V3 — overview

## Summary

Cascade V3 is a Tauri 2 desktop app (macOS Apple Silicon, with Linux bundles from v3.1.0). It turns one software idea plus one locked stack preset into exactly five agent-ready markdown files: PRD, ARD, TRD, TASKS and AGENTS. One DeepSeek request supplies the product meaning; a deterministic local TypeScript compiler owns the IDs, graph, files, phases and the exact markdown bytes. Licence: MIT.

## Details

- **Pipeline:** Jev preflight → one DeepSeek request (plus at most one repair request) → schema validation → Jev integrity checks → normalization → preset compiler → audits → render → SHA-256 → atomic export of exactly five files.
- **Presets:** SwiftUI desktop, SwiftUI menubar, Tauri 2, Astro web, Android Compose.
  - v3.1.0 verified three of them with real apps: ReceiptShelf, PinBoard/Murmur and PromptShelf.
  - Android and Astro are not verified.
- **Starter kits:** v3.1.0 exports a tested `kit/` folder for the verified stacks.
- **Privacy:** no accounts or telemetry. The DeepSeek and TypeSafe Jev keys are held in memory only.
- **Releases:**
  - v3.0.0 (2026-09-06)
  - v3.0.1 (2026-09-23)
  - v3.1.0 (2026-09-27; DMG, Linux tar.gz, AppImage, deb)
  - 60 commits in total. ⚠️ Stale as of 2026-10-08: `b5d1d1d` and `9e38b03` have landed since; `main` = `9e38b03`.

## Contradictions & gaps

1. **Platform:** the README says "Apple Silicon only. No Windows, Linux, or Intel macOS build", yet it has a Linux install section and v3.1.0 ships Linux assets. AGENTS.md and the spec still say "macOS app".
2. **Repair:** the README features table says "no retry, no repair pass" and the 2026-08-29 spec says "no provider repair". The README layer table, AGENTS.md and v3.1.0 all say at most one repair request. The current rule is one repair.
3. **Keys:** v3.1.0 install says you need "your own DeepSeek API key", while the README requires separate DeepSeek **and** TypeSafe Jev keys. ✅ Resolved 2026-10-08 22:57 (owner: "the keys should not be seen"). The [v3.1.0 release body](https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/tag/v3.1.0) (edited 22:48) names no keys. Key names and key/probe setup were removed from the README ([cascade-v3 PR #3](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/3), `def99ca`) and USERGUIDE.md ([cascade-v3 PR #4](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/4), `f8f6850`). Both now say generically that you enter your own provider credentials in the app (memory-only).
4. **Release notes:** v3.1.0 gives only the DMG install steps and checksum, although Linux assets are attached. The Linux bundle commit `d79ec73` comes after the 3.1.0 release commit `6294841`. ~~⚠️ Still open as of 2026-10-08 22:30: the GitHub release body is unchanged. Only the README covers Linux (`b5d1d1d`).~~ ✅ Resolved 2026-10-08 22:48: the [v3.1.0 release body](https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/tag/v3.1.0) was rewritten with macOS DMG and Linux AppImage/deb/tar.gz install steps and SHA-256 for all 4 assets. It notes that the Linux assets were built from `d79ec73`, which matches the tag apart from bundle targets, CI and ROADMAP. A secret scan of the bodies, assets and git history found no real secrets. See [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].
5. **Not ingested:** `ROADMAP.md` (referenced by AGENTS.md), `CLAUDE.md` and `audit/CHANGELOG.md` (build-audit log). All are outside the requested scope.
6. **No PRD/ARD/TRD/TASKS of its own:** the repo produces those files rather than containing them.

## Claims & citations

| Claim | Source |
|-------|--------|
| Purpose, pipeline, presets, privacy, MIT, platform contradiction | [[sources/index/src-20261007-305a501-cascade-v3-readme]] |
| One repair request, compiler linking rules, ROADMAP pointer | [[sources/index/src-20261007-c789017-cascade-v3-agents]] |
| "No provider repair", standalone macOS app | [[sources/index/src-20261007-0937509-cascade-v3-design-spec-2026-08-29]] |
| Releases, assets, verified stacks, kits | [[sources/index/src-20261007-5351bd3-cascade-v3-github-releases]] |
| 60 commits, Linux commit order | [[sources/index/src-20261007-3f34f6c-cascade-v3-git-log]] |

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[_system/templates/catalog/cascade-v3]]

## Decisions and fixes (user, 2026-10-07 14:07 UTC+2; commit `b5d1d1d`, push pending authentication)

- **#1 README platform:** the "Apple Silicon only" line now says macOS builds are Apple Silicon only, with Linux x86_64 listed below.
- **#2 Repair:** the README now says at most one repair request. The 2026-08-29 spec has a historical banner.
- **#3 Keys:** the README Linux section adds the DeepSeek + TypeSafe Jev key requirement (TypeSafe System One API, `api.typesafe.ai`, taken from `src-tauri/src/jev.rs:9`). No release-notes file exists in the repo; the v3.1.0 notes live only on GitHub and are unchanged (no `gh` login).
- **#4 Linux install:** steps and SHA-256 for the three v3.1.0 Linux assets, taken from the GitHub asset digests, were added to the README.
- **#5:** AGENTS.md and the spec now say "macOS + Linux".

## Current status (2026-10-08 22:30 UTC+2)

Verified against the public GitHub API by Grok Bot (ATLAS) during [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]]. Newer facts here take precedence over Details.

- **Repo:** public. `main` = `9e38b03` (README promo GIF, PR #2, merged 2026-10-07 22:54). No open PRs, no GitHub homepage URL. Licence MIT.
- **Latest release:** v3.1.0 (2026-09-27 07:11) with `NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg`, `NODAYSIDLE-Cascade-V3-3.1.0-linux-x86_64.tar.gz`, `NODAYSIDLE.Cascade.V3_3.1.0_amd64.AppImage` and `NODAYSIDLE.Cascade.V3_3.1.0_amd64.deb`.
- **Demo GIF:** `docs/cascade.gif` is in the README and loads.
- ⚠️ **Conflict, visibility history:** SWEEP (2026-10-08 22:18) reported the repo as "now public" and said it was private as of 2026-10-07. This vault recorded it as public via the API on 2026-10-07 13:55 ([[_system/reference/github-org-repositories]]). When, or whether, visibility changed is unverified.
- **Showcase:** listed on the official portfolio (nodaysidle-portfolio-nine.vercel.app, owner-confirmed).
  - ⚠️ Stale: the non-canonical showcase-v2 (nodaysidle-project-pages, last push 2026-09-06) still links the v3.0.0 DMG and says "Not Intel, Windows, or Linux".
- ~~**Still open:** the v3.1.0 release body still gives DMG-only steps and asks only for "your own DeepSeek API key" (contradictions #3 and #4; session next action 17).~~ ✅ Resolved 2026-10-08 22:48–22:57: see contradictions #3 and #4. `main` is now `f8f6850` after [cascade-v3 PR #3](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/3) and [cascade-v3 PR #4](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/4).
