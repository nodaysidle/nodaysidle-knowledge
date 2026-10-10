---
type: catalog-entry
name: NODAYSIDLE Apps (downloads showcase)
status: completed
short_description: Static downloads showcase for the NODAYSIDLE desktop apps (Cascade, Sonora, WhisperBar, NODAYSIDLE Browser for Linux and, since 2026-10-09, the nodaysrammar Chrome extension; since 2026-10-10, Kurek v0.2.0), with links to the GitHub release files.
github_status: published
repo_url: https://github.com/nodaysidle/nodaysidle-apps
site_url: https://nodaysidle-apps.vercel.app
vercel_project: nodaysidle-apps (prj_avsKTC0wU3lCdS3UZEfcZs4jT56d, team muhambals-projects)
local_path: "[PLACEHOLDER: ../nodaysidle-apps when cloned locally]"
stack:
  - Node.js 22+
  - static HTML/CSS/JS
tags:
  - catalog
  - web
  - portfolio
---

# NODAYSIDLE Apps (downloads showcase)

The **downloads showcase** for the desktop apps. It is separate from the official portfolio ([[_system/templates/catalog/portfolio-site]], portfolio-nine), which was left untouched and stays the official portfolio. showcase-v2 / nodaysidle-project-pages remain stale.

- **Repo:** [github.com/nodaysidle/nodaysidle-apps](https://github.com/nodaysidle/nodaysidle-apps) (public). [PR #1](https://github.com/nodaysidle/nodaysidle-apps/pull/1) was squash-merged to `main` as `44052bc` (2026-10-08 23:38 UTC+2). The GitHub homepage is set to the site.
- **Site:** https://nodaysidle-apps.vercel.app. Live since 2026-10-08 ~23:38–23:40 UTC+2.
- **Vercel:** a new project, `nodaysidle-apps` (`prj_avsKTC0wU3lCdS3UZEfcZs4jT56d`), in team `muhambals-projects`.
  - Production deployment `dpl_A6j2ZFBRn3yc1r85EXdQHS6By8zV`: READY at 23:38, built from git `main` @ `44052bc`.
  - The production branch is `main` and the project auto-deploys on push (per Execution Operator; the deployment is git-triggered and has a `git-main` alias).
- **Build:** `vercel.json` runs `npm run build`, which is `node scripts/build.mjs`, and outputs `dist/`. There is no framework. `package.json` requires `node >=22`; the Vercel project's Node setting is `24.x`. The site sets a strict CSP and security headers. Data comes from `data/apps.json`, and media from `public/assets/media/`.
- **Apps on the site (chosen by ATLAS):** *(4 at launch; 5 since 2026-10-09 11:56, see below.)*
  - Cascade v3.1.0: macOS arm64 + Linux (tar.gz, AppImage, deb).
  - Sonora v0.1.1: macOS arm64 (dmg, app.tar.gz) + Linux (AppImage, deb, rpm).
  - WhisperBar v1.1.2: macOS Apple Silicon (dmg).
  - NODAYSIDLE Browser for Linux v0.1.0: Linux x86_64 (AppImage).
- **Not on the site:** ShareGuard and the macOS nodaysidle-browser.
- **Verified 2026-10-08 23:40 (UTC+2):** the site returns HTTP 200 and all 11 release download links return 302. Execution Operator ran the same check. The research notes are on the agent box at `/workspace/showcase-research/` (README and release snapshots, 23:06–23:10). They are not in this vault. *(Superseded 2026-10-09 11:56: 12/12 links return 302.)*
- **Built by:** Execution Operator through a cloud agent.
- ⚠️ **Open (owner decision):** nodaysidle-browser-linux has no licence, so its card says "No licence specified". The GitHub API also detects no licence on the nodaysidle-apps repo itself.
- Details: [[artifacts/vault-operations/repo-status-reconcile-2026-10-08]].

- **Update 2026-10-09 11:56 (UTC+2): five tools.** [PR #2](https://github.com/nodaysidle/nodaysidle-apps/pull/2) "Add nodaysrammar Chrome MV3 extension as fifth showcase card" was merged 11:52:59 as `aab4c1d`. *(Superseded 2026-10-10 07:35: six tools, see below.)*
  - Card 05 is nodaysrammar v1.0.1, labelled "Chrome / Chromium (MV3)" ([[_system/templates/catalog/nodaysrammar]]).
  - The site copy now says "Five tools." and "Desktop tools & a Chrome extension".
  - Verified live: HTTP 200, and 12/12 release download links return 302, including `NODAYSIDLE-nodaysrammar-1.0.1-chrome.zip`.
  - REEL's demo clip (mp4 + gif, v1.0.1 title card) is on the agent box at `/workspace/clips/nodaysrammar/`.

- **Update 2026-10-10 07:35 (UTC+2): six tools.** Kurek (kureksistant v0.2.0, Linux x86_64) is card 06.
  - **[nodaysidle-apps PR #3](https://github.com/nodaysidle/nodaysidle-apps/pull/3) `46251cb`** "Add Kurek v0.2.0 as sixth showcase card" was squash-merged 07:32:00 CEST; Vercel status success; `main` = `46251cb`. It changes `data/apps.json`, `src/index.html` and `scripts/build.mjs` and adds the `public/assets/media/kurek.{mp4,webm,webp,jpg}` media.
  - **Live check, 07:35:** https://nodaysidle-apps.vercel.app returns HTTP 200 and shows "Six tools." and "06 / 06". The page has `#kurek` (nav link) and `#app-kurek`, and **14/14** release download and checksum links return **302**, including kureksistant v0.2.0's tarball and `SHA256SUMS.txt`.
  - **Card credit and media:** the card text says "Requires your own DeepSeek and xAI API keys. Derived from FatihMakes' JARVIS under CC BY-NC 4.0 (non-commercial)." The live `kurek.mp4` has a video **and an audio** track, so it is the voiced clip. The voice-over scripts on the box (`/workspace/clips/kurek/vo/tts.py`, `seg.py`) use OpenRouter `openai/gpt-audio` with voice `onyx`. The page itself doesn't name the voice. The live file is re-encoded, so its hash differs from `/workspace/clips/kurek/kurek-vo.mp4`.
  - **Six apps:** Cascade, Sonora, WhisperBar, NODAYSIDLE Browser for Linux, nodaysrammar, Kurek.
