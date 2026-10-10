---
type: brief
topic_slug: "nodaysidle-browser-linux"
version: 1
status: closed-not-needed
review_status: pending
reviewer: ""
reviewed_at: ""
promoted: false
project_slug: ""
tags:
  - brief
  - nodaysidle-browser-linux
  - audit
---

> **Closed — not needed (2026-10-07 14:24 UTC+2).** The user reports that the browser was audited and fixed and works as intended. This is user-attested; no agent verified it. The brief is kept for history and was not executed. review_status stays pending.

# Brief: Finish the six partial audit findings in nodaysidle-browser-linux (A2–A4, A7–A9)

## Problem / opportunity

The `f5191ff` audit raised nine findings. At HEAD `2fffaab` (plus the docs fix `a46b2cd`), A1, A5 and A6 are fixed. Six are only partially addressed, including three rated High (A2, A3, A4). Each has a small, well-defined remainder. Closing them would let the browser state "audit complete" without a rewrite. [[wiki/concepts/nodaysidle-browser-linux-audit-status]]

## Recommendation

Run one hardening milestone of small, separately reviewable commits, one per finding, in severity order. Each commit adds a regression test where the audit's acceptance criteria allow it. No new features and no GTK 4 migration.

## Scope

- **In scope (remaining gap per finding):**
  - **A2 (High), packaging trust:**
    - checksum-verify an `appimagetool` found on PATH, or refuse it;
    - pin a versioned release URL instead of `continuous`.
  - **A3 (High), URL spoofing:**
    - handle labels written entirely in a lookalike script (e.g. all-Cyrillic) and labels mixing two non-Latin scripts;
    - choose a policy: a confusables check, or punycode for any non-ASCII host;
    - add adversarial tests.
  - **A4 (High), permissions:** after the prompt, recheck that the page is still the same document, not just the same origin; add a test.
  - **A7 (Medium), accessibility:**
    - measure real screen-reader (AT-SPI) output;
    - check that the close button is reachable by keyboard;
    - verify behaviour at 150% and 200% scaling and with larger fonts.
  - **A8 (Medium), narrow windows:**
    - run the history, find and menu surfaces at 360, 480 and 640 px;
    - decide whether to add a tab-overflow list.
  - **A9 (Low), quality gates:**
    - add CI (fmt, clippy, display-backed tests under Xvfb), now that `origin` exists;
    - optionally split `src/tabs.rs` (2,812 lines) into smaller modules without changing behaviour.
- **Out of scope:** A1, A5 and A6 (fixed), making the AppImage portable, new features (bookmarks, zoom, sync), and GTK 4 or WebKitGTK 6.

## Evidence

- Per-finding status with labels (observed, reproduced, inferred): [[wiki/concepts/nodaysidle-browser-linux-audit-status]]
- Original findings and acceptance criteria: [[sources/index/src-20261007-030f677-browser-linux-audit]]
- Packaging contract: [[sources/index/src-20261007-e79ab38-browser-linux-appimage]]
- Stability rules (don't hold RefCell borrows across GTK calls; keep the teardown tests): [[sources/index/src-20261007-6223dc7-browser-linux-agent-handoff]] (⚠️ marked unreliable; verify against the code)
- Quality gates passed on 2026-10-07: fmt, clippy and 65 tests (from the audit-status note).

## Risks & unknowns

- The remaining A3 and A4 gaps are *inferred* from reading the code. A3 has no confusables test case yet. A4 may be limited by the WebKitGTK API (no way to identify the requesting frame).
- A7 and A8 need a real Wayland/Hyprland session and a screen reader, which can't be done headless.
- A9 CI needs a hosted runner with WebKitGTK 4.1 and a display (Xvfb). Its cost and setup are not assessed.
- Refactoring `tabs.rs` risks breaking the re-entrancy rules; the GTK lifecycle test must keep passing.
- An updated `appimagetool` release URL changes its checksum, which needs a documented process for updating the pin.

## Suggested project shape (if promoted)

- Repo: https://github.com/nodaysidle/nodaysidle-browser-linux
- Milestones:
  1. A2 and A4: small security fixes, each with a test.
  2. A3: decide the URL-display policy, then add tests.
  3. A9: CI workflow. This lets later milestones run under CI.
  4. A7 and A8: manual native-desktop checks, then fixes.
  5. Optional: split `tabs.rs` into modules.
- Done when: every finding's original acceptance criteria are met or explicitly waived by a human, and the audit-status note shows all nine as fixed.

## Review checklist (human only)

Agents must not set `review_status: approved`.

- [ ] sources_cited
- [ ] claims_verified
- [ ] scope_clear

## Approval record

(Filled by human after review.)

## Decisions recorded (user, 2026-10-07 14:07 UTC+2)

- **A3:** keep the current lookalike-script policy (non-Latin hostnames allowed unless they look like spoofing). Scope narrows to closing its gaps (all-one-script lookalikes, two-non-Latin-script mixes); no "punycode for all non-ASCII" option.
- **A4:** the same-site recheck is accepted. **A4 is removed from scope**, so milestone 1 is A2 only.
- **AGENT-HANDOFF.md:** marked historical in the repo (`a124f2f`). Cite it only as background.
