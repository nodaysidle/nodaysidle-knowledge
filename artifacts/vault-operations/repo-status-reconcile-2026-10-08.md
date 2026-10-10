---
type: artifact
artifact_kind: audit
topic_slug: vault-operations
generated: 2026-10-08
generator_agent: auditor
verified_at: 2026-10-08T22:30:00+02:00
scope:
  - whisper-bar
  - nodaysidle-cascade-v3
  - nodaysidle-sonora
  - nodaysidle-shareguard
  - nodaysidle-browser-linux
tags:
  - artifact
  - audit
  - repo-status
---

# Audit: repo status reconcile, five public repos (2026-10-08)

Run 2026-10-08 22:28–22:40 (UTC+2) by Grok Bot (ATLAS), per user ("Reconcile the vault for those 5 repos now"). Inputs: the SWEEP report (22:18) and the SHIP report (22:27). Each claim was re-checked against the public GitHub REST API, the raw README files on the default branch, both showcase sites, and the Vercel project `nodaysidle-portfolio`. No GitHub repo or Vercel project was changed. All times are UTC+2.

## Current status (verified ~22:30)

| Repo | Visibility | Default branch / HEAD | Latest release (published) | Download assets | README GIF | Homepage | Open PRs | Licence (GitHub API) |
|---|---|---|---|---|---|---|---|---|
| [whisper-bar](https://github.com/nodaysidle/whisper-bar) | public | `main` / `becc15a` → `239f1a7` (2026-10-08 22:30) → `2108144` (22:58) | [v1.1.2](https://github.com/nodaysidle/whisper-bar/releases/tag/v1.1.2) (2026-09-22 01:13) | `WhisperBar.dmg` | `docs/whisperbar.gif` (loads) | none | [#2](https://github.com/nodaysidle/whisper-bar/pull/2) (draft) → ✅ merged `239f1a7` | MIT (`LICENSE` added via [whisper-bar PR #3](https://github.com/nodaysidle/whisper-bar/pull/3), merged 2026-10-08 22:58 as `2108144`) |
| [nodaysidle-cascade-v3](https://github.com/nodaysidle/nodaysidle-cascade-v3) | public | `main` / `9e38b03` → `def99ca` (22:54) → `f8f6850` (22:57) | [v3.1.0](https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/tag/v3.1.0) (2026-09-27 07:11) | aarch64 `.dmg`, linux-x86_64 `.tar.gz`, amd64 `.AppImage`, amd64 `.deb` | `docs/cascade.gif` (loads) | none | none | MIT |
| [nodaysidle-sonora](https://github.com/nodaysidle/nodaysidle-sonora) | public | `main` / `e3add87` | [v0.1.1](https://github.com/nodaysidle/nodaysidle-sonora/releases/tag/v0.1.1) (2026-09-16 03:59; body edited 2026-10-08 22:24) | aarch64 `.dmg`, `Sonora_aarch64.app.tar.gz`, amd64 `.AppImage`, amd64 `.deb`, x86_64 `.rpm` | `docs/sonora.gif` (loads) | none | none | MIT |
| [nodaysidle-shareguard](https://github.com/nodaysidle/nodaysidle-shareguard) | public | `main` / `fc8bb3d` → `eeaaca0` (2026-10-08 22:30) → `4332029` (22:54) | [v0.1.0-dmg.20260727](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.0-dmg.20260727) (2026-07-27 02:39) → [v0.1.2](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.2) (2026-10-08 22:47, same 0.1.0 DMG) | `ShareGuard-0.1.0.dmg` + `.sha256` | `docs/shareguard.gif` (loads) | none | [#4](https://github.com/nodaysidle/nodaysidle-shareguard/pull/4) (draft) → ✅ merged `eeaaca0` | NOASSERTION (proprietary per [[wiki/concepts/x-promo-strategy]]) |
| [nodaysidle-browser-linux](https://github.com/nodaysidle/nodaysidle-browser-linux) | public | **`master`** / `a813e70` | [v0.1.0](https://github.com/nodaysidle/nodaysidle-browser-linux/releases/tag/v0.1.0) (2026-10-07 09:38) | `nodaysidle-browser-x86_64.AppImage` | `docs/browser-linux.gif` (loads) | none | none | none detected |

The HEAD of each repo is the README GIF merge from 2026-10-07 between 22:23 and 22:55 (whisper-bar #1, cascade-v3 #2, sonora #2, shareguard #3, browser-linux #1).

## Work recorded today (2026-10-08)

- **SHIP, sonora v0.1.1 release notes (done):** the body was rewritten (release edited 22:24). It now covers the Linux Spotify sign-in fix, the docs cleanup, a download table for all 5 files, and SHA-256s. The SHA-256s match the GitHub asset digests (checked 22:30).
- **SHIP, [whisper-bar PR #2](https://github.com/nodaysidle/whisper-bar/pull/2) (open, draft, mergeable):** README Installation gets the v1.1.2 `WhisperBar.dmg` download, a SHA-256 check and a Gatekeeper note. It also fixes the clone URL; `main` still says `github.com/your-username/whisper-bar.git`. Waiting on owner review. ✅ **Merged 2026-10-08 22:30** as `239f1a7` (owner-approved squash; verified 22:32).
- **SHIP, [shareguard PR #4](https://github.com/nodaysidle/nodaysidle-shareguard/pull/4) (open, draft):** README Installation is pointed at `ShareGuard-0.1.0.dmg` + `.sha256` from `v0.1.0-dmg.20260727`, with a fallback to the v0.1.0 ZIP. `main` still links only the ZIP. Waiting on owner review. ✅ **Merged 2026-10-08 22:30** as `eeaaca0` (owner-approved squash; verified 22:32).

## Showcase surfaces

- **Official (owner-confirmed via SWEEP, 2026-10-08):** https://nodaysidle-portfolio-nine.vercel.app, served by the Vercel project `nodaysidle-portfolio` (Vite). Its last production deployment was READY on 2026-10-07 09:38. Of these five repos it lists Cascade, WhisperBar and Sonora. Its "NODAYSIDLE Browser" card links the **macOS** `nodaysidle-browser`, not `nodaysidle-browser-linux`. It also links `synapse-notes`. **ShareGuard and browser-linux are not listed.**
- **Stale, not canonical:** https://nodaysidle-showcase-v2.vercel.app ([nodaysidle-project-pages](https://github.com/nodaysidle/nodaysidle-project-pages), last push 2026-09-06 05:26). Of the five it lists only Cascade V3: the CTA links the v3.0.0 DMG and the copy says "Not Intel, Windows, or Linux".

## Contradictions

| Topic | Source A | Source B | Resolution |
|-------|----------|----------|------------|
| cascade-v3 / sonora visibility history | SWEEP (22:18): both "now public" and private as of 2026-10-07; sonora's flip was perhaps around the 2026-10-07 ~22:54 pushes | [[_system/reference/github-org-repositories]]: the 2026-10-07 13:55 correction recorded both as public via the API (cloned anonymously). Only the superseded 10:10 entry called them private | **Open.** Both are public now (API). The vault has not had them as private since 13:55. Any flip time is unverified, and SWEEP may have relied on the superseded 10:10 entry. |
| Which repo deploys portfolio-nine | [[_system/templates/catalog/portfolio-site]] + vault README: the public `Portfolio` repo, "dependency-free" static build; that repo's GitHub homepage is portfolio-nine | Vercel: the domain belongs to project `nodaysidle-portfolio` (Vite). `nodaysidle-portfolio` is private repo #3 in the user's 14:18 list (public API: 404) | ~~**Open.**~~ The Vercel API returned no git link. Needs owner confirmation. ✅ **Resolved 2026-10-08 23:41:** the latest production deployment (`dpl_D3YGzcmFeTnmF9VHpuTaPrUJUFSo`, 2026-10-07 09:38) is from the public `nodaysidle/Portfolio`, `master` @ `a225402`, deployed by hand with `npx vercel --prod` (Vercel API with git info, `source: cli`). Deployments up to 2026-09-18 came from the private `nodaysidle-portfolio` repo (per user; not checked here). |
| Canonical showcase | Vault README + portfolio-site catalog: project-pages / showcase-v2 is the "Showcase" | Owner (via SWEEP, 2026-10-08): portfolio-nine is the official showcase | **Resolved by owner.** showcase-v2 / project-pages is marked stale, not canonical. |
| WhisperBar licence | README: "MIT License" | GitHub API: no licence detected (no LICENSE file recognised) | ~~**Open.**~~ ✅ **Resolved 2026-10-08 22:58:** the owner chose MIT. An MIT `LICENSE` ("Copyright (c) 2026 NODAYSIDLE") matching the README was added via [whisper-bar PR #3](https://github.com/nodaysidle/whisper-bar/pull/3), merged as `2108144`. The GitHub API now detects MIT. |
| ShareGuard install path | README on `main`: v0.1.0 ZIP | Latest release: `v0.1.0-dmg.20260727` DMG | **Pending** PR #4 (draft). ✅ **Resolved 2026-10-08 22:30:** PR #4 was merged as `eeaaca0`. The README on `main` now links `ShareGuard-0.1.0.dmg` + `.sha256` from `v0.1.0-dmg.20260727` (verified 22:32). |
| ShareGuard release tags | Tag `v0.1.1` "NODAYSIDLE theme fleet v0.1.1" (2026-07-24 00:39, **no assets**) | `v0.1.0-dmg.20260727` is GitHub's latest app release | ~~**Open.**~~ ✅ **Resolved 2026-10-08 22:48** (owner-approved): new release [v0.1.2](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.2) at the build commit `7f1888c` re-attaches the unchanged `ShareGuard-0.1.0.dmg` + `.sha256` (SHA-256 `590bd3e0…84fd`, `sha256sum -c` OK). Its notes say it is the same 0.1.0 app build. It is now GitHub's Latest. [v0.1.1](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.1) is marked pre-release with a "not an app release" note. No tag or release was deleted, and no release workflow ran. The README Installation now links the v0.1.2 DMG + `.sha256` via [shareguard PR #5](https://github.com/nodaysidle/nodaysidle-shareguard/pull/5), merged 2026-10-08 22:54 as `4332029`. |
| Cascade v3.1.0 release body | GitHub release: DMG-only install steps; "your own DeepSeek API key" | README (`b5d1d1d`): Linux install + checksums; DeepSeek **and** TypeSafe Jev keys | ~~**Open**~~ ✅ **Resolved 2026-10-08 22:48** (owner-approved; session next action 17): the [v3.1.0 body](https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/tag/v3.1.0) was rewritten. It now covers macOS DMG and Linux AppImage/deb/tar.gz install, gives SHA-256 for all 4 assets, and notes that the Linux assets were built from `d79ec73`. It names no API keys and has no key setup. A secret scan of the bodies, all 4 unpacked assets and the full git history found no real secrets, so nothing needs rotating. Key names and key/probe setup were removed from the README via [cascade-v3 PR #3](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/3) (merged 22:54, `def99ca`) and from USERGUIDE.md via [cascade-v3 PR #4](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/4) (merged 22:57, `f8f6850`). |

## Stale items marked

- [[wiki/concepts/nodaysidle-sonora-overview]]: contradiction #8 (thin v0.1.1 notes) is marked resolved, and the "12 commits" figure is marked stale.
- [[wiki/concepts/cascade-v3-overview]]: the "60 commits" figure is marked stale; contradiction #4 is marked still open.
- [[wiki/concepts/nodaysidle-browser-linux-overview]]: the "56 commits … `2fffaab`" history line is marked stale.
- [[sessions/2026-10-07-vault-operations-session]]: next action 6's optional release-body edit is marked done. The v0.1.0 body already says "Host-dependent AppImage" and gives SHA-256 `f6d82efa…4404`.
- [[_system/templates/catalog/portfolio-site]] and the vault `README.md`: the showcase-v2 / project-pages "Showcase" references are marked stale.

## Coverage gaps

- whisper-bar and shareguard have catalog entries only; no sources are ingested and there is no wiki overview.
- Session line 2026-10-08 02:50 says local clones of all five exist. At 22:35 there was no `../whisper-bar` or `../nodaysidle-shareguard` under `/home/arch/dev/nodaysidle/`. Not investigated further.

## Recommended next research

- Owner: review whisper-bar PR #2 and shareguard PR #4 (both drafts, docs only). ✅ Done 2026-10-08 22:30: both were merged (`239f1a7`, `eeaaca0`).
- Owner: confirm which repo deploys portfolio-nine, and whether ShareGuard and browser-linux should be added to it. ✅ Deploy source resolved 2026-10-08 23:41 (public `Portfolio`, `a225402`). portfolio-nine stays untouched. Instead, browser-linux (not ShareGuard) is on the new downloads showcase.
- Owner: WhisperBar licence file; ShareGuard theme-only `v0.1.1` tag. ✅ Decided 2026-10-08 22:47: v0.1.2 is published and v0.1.1 is demoted. The MIT LICENSE was merged via [whisper-bar PR #3](https://github.com/nodaysidle/whisper-bar/pull/3) (22:58).
- Optional (needs `gh`): update the cascade v3.1.0 release body with the Linux steps and the Jev key. ✅ Done 2026-10-08 22:48 with the Linux steps. On the owner's instruction ("the keys should not be seen"), no key names are included.

## Update 2026-10-08 22:32 (UTC+2): README PRs merged

SHIP reported at 22:31 that the owner approved both README PRs. Verified on GitHub with the public API and the raw README at each merge commit:

- [whisper-bar PR #2](https://github.com/nodaysidle/whisper-bar/pull/2): closed and merged 2026-10-08 22:30:40. Squash commit `239f1a7` is now `main` HEAD. README Installation links the v1.1.2 `WhisperBar.dmg` with expected SHA-256 `7db0c6d5…84da`, matching the release digest. The clone URL is `github.com/nodaysidle/whisper-bar.git`.
- [shareguard PR #4](https://github.com/nodaysidle/nodaysidle-shareguard/pull/4): closed and merged 2026-10-08 22:30:33. Squash commit `eeaaca0` is now `main` HEAD. README Installation links `ShareGuard-0.1.0.dmg` and its `.sha256` from `v0.1.0-dmg.20260727`, with SHA-256 `590bd3e0…84fd` matching the release digest. **The "ShareGuard install path" contradiction is resolved.**
- Still open: the cascade-v3/sonora visibility history, which repo deploys portfolio-nine, the WhisperBar licence, the ShareGuard theme-only `v0.1.1` tag, and the cascade v3.1.0 release body. *(See the 22:50 and 22:58 updates: the last three are resolved and their PRs are merged.)*

## Update 2026-10-08 22:50 (UTC+2): ShareGuard v0.1.2, Cascade notes, WhisperBar licence

The owner approved SHIP's drafts at 22:47. Verified on GitHub with `gh`:

- **ShareGuard:** [v0.1.2](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.2) was published at 22:47:50. Its lightweight tag points at `7f1888c`. It carries `ShareGuard-0.1.0.dmg` + `.sha256`, re-downloaded and checked with `sha256sum -c` (OK; SHA-256 `590bd3e0…84fd`, matching the README). `releases/latest` = `v0.1.2`. [v0.1.1](https://github.com/nodaysidle/nodaysidle-shareguard/releases/tag/v0.1.1) was marked pre-release with a note at 22:48:31. No release workflow ran, because `7f1888c` predates `release-on-tag.yml`. All 4 tags and releases are kept. **The "ShareGuard release tags" contradiction is resolved.** The README PR followed: [shareguard PR #5](https://github.com/nodaysidle/nodaysidle-shareguard/pull/5) (merged 22:54).
- **Cascade:** the [v3.1.0](https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/tag/v3.1.0) body was replaced at 22:48:47. The live body matches the draft and contains no key names. **The "Cascade v3.1.0 release body" contradiction is resolved.** This is also [[wiki/concepts/cascade-v3-overview]] contradictions #3 and #4 (line 62 above), which is the same issue. The overview page itself was not edited. The README and USERGUIDE PRs followed: [cascade-v3 PR #3](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/3) and [cascade-v3 PR #4](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/4) (merged 22:54 and 22:57).
- **WhisperBar:** the owner chose an MIT `LICENSE` ("Copyright (c) 2026 NODAYSIDLE"). It was added via [whisper-bar PR #3](https://github.com/nodaysidle/whisper-bar/pull/3) (merged 22:58).

## Update 2026-10-08 22:58 (UTC+2): follow-up PRs merged

Cloud agents opened these PRs and the owner approved squash merges. Each was verified on GitHub (state merged, merge commit) at 22:59:

- [shareguard PR #5](https://github.com/nodaysidle/nodaysidle-shareguard/pull/5) "docs(readme): install ShareGuard from v0.1.2 release": merged 22:54:51 as `4332029`. README Installation links `releases/download/v0.1.2/`.
- [cascade-v3 PR #3](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/3) "docs(readme): remove API key names and stray key line": merged 22:54:51 as `def99ca`.
- [cascade-v3 PR #4](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/4) "docs(userguide): remove API key names": merged 22:57:52 as `f8f6850`. README.md and USERGUIDE.md on `main` no longer contain API key names, key env vars, `probe:live` or `api.typesafe.ai`.
- [whisper-bar PR #3](https://github.com/nodaysidle/whisper-bar/pull/3) "chore: add MIT LICENSE file": merged 22:58:02 as `2108144`. The `LICENSE` matches the approved text, and the GitHub API now detects MIT. MIT can now be claimed in promo.
- [[wiki/concepts/cascade-v3-overview]]: contradictions #3 and #4 (the release-body issue) are marked resolved.

## Update 2026-10-08 23:41 (UTC+2): downloads showcase live; portfolio-nine deploy source

Recorded by Grok Bot (ATLAS) and verified with the public GitHub API, the Vercel API and live HTTP checks at 23:40.

- **New downloads showcase:** https://nodaysidle-apps.vercel.app, from the repo [nodaysidle-apps](https://github.com/nodaysidle/nodaysidle-apps) (public).
  - [PR #1](https://github.com/nodaysidle/nodaysidle-apps/pull/1) was squash-merged as `44052bc` at 23:38.
  - It runs on the new Vercel project `nodaysidle-apps` (`prj_avsKTC0wU3lCdS3UZEfcZs4jT56d`, team `muhambals-projects`). Production deployment `dpl_A6j2ZFBRn3yc1r85EXdQHS6By8zV` was READY at 23:38, from git `main` @ `44052bc`.
  - Build: a static site built by `node scripts/build.mjs` into `dist/`.
  - Apps listed:
    - Cascade v3.1.0 (macOS arm64 + Linux);
    - Sonora v0.1.1 (macOS arm64 + Linux);
    - WhisperBar v1.1.2 (macOS Apple Silicon);
    - NODAYSIDLE Browser for Linux v0.1.0 (Linux x86_64).
  - The site returns 200 and all 11 release download links return 302.
  - Built by Execution Operator through a cloud agent. ATLAS chose the apps; the research notes are on the agent box at `/workspace/showcase-research/`.
  - Catalog page: [[_system/templates/catalog/nodaysidle-apps]].
- **Showcase coverage of the five repos, now:**
  - cascade-v3, sonora and whisper-bar are on both the portfolio and the downloads showcase.
  - browser-linux is on the downloads showcase only.
  - ShareGuard is on neither.
- **Contradiction "Which repo deploys portfolio-nine": resolved.** The table above has the details. portfolio-nine was left untouched and is still the official portfolio. showcase-v2 / project-pages remain stale.
- **Still open:**
  - the cascade-v3/sonora visibility history;
  - the browser-linux licence (the downloads card says "No licence specified"; owner decision).
- **Minor difference:** the user's note says Node 22. `package.json` requires `node >=22`, but the Vercel project's Node setting is `24.x`.
- SHIP's 22:47–22:58 fixes (ShareGuard v0.1.2, the Cascade notes and key-name removal, the WhisperBar MIT LICENSE) are already recorded above in the 22:50 and 22:58 updates, so they are not repeated here.
