---
type: wiki-note
note_kind: concept
topic_slug: nodaysidle-browser-linux
status: draft
created: 2026-10-07
updated: 2026-10-07
tags:
  - wiki
  - nodaysidle-browser-linux
  - packaging
---

# nodaysidle-browser-linux — AppImage is host-dependent (not standalone)

## Summary

**Verdict: "host-dependent" is correct; "Standalone"/"Portable" in the v0.1.0 release notes is wrong.** The AppImage contains the binary, desktop metadata and icon only. GTK 3 and WebKitGTK 4.1 must already be installed on the host.

## Evidence

1. [[sources/index/src-20261007-e79ab38-browser-linux-appimage]] says it does **not** bundle GTK 3, WebKitGTK 4.1, JavaScriptCore, libsoup3 or the WebKit helper processes.
2. [[sources/index/src-20261007-2d7bab4-browser-linux-readme]]: "The AppImage bundles the browser binary and metadata only; GTK 3 and WebKitGTK 4.1 must already be installed."
3. [[sources/index/src-20261007-030f677-browser-linux-audit]] A1: the packaging script copies only the executable, launcher and icon, and the binary is dynamically linked to system libraries.
4. Reproduced 2026-10-07 at `2fffaab`:
   - `--appimage-extract` of `dist/nodaysidle-browser-x86_64.AppImage` yields exactly 6 files: `AppRun`, `usr/bin/nodaysidle-browser`, 2× `.desktop`, 2× `.svg`;
   - `scripts/package-appimage.sh` header: "Packages nodaysidle-browser into a host-dependent .AppImage".
5. Contradicting source: [[sources/index/src-20261007-1764cc7-browser-linux-release-notes-v0-1-0]] asset table ("Standalone Executable", "Portable Linux x86_64 AppImage"). Its own System Requirements section lists GTK 3 / WebKitGTK 4.1 libraries, so the notes contradict themselves.

## Side observation

The local `dist/` AppImage (built 2026-10-07 09:37 UTC+2) has SHA-256 `f6d82efa…4404`. That differs from the release-notes value `06a91e47…bd48`. This may just be a rebuild (inferred); the published GitHub asset has not been checked.

## Suggested repo fix (not applied; repo docs untouched)

- In `docs/RELEASE-NOTES-v0.1.0.md` (and the GitHub release body), change "Standalone Executable" / "Portable Linux x86_64 AppImage" to "Host-dependent Linux x86_64 AppImage (requires system GTK 3 + WebKitGTK 4.1)", and link `docs/APPIMAGE.md`.
- Re-verify the published asset's SHA-256 against the release notes.

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[wiki/concepts/nodaysidle-browser-linux-audit-status]] (A1)

## Update 2026-10-07 10:20 (UTC+2) — repo fix applied (local commit, not pushed)

- With your approval of session action 6, browser-repo commit `a46b2cd` (local; `master` is 1 ahead of `origin`) changes `docs/RELEASE-NOTES-v0.1.0.md`:
  - asset row is now "Host-dependent AppImage, requires system GTK 3 + WebKitGTK 4.1";
  - SHA-256 is now `f6d82efa6d7c972ff25f269f98457f0d5c99263a45c80162cfc9a085b20c4404`.
- **Checksums (reproduced):**
  - published GitHub v0.1.0 asset (downloaded with curl; the API `digest` agrees): `f6d82efa…4404`;
  - local `dist/`: `f6d82efa…4404`;
  - old release-notes value `06a91e47…bd48` matched **no** asset, so the notes were wrong. This resolves the "Side observation" above.
- No other repo file claimed standalone/portable. Only `agenthandoff_audit.md` mentions it, as a description of the defect; left unchanged.
- The GitHub release body already says GTK 3 + WebKitGTK 4.1 must be installed and has no "standalone" wording or checksum. `gh` is not authenticated, so it was not edited.
- Wording is now consistent everywhere in the repo once `a46b2cd` is pushed.
