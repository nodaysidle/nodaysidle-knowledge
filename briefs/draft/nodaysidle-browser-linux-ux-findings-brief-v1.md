---
type: brief
topic_slug: "nodaysidle-browser-linux"
version: 1
status: draft
review_status: pending
reviewer: ""
reviewed_at: ""
promoted: false
project_slug: ""
tags:
  - brief
  - nodaysidle-browser-linux
  - ui
  - docs
---

# Brief: nodaysidle-browser-linux — version-badge docs fix (confirmed) + address-bar indicator/focus-loss candidate (static inference)

> **Recorded by ATLAS 2026-10-15 ~17:16 UTC.** This records findings raised by AGY and reported read-only by SHIP. **No app code was touched and nothing is authorised:** the UI item below is a *static code inference*, not a runtime reproduction, and must not be called a security vulnerability or a confirmed runtime bug. No implementation, commit, push or PR follows from this brief without a separate, explicitly agreed scope.

## Problem / opportunity

Two items sit at different levels of confidence, and the priority order matters:

1. **Confirmed, trivial, docs only.** The live `README.md` version badge says `0.1.0` while the project is v0.2.0 everywhere else (crate version, download links, release). One line, no code, no behaviour change.
2. **Substantive UI/UX candidate, unconfirmed.** The address bar appears to clear its HTTPS indicator (icon, tooltip and `secure`/`insecure` CSS) whenever its text changes while it has focus, and no focus-out path seems to restore it. An abandoned edit may therefore leave the user's draft URL and a blank indicator in place until some later load/status event or a tab switch. This is read from the code; it has **not** been reproduced at runtime.

## Recommendation

1. **Docs fix first and on its own:** correct `README.md:13` to the v0.2.0 badge (one line, docs-only PR). It is a pure docs correction with no behavioural risk and is safe to land independently of item 2.
2. **Do not implement the UI change yet.** Reproduce item 2 at runtime first, on a real GTK 3 + WebKitGTK 4.1 session: load an HTTPS page, click into the address bar, type a character, then move focus away without submitting, and observe whether the draft text and a blank indicator persist until the next load/status event or tab switch.
3. **Only if reproduced,** make the minimal fix: on focus loss, restore the selected WebView's committed URL display and re-apply the security indicator for the selected tab; optionally have Escape abandon the edit and do the same. Add a GTK integration regression test — the URI/TLS→security *classification* is already unit-tested (`:2140-2170`), but the widget wiring is not.
4. **Start from a clean tree.** Branch/worktree from live `master` (`ca1bc3e` at the time of writing). Never build on Alan's dirty local checkout at `a813e70` (20+ uncommitted entries; see [[sessions/LATEST]]).

## Scope

- **In scope (if and when a human approves execution):**
  - the one-line `README.md:13` badge correction (v0.1.0 → v0.2.0);
  - runtime reproduction of the address-bar indicator/focus-loss behaviour;
  - if it reproduces: restore URL display and security indicator on focus loss, optional Escape handling, plus a GTK integration regression test;
  - a clean worktree/branch off live `master` — not the owner's dirty checkout.
- **Out of scope:** any implementation at the time of this brief (none is authorised); the words "security vulnerability" or "security bug" as a label; any claim of a reproduced runtime bug; refactoring `src/tabs.rs`; CI setup; unreleased features; changes to the release, the AppImage or the GitHub Pages surfaces; committing or pushing anything without a separately agreed scope.

## Evidence

All line numbers below were read **first-hand by ATLAS on 2026-10-15 at ~17:16 UTC** against live `master` = `ca1bc3e` (committed 2026-10-15T00:29:24Z; `gh api repos/nodaysidle/nodaysidle-browser-linux/commits/master`) and against the `ca1bc3e` tree extracted from the GitHub tarball, unless a line is marked *(relayed)*.

- **Live state:** latest release **v0.2.0**, published 2026-10-14T06:04:20Z (`.../releases/latest`); `Cargo.toml:3` = `version = "0.2.0"`; `README.md:41` "What's new in v0.2.0"; `README.md:55` v0.2.0 AppImage download; `README.md:62` v0.2.0 SHA-256. `origin`-side README fetch: https://raw.githubusercontent.com/nodaysidle/nodaysidle-browser-linux/master/README.md
- **Confirmed docs defect — `README.md:13`:** the badge is `<img src=".../badge/version-0.1.0-..." alt="Version 0.1.0">`, so both the badge and its alt text read 0.1.0 on a repo whose crate and release are v0.2.0. Blob: https://github.com/nodaysidle/nodaysidle-browser-linux/blob/master/README.md#L13
- **The candidate, `src/tabs.rs:251-259`** — the address bar's only text-change handler:
  ```rust
  self.inner.borrow().url_entry.connect_changed(|entry| {
      if entry.is_focus() {
          entry.set_icon_from_icon_name(gtk::EntryIconPosition::Primary, None);
          entry.set_icon_tooltip_text(gtk::EntryIconPosition::Primary, None);
          let style = entry.style_context();
          style.remove_class("secure");
          style.remove_class("insecure");
      }
  });
  ```
  Blob: https://github.com/nodaysidle/nodaysidle-browser-linux/blob/master/src/tabs.rs#L251-L259
- **Precision (ATLAS):** this fires on a *text change while focused*, not on focus itself — merely clicking the address bar and leaving does not clear the indicator. The state needs an actual edit.
- **The one function that sets the indicator is `apply_page_status` (`src/tabs.rs:1332`)** and it is reached only from `:853`/`:859` (`select_tab_id`, i.e. tab switch), `:1228` (`show_home_surface`) and `:1327` (`sync_page_status`). `sync_page_status` (`:1317`) is itself called from `load_changed` (`:490`), a `notify::uri` handler (`:553`) and the `estimated-load-progress` / `is-loading` notifies (`:559`). **None of those is a focus-loss path.**
- **No focus-out restoration anywhere:** `grep -rn 'focus_out|focus-out|focus_in|connect_focus|Escape' src/` over the whole `ca1bc3e` tree returns only `src/home.rs:36`/`:40` (focus handlers for the *Home search* entry's pill styling), `src/popup.rs:100` (Escape closes a pop-up window) and `src/find.rs:99` (Escape hides the find bar). There is **no** focus-in/focus-out handler and **no** Escape handling for the address bar.
- **Draft text is preserved deliberately:** `sync_view_chrome` (`:1263`) sets the entry text through `url_bar_sync_value` (`:1455`, `(!is_focused).then_some(uri)`, used at `:1307`), so a focused entry is never overwritten. This is asserted by the unit test `uri_updates_preserve_text_while_the_url_bar_is_focused` (`:2229-2233`). Test coverage of the indicator is **partial, and ATLAS checked it precisely** (second pass, 17:18 UTC): the pure decision helper `security_state` (`:1389`) **is** unit-tested (`:2140-2170` — `Security::Secure` at `:2145`, `Insecure` at `:2149`/`:2154`/`:2158`, `None` at `:2151`/`:2162`/`:2166`/`:2168-2170`), i.e. the URI/TLS→security *classification* is covered; what has **no coverage at all** is the widget-facing side — `apply_page_status` (`:1332`) and the clear-on-edit at `:251-259`. No assertion touches the entry's icon, tooltip or `secure`/`insecure` class, and the repo has no `tests/` directory (all 20 `#[test]`s in `src/tabs.rs` are in-file in `mod tests`, `:1968`).
- **Claim-vs-behaviour link:** `README.md:32` advertises "Address bar with instant search / URL resolution, **real-time HTTPS indicator**, load progress, and decoded Unicode URLs", so a persistent blank indicator after an abandoned edit would sit against a documented promise — worth weighing, and worth checking at runtime before any wording changes.
- **Provenance:** the substantive item came to ATLAS as AGY's *static code inference* (relayed), independently read read-only by SHIP, both reaching the same code path; ATLAS's checks above are first-hand. Related vault pages: [[wiki/concepts/nodaysidle-browser-linux-overview]], [[wiki/concepts/nodaysidle-browser-linux-audit-status]], [[_system/templates/catalog/nodaysidle-browser-linux]], [[briefs/draft/readme-sweep-brief-v1]] (the batch-1 PR that produced `ca1bc3e`), [[briefs/draft/nodaysidle-browser-linux-audit-completion-brief-v1]] (closed-not-needed).

## Risks & unknowns

- **Not reproduced.** Everything about the focus-loss behaviour is inference from reading `ca1bc3e`. A runtime session may well show a restoration path this analysis missed (another callback, a GTK/Tab-cycling side effect, or a WebKit notify following the focus change), or may show the state is imperceptible in practice. Reproduce before believing it.
- **Not a security vulnerability.** The indicator goes *blank*; no secure lock is shown on an insecure page and no spoofed URL is presented — the text shown is the user's own draft. Do not label it a security issue in any handoff, post or issue.
- **The full effect of focus loss is unverified beyond `src/`.** The search was over the extracted `src/` tree at `ca1bc3e`; nothing in the repo's other directories restores the indicator, but a WebKit-side notify sequence was not exercised.
- **Two plausible fixes have different blast radii:** re-applying the indicator alone is small; also restoring/replacing the URL text touches the deliberate "don't overwrite a focused entry" rule asserted at `:2229` and needs care to keep that test meaningful.
- **Escape handling does not exist today** for the address bar, so adding it is a new behaviour, not a restoration — it should be a separate, explicitly approved decision.
- **Testing limit:** the repo's GTK tests need a display; a real Wayland/Hyprland session is needed for the reproduction, which cannot be done headless.

## Suggested project shape (if promoted)

- Repo: https://github.com/nodaysidle/nodaysidle-browser-linux
- Base: a clean branch/worktree from live `master` (`ca1bc3e`) — never `a813e70`.
- Milestones:
  1. Docs-only: `README.md:13` badge → v0.2.0 (can land alone).
  2. Runtime reproduction of the address-bar indicator/focus-loss behaviour, recorded with its environment; report observed vs inferred.
  3. If reproduced: minimal fix on focus loss (URL display + indicator), with a GTK integration regression test.
  4. Optional, separately approved: Escape abandons the edit.
- Done when: the badge reads v0.2.0 on `master`, and the behavioural item is either reproduced-and-fixed with a test, or explicitly waived by a human as not worth changing.

## Review checklist (human only)

Agents must not set `review_status: approved`.

- [ ] sources_cited
- [ ] claims_verified
- [ ] scope_clear

## Approval record

(Filled by human after review.)

- **No approval recorded.** No implementation, commit, push or PR is authorised by this brief. The UI item stays labelled **static inference, not runtime-confirmed** until someone reproduces it.

Agent: ATLAS
