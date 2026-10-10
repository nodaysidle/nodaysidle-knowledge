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
  - audit
---

# nodaysidle-browser-linux — audit A1–A9 status at HEAD

## Summary

The audit [[sources/index/src-20261007-030f677-browser-linux-audit]] was taken at `f5191ff`. On 2026-10-07 an agent re-checked each finding against HEAD `2fffaab` by reading code and running the quality gates. Result: 2 fixed (A5, A6), 7 partial (A1–A4, A7–A9), 0 fully open. **Update 10:20:** A1 → fixed via the audit's documented-host-dependency route (release notes corrected in local commit `a46b2cd`, not pushed). Now 3 fixed, 6 partial. No browser-repo files were changed (builds used `CARGO_TARGET_DIR=/tmp/ndi-check-target`).

**Evidence labels:** *reproduced* = ran a command and saw the result; *observed* = read the code/tests; *inferred* = reasoning, not checked.

## Quality gates (reproduced, rustc 1.98.1, 2026-10-07 ~10:05 UTC+2)

- `cargo fmt --check`: exit 0 (audit: failed)
- `cargo clippy --locked --offline --all-targets -- -D warnings`: exit 0 (audit: failed)
- `NODAYSIDLE_REQUIRE_DISPLAY=1 cargo test --locked --offline --release`: 65 passed, 0 failed (audit: 56 passed); the display was available, so the GTK test ran rather than skipping.

## Findings

| ID | Sev | Status | Evidence | What we found at `2fffaab` |
|----|-----|--------|----------|----------------------|
| A1 | High | fixed (docs; commit `a46b2cd`, pushed to origin/master 2026-10-07) | reproduced | The AppImage is still host-dependent. Extracting `dist/…AppImage` shows only `AppRun`, the binary, the `.desktop` file and icons; no GTK/WebKit libraries. That is now intentional and documented in README and `docs/APPIMAGE.md`, but the v0.1.0 release notes still say "Standalone"/"Portable". The audit's fallback acceptance (remove the standalone claim) is met everywhere except the release notes. See [[wiki/concepts/nodaysidle-browser-linux-appimage-packaging]]. |
| A2 | High | partial | observed | `scripts/package-appimage.sh`: `/tmp` is no longer trusted; the tool is cached in `target/appimagetool-cache/`; SHA-256 is pinned in `scripts/appimagetool.sha256`; `.partial` downloads are verified before `mv`; `cargo build --release --locked`. Remaining: (a) an `appimagetool` found on `PATH` is run **without** checksum (the script says so itself); (b) the URL is still the mutable `continuous` release, so the pin will fail closed when upstream changes (inferred). |
| A3 | High | partial | observed (tests reproduced) | New `src/url_display.rs`. It falls back to punycode for Latin+non-Latin mixed labels and keeps bidi, zero-width, soft-hyphen and BOM characters percent-encoded. Tests cover `%E2%80%AE`, ZWSP, mixed-script and delimiters. Gaps (inferred from the code): whole-script confusables (an all-Cyrillic lookalike label) still display as Unicode, and mixing two non-Latin scripts (e.g. Cyrillic+Greek) is not detected. There is no confusables table. |
| A4 | High | partial | observed | `src/permissions.rs`: Allows are **never cached** (only Denials, keyed by origin and permission); there is a default-Deny response; the origin is rechecked after the dialog and the request denied if it changed; unknown request types are denied. Residual: the recheck compares the top-level *origin*, not the document, so a same-origin navigation during the prompt still gets the Allow (inferred). The core consent-inheritance issue is fixed. |
| A5 | Medium | fixed | observed | `src/profile.rs`: `persistent_web_context` returns `Result` and rejects symlinked, wrong-type or foreign-owned directories and cookie files before WebKit setup. `main.rs` shows `show_fatal_profile_error` and stops on `Err`. Tests: `symlinked_profile_paths_are_rejected` and others. The sandbox stays on. |
| A6 | Medium | fixed | observed | `src/privacy.rs`: Clear Browsing Data dialog with history / cookies+site storage / cache / session denials, default Cancel. It uses WebsiteDataManager `clear`. `HistoryStore::clear` resets `save_pending` and flushes; test `cleared_history_stays_empty_after_reload`. Not checked at runtime across a restart. |
| A7 | Medium | partial | observed | `wire_tab_accessibility` in `src/tabs.rs` sets ATK `PageTab` role, name and `Selected` state, and gives the close button a `PushButton` role with a "Close …" label. Tab label size went from 11px to 12px (`theme.rs`). Not measured: actual AT-SPI output, scaling, contrast; the close-button keyboard reachability is unchanged (not verified). |
| A8 | Medium | partial | observed | History popover width is now derived from the window width, clamped to 260–420; height 200–480; empty-state "No pages in history yet." The find bar hides on switching to Home. Not done or checked: a tab-overflow list affordance, and runtime checks at 360/480/640 px. |
| A9 | Low | partial | reproduced | fmt, clippy and tests are green; `scripts/validate.sh` exists and uses `NODAYSIDLE_REQUIRE_DISPLAY=1`. Remaining: no CI (`.github/` is absent although the remote now exists); `src/tabs.rs` grew to 2,812 lines (audit: 2,557), with no module extraction. |

## Update log

- 2026-10-07 10:20 (UTC+2): A1 partial → fixed. The release notes no longer say Standalone/Portable, and the checksum was corrected to the published asset. Becomes public only after a push.
- 2026-10-07 13:39 (UTC+2): `a46b2cd` pushed by the user (`2fffaab..a46b2cd`). `git fetch` confirms `origin/master` = `a46b2cd`. A1 fix is public.

## Claims & citations

| Claim | Source |
|-------|--------|
| Original findings, baseline `f5191ff`, acceptance criteria | [[sources/index/src-20261007-030f677-browser-linux-audit]] |
| Commit `2fffaab` = "privacy, URL display, and packaging updates" | [[sources/index/src-20261007-e02f632-browser-linux-git-log]] |
| Host-dependent packaging contract | [[sources/index/src-20261007-e79ab38-browser-linux-appimage]] |
| "Standalone"/"Portable" wording | [[sources/index/src-20261007-1764cc7-browser-linux-release-notes-v0-1-0]] |
| Per-finding status | code at `2fffaab` + commands above (agent check 2026-10-07; not a source note) |

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[wiki/concepts/nodaysidle-browser-linux-overview]]
- [[wiki/concepts/nodaysidle-browser-linux-appimage-packaging]]

## Open questions

- Should A3 adopt a confusables / whole-script policy, or always show punycode for non-ASCII hosts?
- Should CI be added now that `origin` exists (A9)?

## Decisions (user, 2026-10-07 14:07 UTC+2)

- **AGENT-HANDOFF.md:** marked historical with a banner (commit `a124f2f`; push pending authentication).
- **A3, URL display:** policy accepted. Non-Latin hostnames are allowed unless they look like spoofing, keeping the current lookalike-script policy. The remaining gaps (all-one-script lookalikes, mixes of two non-Latin scripts) will be closed through the brief.
- **A4, permissions:** the same-site recheck after the prompt is **accepted as sufficient**. The browser works for the user. A4 is closed by decision; no document-level recheck is planned.

## User confirmation (2026-10-07 14:24 UTC+2)

- **Status:** the user says the browser was audited and fixed and works as intended. This is **user-attested; no agent verified it**. The partial findings A2–A9 recorded above were not re-checked.
- **Brief:** the audit-completion brief is closed as not needed (`status: closed-not-needed`; review_status stays pending).
