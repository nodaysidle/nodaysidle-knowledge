---
type: brief
topic_slug: "readme-sweep"
version: 1
status: closed-executed
review_status: completed
reviewer: "owner (closure requested in chat 2026-10-17)"
reviewed_at: 2026-10-17
completion_note: "Batch 1 executed 5/5 on 2026-10-15 (cascade-v3 #5 3edd3cc, sonora #3 f8b45ba, browser-linux #5 ca1bc3e, nodaysrammar #3 1de303b, kureksistant #23 e5341b7). Closed per [[artifacts/2026-10-17-vault-and-grokbot-audit]]. Not promoted; nothing under projects/."
promoted: false
project_slug: ""
tags:
  - brief
  - readme-sweep
---

# Brief: README sweep: direct download links and checksums (Batch 1)

> Owner ask, relayed by EO at 2026-10-15 02:08 CEST: "SHIP: plan batch 1 of the README sweep, starting with nodaysidle-cascade-v3 (add the Mac DMG checksum and direct Linux download links). Plan only, no PRs yet. I'll approve the batch."
> **This is a plan only.** No branches, PRs or repo edits have been made.

## Problem / opportunity

The app READMEs differ in how they offer downloads. Some link only to the release page, some have no checksums, and Kurek's says there is no APK even though v0.2.1 now has one. Each README should give **direct asset URLs plus a SHA-256** for the current release, so readers of the X posts (Cascade, Thu 15 Oct 17:30; Kurek, Wed 21 Oct 17:30) can download and verify in one step.

## Recommendation

Batch 1 is five docs-only PRs, one per repo, each changing one file (`README.md`). Put **nodaysidle-cascade-v3 first**, because it's the owner's ask and it posts today. Then kureksistant (posts Wed 21), nodaysidle-sonora, nodaysidle-browser-linux and nodaysrammar.

**Why these five:**
- All five are on nodaysidle-apps.vercel.app and have release assets.
- Each has a real gap: no checksum, links to the tag page instead of the asset, or a stale statement.

**Deferred:**
- **whisper-bar** and **nodaysidle-shareguard** already have direct DMG links and SHA-256s that match the GitHub asset digests (WhisperBar `7db0c6d5…84da`, ShareGuard `590bd3e0…e8fd`).
- They are macOS-only, and the owner has no Mac to verify them on.

## Scope

- **In scope:** README download/install sections only: direct asset links and SHA-256 values for the current Latest release.
- **Out of scope:** code, release assets, GIF/media changes, marketing claims (speed, "tested on M4", RAM). Those would need separate verification.

## Evidence (checked 2026-10-15 ~02:10, gh read-only)

| Repo | Latest release | Assets | README top: pitch / GIF / download near top | Direct asset links | Checksums in README |
|---|---|---|---|---|---|
| nodaysidle-cascade-v3 | v3.1.0 | aarch64 DMG, AppImage, deb, linux tar.gz | yes / `docs/cascade.gif` / "Download Releases" (the releases page, L27) | DMG only (L94); Linux points to the tag page (L130) | Linux ×3 (L134-136) ✅ match; **DMG missing** |
| kureksistant | v0.2.1 | linux tar.gz, debug APK, SHA256SUMS.txt | yes / **no GIF** / Release badge links the tag | **none**; install is `git clone` | **none** |
| nodaysidle-sonora | v0.1.1 | aarch64 DMG, AppImage, deb, rpm, app.tar.gz | yes / `docs/sonora.gif` / DMG + AppImage buttons (L26-28) | DMG, AppImage; deb/rpm only by name, on the tag page (L162) | **none** |
| nodaysidle-browser-linux | v0.2.0 | AppImage, SHA256SUMS | yes / `docs/browser-linux.gif` / Download section at L53 | AppImage v0.2.0 + v0.1.0 (L55) | **none** (SHA256SUMS exists in the release) |
| nodaysrammar | v1.0.1 | chrome.zip + .sha256 | yes / `docs/media/nodaysrammar.gif` / Releases link (L50) | **none** (`<version>` placeholder, L79) | **none** (the command uses the .sha256 file) |
| whisper-bar (deferred) | v1.1.2 | DMG | yes / gif / yes | yes (L167) | yes ✅ matches the digest |
| nodaysidle-shareguard (deferred) | v0.1.2 | DMG + .sha256 | yes / gif / yes | yes (L54) | yes ✅ matches the digest |

**Cascade v3.1.0:** downloaded on the box and hashed with sha256sum. Every value matches the GitHub API `digest`.

| Asset | SHA-256 | Direct URL |
|---|---|---|
| NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg | `1aec1ffd45ce4dde171210a3ad1a0b195da0214316b2d1adb27e2657979ed3d9` | https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/download/v3.1.0/NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg |
| NODAYSIDLE.Cascade.V3_3.1.0_amd64.AppImage | `fe784421f37d6148e1c8f13639ad261cbe930ab6357f8d25528e9c8ed120eac4` | https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/download/v3.1.0/NODAYSIDLE.Cascade.V3_3.1.0_amd64.AppImage |
| NODAYSIDLE.Cascade.V3_3.1.0_amd64.deb | `5dddd77aef0f4c5156cd1987547ebda5f3e06f795ba11d6809a87c08dedb297e` | https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/download/v3.1.0/NODAYSIDLE.Cascade.V3_3.1.0_amd64.deb |
| NODAYSIDLE-Cascade-V3-3.1.0-linux-x86_64.tar.gz | `f3e7693d2d9ed9657fca75f4168295c4283ca280a0636537ce606990419b83b3` | https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/download/v3.1.0/NODAYSIDLE-Cascade-V3-3.1.0-linux-x86_64.tar.gz |

There are **no checksum mismatches**. The three Linux SHA-256s in the Cascade README (L134-136) equal both the downloaded files and the API digests.

**For the other repos,** the values come from the GitHub API `digest`. Each will be re-checked by download when its PR is made.
- Sonora: DMG `85bb2213…9727`, AppImage `16e9bdc2…346c`, deb `2f8ca891…2ecb`, rpm `6defc8d5…88b6`, app.tar.gz `fe18857a…7b9d`.
- Browser: AppImage `02d7a85c…ad93`.
- nodaysrammar: zip `31d86ad8…6e6d`.
- Kurek: tarball `8b3a7a6e…6b33`.

**GIF sources** (box `/workspace/clips/`): there is a GIF for cascade, sonora, browser-linux, nodaysrammar, whisperbar, shareguard, kurek and kurek-remote (`kurek-remote-v021.gif` is the v0.2.1 one), plus cliprail and synapse-notes. All batch-1 READMEs except kureksistant already embed a GIF.

## Proposed changes, per repo (one docs-only PR each, commit trailer `Agent: SHIP`)

### 1. nodaysidle-cascade-v3: `README.md` (~+6/-4 lines)
- L94 before: ``1. Download [`NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg`](…/download/v3.1.0/NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg).``
  after: the same line, plus a new sub-line: ``   SHA-256: `1aec1ffd45ce4dde171210a3ad1a0b195da0214316b2d1adb27e2657979ed3d9`. Verify with `shasum -a 256 NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg`.``
- L130 before: ``2. Download one of the v3.1.0 Linux assets from [GitHub Releases](…/releases/tag/v3.1.0) and verify it with `sha256sum`:``
  after: ``2. Download one of the v3.1.0 Linux assets below (direct links) and verify it with `sha256sum`:``
- L134-136: the first cell of each row becomes a direct link, e.g. ``| [`NODAYSIDLE.Cascade.V3_3.1.0_amd64.AppImage`](https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/download/v3.1.0/NODAYSIDLE.Cascade.V3_3.1.0_amd64.AppImage) | `fe78…` |``. The same applies to the deb and tar.gz rows. The hashes stay as they are.
- Optional (owner choice): change the top button at L27 to point at `releases/latest`. Recommendation: leave it.

### 2. kureksistant: `README.md` (~+12/-0, plus an optional ±3)
- Add before "### 1. Clone and run the installer" (L83):
  ```
  ### Option: download the v0.2.1 bundle
  Download [`kureksistant-v0.2.1-linux-x86_64.tar.gz`](https://github.com/nodaysidle/kureksistant/releases/download/v0.2.1/kureksistant-v0.2.1-linux-x86_64.tar.gz) and [`SHA256SUMS.txt`](https://github.com/nodaysidle/kureksistant/releases/download/v0.2.1/SHA256SUMS.txt), then:
      sha256sum -c --ignore-missing SHA256SUMS.txt   # tarball: 8b3a7a6ec36795d6651a3b38d36b62f5dc1590a5a17abe1a3604ecf8c7a96b33
      tar -xzf kureksistant-v0.2.1-linux-x86_64.tar.gz && cd kureksistant-0.2.1 && ./install_linux.sh
  ```
  These steps match the v0.2.1 release notes, which were checked against `install_linux.sh`.
- ⚠️ **Owner decision:** README L14 (badge "Android app (build from source)"), L47 ("No APK release has been published") and L176 ("There is **no published APK**") are no longer true. The v0.2.1 release has `kurek-remote-v0.2.1-debug.apk`. Options:
  - (a) Reword to "a debug-signed APK is attached to the v0.2.1 release; or build from `android/`".
  - (b) Leave it, to keep the APK low-profile in line with the post rule "keep the APK out of post copy".
  - Recommendation: (a), but with **no direct APK link** in the README.

### 3. nodaysidle-sonora: `README.md` (~+10/-1)
- L162 before: ``1. Download `Sonora_0.1.1_amd64.AppImage`, `Sonora_0.1.1_amd64.deb` or `Sonora-0.1.1-1.x86_64.rpm` (Fedora / openSUSE) from [Releases](…/releases/tag/v0.1.1).``
  after: the three names become direct `releases/download/v0.1.1/…` links.
- After the Install heading (L150), add a SHA-256 table for all five v0.1.1 assets (values as above, re-verified by download).

### 4. nodaysidle-browser-linux: `README.md` (~+4/-0)
- After L55, add:
  ``SHA-256 (v0.2.0 AppImage): `02d7a85c3d99f5e395425722c57c46d12fabceccd063554b7f01c2b43229ad93` ([SHA256SUMS](https://github.com/nodaysidle/nodaysidle-browser-linux/releases/download/v0.2.0/SHA256SUMS)). Verify with `sha256sum -c SHA256SUMS`.``

### 5. nodaysrammar: `README.md` (~+3/-1)
- L79 before: ``1. Open [Releases](https://github.com/nodaysidle/nodaysrammar/releases) and download `NODAYSIDLE-nodaysrammar-<version>-chrome.zip` plus the matching `.sha256` file.``
  after: ``1. Download [`NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip`](https://github.com/nodaysidle/nodaysrammar/releases/download/v1.0.1/NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip) and [`.sha256`](https://github.com/nodaysidle/nodaysrammar/releases/download/v1.0.1/NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip.sha256) (SHA-256 `31d86ad88491798dbc7a891793cf4824681244e734ab4fb4935db9567a5a6e6d`), or any version from [Releases](https://github.com/nodaysidle/nodaysrammar/releases).``
- L80: `<version>` → `1.0.1` in the verify command.

**Batch total:** 5 PRs, 5 files (`README.md` each), about 35-45 lines. Each PR re-downloads its assets and checks the sha256 before committing, then runs a secret scan and waits for CI where the repo has it. None are merged without the owner.

## Batch 1 PRs (opened 2026-10-15 ~02:20, status: open)

Owner approval, relayed by EO at 2026-10-15 02:13 CEST: "Approve all 5, Kurek APK wording as SHIP recommends".

| Repo | PR | Branch | Head SHA | CI | Status |
|---|---|---|---|---|---|
| nodaysidle-cascade-v3 | https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/5 | `readme-cascade-direct-downloads` | `db1afb4f4d7a85ece10b7f9cf74d31cab1a79fca` | checks ✅ (2 runs) | open |
| kureksistant | https://github.com/nodaysidle/kureksistant/pull/23 | `readme-kurek-download-bundle` | `802d810e2c3020402c50172660909a707977fe40` | lint-and-smoke ✅ | open (needs EO merge gate) |
| nodaysidle-sonora | https://github.com/nodaysidle/nodaysidle-sonora/pull/3 | `readme-sonora-checksums` | `df2483340fe4ae083d76c63d0716be25f1af7015` | no PR CI (only release workflows) | open |
| nodaysidle-browser-linux | https://github.com/nodaysidle/nodaysidle-browser-linux/pull/5 | `readme-browser-checksum` | `96269b8c782dba50b417ef3bfd05f2eca7c52ecb` | check ✅ | open |
| nodaysrammar | https://github.com/nodaysidle/nodaysrammar/pull/3 | `readme-nodaysrammar-direct-download` | `fae8265364bf0e56fbd185a86702dbd6f777e665` | test ✅ | open |

Every hash was re-verified by fresh download and every new URL returns 200. The gitleaks and rg scans were clean. Only `README.md` changed in each PR.

Deviations from the plan:
- **browser-linux:** the SHA-256 line goes after the run commands' code block, not directly after L55, because L55 leads into that block.
- **kureksistant:** the Android badge text changes too ("build from source" → "debug APK in v0.2.1"). The L47 and L176 wording also says to uninstall the old copy first. There is no direct APK link; only the release page is linked.

## Risks & unknowns

- **Version-pinned links go stale on the next release.** Every new release must update the README links and checksums too. A mitigation for a later batch: generate the links in release CI, or use `releases/latest/download/<name>` only where asset names don't contain the version (this applies to none of these five).
- **macOS assets can't be run-tested** (no Mac). For Cascade and Sonora DMGs only the checksum is verified, not that the app works.
- **Cascade posts today at 17:30.** If the PR merges before then, the README improves. If it doesn't, nothing breaks, because the current links work.
- **Kurek APK wording** needs an owner decision (see 2). The rule is never to link the debug APK in posts.
- **Claims not touched:** Sonora "Tested and measured live on M4", Cascade "one model call", and WhisperBar "zero third-party…" are unverified marketing claims. They're out of scope for this batch and could be audited in batch 2.
- **kureksistant README was just rewritten** (#14); there's a small conflict risk if someone else edits it at the same time.

## Suggested project shape (if promoted)

- Repos: nodaysidle-cascade-v3, kureksistant, nodaysidle-sonora, nodaysidle-browser-linux, nodaysrammar.
- Milestones: (1) Cascade PR, today, before 17:30 if the owner approves; (2) the other four PRs; (3) batch 2: whisper-bar and shareguard claims review, plus release-time README automation.

## Review checklist (human only)

Agents must not set `review_status: approved`.

- [ ] sources_cited
- [ ] claims_verified
- [ ] scope_clear

## Approval record

(Filled by human after review.)
