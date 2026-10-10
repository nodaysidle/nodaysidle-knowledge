---
type: wiki-note
note_kind: concept
topic_slug: kureksistant
status: draft
created: 2026-10-07
updated: 2026-10-08
tags:
  - wiki
  - kureksistant
  - audit
---

# Kureksistant — source contradictions and gaps

## Summary

The kureksistant sources disagree on licence, tool count, RAM, memory model, version and repo visibility. AGENTS.md looks inherited from an earlier "JARVIS" project. None of these were resolved; each needs a human decision or a repo fix.

## Details

| # | Topic | A | B | Evidence |
|---|-------|---|---|----------|
| 1 | Licence | README: "MIT © Alan Pfeifer (NODAYSIDLE)" | `LICENSE`: CC BY-NC 4.0, header "MARK 53 — JARVIS / Copyright (c) 2026 FatihMakes" | [[sources/index/src-20261007-c1c7fe9-kureksistant-readme]]; LICENSE read 2026-10-07 (agent check, not ingested) |
| 2 | Tool count | README / release notes: 20 (or "20+") | AGENTS.md: 17 | `actions/` has 28 modules (agent check) |
| 3 | RAM | README: ~55MB | AGENTS.md: ~60MB | [[sources/index/src-20261007-c1c7fe9-kureksistant-readme]], [[sources/index/src-20261007-459dbb7-kureksistant-agents]] |
| 4 | Memory model | README: Muse 3-tier markdown files in `~/` | AGENTS.md: `memory/kurek_history.json` + `long_term.json` + Hermes | [[sources/index/src-20261007-c1c7fe9-kureksistant-readme]], [[sources/index/src-20261007-459dbb7-kureksistant-agents]] |
| 5 | Paths | — | AGENTS.md links point to `/home/arch/Projects/JARVIS/` | [[sources/index/src-20261007-459dbb7-kureksistant-agents]] |
| 6 | Version | commit `9973462`: "v2.0" | release v0.1.0 | [[sources/index/src-20261007-2aa023e-kureksistant-git-log]], [[sources/index/src-20261007-46ff002-kureksistant-release-notes-v0-1-0]] |
| 7 | Visibility | user (10:03): private repo | GitHub API (2026-10-07 ~13:45 UTC+2): `"private": false, "visibility": "public"`, release publicly listed | [[_system/reference/github-org-repositories]] |
| 8 | Installer | commit `3c589e5`: "portable installer" | README: Arch/Hyprland first; needs mpv, grim, wl-clipboard | [[sources/index/src-20261007-2aa023e-kureksistant-git-log]], [[sources/index/src-20261007-c1c7fe9-kureksistant-readme]] |

## Gaps

- `docs/` contains only `demo.gif`. It is binary and was not ingested.
- There are no PRD, ARD, TRD or TASKS files.
- Release notes exist only in git-ignored `dist/`. They are not tracked in the repo.

## Related

- [[wiki/concepts/kureksistant-overview]]
- [[wiki/MOC/moc-nodaysidle-knowledge]]

## Open questions

- Which licence is intended, and is the FatihMakes / JARVIS attribution an upstream licence that must be kept?
- Is the repo meant to be private? It is currently public.

## Decisions (2026-10-07 13:45 UTC+2, user)

- **#1 Licence — resolved:** kureksistant is derived from FatihMakes' JARVIS, so **CC BY-NC 4.0** (the `LICENSE` file) is correct. The README line "MIT © Alan Pfeifer (NODAYSIDLE)" is wrong. The repo fix is proposed in session next actions and has not been applied.
- **#7 Visibility — resolved:** kureksistant **stays public**, which matches the GitHub API. The earlier "private" statement is withdrawn.

## Decisions and fixes (user, 2026-10-07 14:07 UTC+2; commit `99a7cec`, pushed)

- **#2 Tool count:** 28 is correct; the user added new tools, including jev. README and AGENTS.md now say 28.
- **#3–#5 AGENTS.md:** updated to match the README: ~55MB, Muse three-tier markdown memory (with `memory/kurek_history.json` kept for conversation context, which the code still uses), repo-relative links, no JARVIS paths.
- **#6 Version:** the release is v0.1.0. The old "v2.0" commit message stays (no history rewrite); the docs say v0.1.0.
- **#8 "Portable":** no "portable" wording was found in tracked docs; it appears only in commit `3c589e5`'s message, which is left alone.

## Audit findings and fixes (2026-10-08 03:32 UTC+2; PRs #2 and #3, merged)

Source: [[artifacts/kureksistant/audit-2026-10-08]] (read-only audit at `99a7cec`, grade C−). Earlier entries above are left as written.

| # | Topic | Claim | Measured / found | Status |
|---|-------|-------|------------------|--------|
| 3 | RAM | README / AGENTS.md: ~55MB | ~333MB RSS with faster-whisper loaded | **Fixed:** docs say ~333MB (PR #3, `52d009b`) |
| 2 | Tool count | README / AGENTS.md: 28 (user decision 2026-10-07) | 24 tools load at runtime; 3 `actions/` modules have no `TOOL` | **Fixed:** docs say 24 (PR #3, `52d009b`). This overrides the 28 decision above |
| 9 | OpenRouter | AGENTS.md: "never OpenRouter" | v0.1.0 tarball shipped `config/api_keys.json` with an OpenRouter key (plus Gemini) | **Release fixed:** re-cut without key files, new SHA-256 `a4085d73…1003`. The OpenRouter story itself is still undecided |
| 10 | Product identity | Docs: lean headless daemon | ~6.5k lines of JARVIS PyQt6 GUI shipped alongside; `setup.py` pointed to `main.py` | **Fixed:** GUI moved to `legacy/`, daemon is canonical (PR #2, `31d7e56`) |
| 11 | Installer | README: install script sets up the daemon | `install_linux.sh` misses `google-genai`, `PyYAML`, `send2trash`, `beautifulsoup4`, `typesafe_sdk`, Playwright browsers and apt `portaudio`/`python3-tk`/`mpv`/`grim` | **Open** (deferred by user) |
| 12 | Licence detection | `LICENSE` is CC BY-NC 4.0 | GitHub showed the licence as unrecognised | **Partly fixed:** SPDX header added (PR #2); GitHub may still show "Other" |
| 7 | Visibility | — | Repo is public (consistent with the 2026-10-07 decision) | No change |
