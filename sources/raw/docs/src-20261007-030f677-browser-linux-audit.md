# nodaysidle Linux browser — audit and next-agent handoff

## Scope and baseline

Audit of the installed native Rust / GTK 3 / WebKitGTK browser and its repository at commit `f5191ff`. This is an audit, not a repair: application source, installation, and user profile were not intentionally changed. Runtime browsing checks used a separate temporary profile and a local HTTP fixture.

Installed executable: [nodaysidle-browser](</home/arch/.local/bin/nodaysidle-browser>). Its SHA-256 matches the existing [release executable](<target/release/nodaysidle-browser>): `75478a07808ed4ee979242efad87e24c0e8850eb8db56b86706fbe73899c7d52`. This ties the runtime observations to the local build artifact; it is not independent proof of reproducible compilation from HEAD.

### Verification results

- `cargo test --locked --offline --release`: **56 passed, 0 failed**, including the realized GTK / WebKit lifecycle test. Completed in 3.44 seconds.
- `cargo clippy --locked --offline --all-targets -- -D warnings`: **failed, exit 101**. Two lint errors: derivable Default implementation and menu-item type complexity.
- `cargo fmt --check`: **failed, exit 1**, formatting differences across multiple modules. No formatter changes applied.
- `ldd` of the installed executable resolves GTK, WebKitGTK, JavaScriptCore and many other libraries from the host. No missing dependency was reported on this machine.
- No configured git remote was returned; no GitHub workflow files were found. Do not create a remote or push without user authorization.

### Runtime method and limitations

The installed application ran through GTK Broadway at `http://127.0.0.1:8085/`; Chromium/CDP supplied mouse/text input and screenshots. A local server on port 8777 supplied deterministic pages. This tests real native GTK and WebKit flows, but not native Wayland compositing, GPU performance, AT-SPI screen-reader output, desktop scaling, or production keyboard input forwarding.

Confirmed working: local page navigation, long-title truncation, menu-driven Find, no-match feedback, many new tabs with active-tab reveal/overflow, `target="_blank"` opening a tab, and sized `window.open` opening a separate popup with a read-only address field.

**Do not report Ctrl+F or Ctrl+T as broken.** CDP/Broadway modifier injection was inconclusive; menu and button equivalents worked. Screenshots must specify the viewport each run: earlier captures unexpectedly became cropped when the override was omitted.

The runtime [application log](</tmp/ndi-audit/app.log>) reports a missing external GTK theme import and Broadway's unsupported OpenGL backend. These are environment limitations, not demonstrated application crashes or production GPU defects.

## Executive assessment

The small browser has a solid functional baseline and meaningful regression tests. Lazy WebView creation, sandbox enablement, escaped error pages, download cancellation state, find feedback, focus styling, and bounded visit recording are good foundations. No critical application failure was confirmed during this audit.

Prioritize release integrity and security-sensitive presentation/consent before cosmetic polish. High items below are source-confirmed risk mechanisms, not claims of a successfully exploited vulnerability.

## Prioritized findings and implementation plans

### A1 — High: AppImage is not self-contained as advertised

**Confirmed packaging defect.** [Packaging script:21–38](<scripts/package-appimage.sh#L21-L38>) copies the executable, launcher and icon, and builds an AppRun that adjusts PATH and XDG data directories. It does not bundle GTK/WebKit libraries, WebKit subprocess helpers, or their resource closure. The installed binary is dynamically linked to those system libraries. This contradicts the standalone/portable positioning in [README:36–47](<README.md#L36-L47>).

**Impact:** an AppImage can work on the developer's Arch machine yet fail on a clean distribution without matching WebKitGTK 4.1 and compatible ABI versions. Building an image is not a portability test.

**Next agent:** decide explicitly between a host-dependent AppImage (correct documentation and publish prerequisites) and a genuinely portable distribution. For portability, build on a defined compatibility baseline and bundle the supported runtime closure, including WebKit helper processes/resources; do not copy libraries blindly or disable the WebKit sandbox to make packaging work. Document how bundled WebKit security updates reach users.

**Acceptance:** exercise navigation, HTTPS, local files, downloads, media and sandboxed subprocess launch on a clean supported system that lacks developer packages. Record supported distributions/ABI baseline and dependency inventory. If host dependencies remain intentional, remove the standalone claim and verify a precise dependency installation procedure.

### A2 — High: packaging executes an unverified, mutable build tool

**Confirmed supply-chain risk.** [Packaging script:41–56](<scripts/package-appimage.sh#L41-L56>) accepts an executable at `/tmp/appimagetool`, or downloads the mutable `continuous` release, marks it executable, and executes it without checksum/signature verification. A pre-existing executable in the shared temporary namespace is trusted without provenance checks.

**Impact:** arbitrary code runs with the packaging user's privileges if the tool is replaced or the shared temporary path is planted. No compromise was demonstrated.

**Next agent:** remove implicit trust of the shared `/tmp` executable; pin a release and an independently maintained digest/signature policy; download into a private directory, verify before execution, and avoid leaving partially downloaded executables as reusable cached tools. Use `cargo build --release --locked` for release packaging and installation. Make externally supplied tools an explicit, documented trust choice.

**Acceptance:** valid pinned tool works; altered bytes fail before execution; a planted `/tmp/appimagetool` is ignored; interrupted downloads cannot become runnable cache entries; release dependency resolution is locked.

### A3 — High: URL display lacks a spoof-resistant Unicode policy

**Confirmed source risk; phishing exploit not exercised.** [URL display:170–182](<src/navigation.rs#L170-L182>) unconditionally converts punycode hosts to Unicode. [UTF-8 decoding:200–219](<src/navigation.rs#L200-L219>) accepts any decoded non-ASCII character not rejected by Rust's `is_control()`. Unicode formatting characters, including bidi controls, are not comprehensively covered by that check. [Fallback titles:237–255](<src/navigation.rs#L237-L255>) also decode IDNs.

**Impact:** mixed-script/confusable hostnames can resemble a trusted ASCII domain; percent-encoded bidi/default-ignorable characters can alter visual interpretation of the displayed URL. A valid HTTPS connection does not establish brand identity.

**Next agent:** keep canonical URI separate from display text. Use conservative punycode host display unless a reviewed script/confusable policy permits Unicode; retain encoded bidi/default-ignorable formatting characters. Apply the same policy to address fields, popup fields, tooltips and fallback titles. Replace hosts structurally, not via unrestricted substring search. Preserve legitimate international paths where safe.

**Acceptance:** unit tests cover valid international URLs, mixed-script IDNs, confusables, `%E2%80%AE` (U+202E), directional isolates, zero-width characters and escaped ASCII delimiters. Copying/reloading must preserve the canonical destination. Check rendered address bars with adversarial fixtures and ordinary multilingual URLs.

### A4 — High: permission consent is cached under an origin the request cannot authenticate

**Confirmed model limitation and risk.** [Permission handling:52–66](<src/permissions.rs#L52-L66>) states the WebKit permission request does not identify the requesting frame. Nevertheless it uses the current top-level view URI to look up an Allow/Deny decision and can automatically allow a later request. [Caching:92–100](<src/permissions.rs#L92-L100>) remembers that result for the session. The prompt discloses that an embedded site might be requesting, which is good, but does not make origin attribution reliable.

**Impact:** once access is granted on a top-level origin, another requester embedded in that origin can inherit consent when WebKit permits the underlying request. Different embedded origins are indistinguishable to this cache. A modal nested loop also deserves navigation/lifecycle checks before an asynchronous request is allowed. Actual exploitation depends on WebKit permission-policy enforcement and was not tested.

**Next agent:** do not cache positive consent across requests unless requester identity can be reliably established. Prefer explicit per-request consent when attribution is unavailable; consider retaining conservative denials only. Revalidate view/navigation lifecycle after the dialog and deny invalidated requests. Verify the exact WebKit API contract rather than assuming the top-level URI is the caller. Add revoke/reset controls if remembered grants are retained.

**Acceptance:** two distinct frame-origin fixtures under the same top-level page do not silently share an Allow decision; dismissed prompts deny; navigation or page teardown while a prompt is open cannot apply approval to a different document; unsupported requests remain denied. Test with actual media/location permissions and available devices or deterministic harnesses.

### A5 — Medium: profile privacy setup logs failures but continues persistent storage

**Confirmed fail-open behavior.** [Profile setup:14–35](<src/profile.rs#L14-L35>) logs failed directory restriction or cookie-file preparation, then still configures the persistent WebsiteDataManager and cookie storage at those paths. [Directory/file helpers:40–63](<src/profile.rs#L40-L63>) operate through ordinary filesystem paths; normal profile paths lack the explicit ownership/symlink trust checks used by the temporary fallback.

**Impact:** the application cannot guarantee its documented private-storage permissions when preparation fails. A readable but non-private existing directory may still be used; a symlink can cause permission changes or writes at an unintended target. This is a hardening issue, not a demonstrated cross-user leak on the audited profile.

**Next agent:** make setup return a Result and prevent persistent context creation until directories/files are validated. Choose a user-visible error or genuinely ephemeral safe fallback, never silent reuse of unsafe storage. Check ownership, file type and symlink policy before mutation; use race-resistant filesystem operations where the threat model requires them. Avoid chmod on arbitrary symlink targets.

**Acceptance:** non-writable, non-owned, symlinked and wrong-type profile paths are safely rejected or isolated; valid profiles preserve existing data and use 0700 directories / 0600 cookie storage; the failure mode is explained to the user and does not disable sandboxing.

### A6 — Medium: persistent data has no in-app deletion or permission-reset surface

**Confirmed product/privacy gap, not an undocumented telemetry claim.** [History store:38–95](<src/history.rs#L38-L95>) persists full URLs/titles. [History UI:967–1020](<src/tabs.rs#L967-L1020>) only lists and navigates entries. Cookies/site data persist through [profile setup](<src/profile.rs#L7-L38>). No clear-data, private-session, or permission-reset implementation was found in source.

**Impact:** users can accumulate sensitive history (including query strings) and site storage without an accessible way to erase it. Closing a tab or returning Home does not erase persisted browsing data. Session-only grants require a full browser restart to reset.

**Next agent:** add a small privacy action with explicit categories (history, cookies/site storage, cache, session grants) and confirmation appropriate to destructive scope. Clear both in-memory and on-disk history and coordinate save timers so erased history cannot be written back. Use WebKit's WebsiteDataManager APIs for site storage, not arbitrary live SQLite deletion. Document limitations; private mode is a separate product decision.

**Acceptance:** clear chosen categories, restart and verify they remain gone; pending history save cannot resurrect deleted entries; unselected categories survive; active pages receive sensible feedback and grant reset is effective.

### A7 — Medium: native accessibility semantics and readability need a focused pass

**Source-confirmed semantic omission; assistive-technology behavior not measured.** [Tab construction:316–374](<src/tabs.rs#L316-L374>) uses a focusable EventBox with custom key/click handlers rather than an explicit accessible tab role/selected state. Its icon-only close button has no explicit semantic label in this block and is intentionally excluded from Tab order. Source search found no explicit accessible-name/role wiring. Do not assume tooltips alone establish complete AT-SPI semantics.

**Observed visual concern:** [theme:28–60](<src/theme.rs#L28-L60>) fixes tab text at 11px and uses a very subtle selected background; close-icon color `#6b6b70` against selected `#202022` is approximately 3.05:1, leaving little margin for icon rendering and theme variations. This is not a blanket contrast-failure claim. The active text is noticeably brighter, a useful existing cue.

**Next agent:** inspect actual AT-SPI output with a native screen reader. Add descriptive names, tab role/selection/action semantics and contextual “Close [title]” labeling. Ensure close functionality is discoverable without requiring knowledge of Ctrl+W. Prefer a GTK tab/button primitive where it preserves the intended compact layout. Increase text scale or inherit user font sizing; strengthen active-tab indication without relying on color alone.

**Acceptance:** screen reader announces full title, role and selected state; all navigation/close actions are operable by keyboard/assistive technology; focus remains visible; 100%, 150% and 200% scaling, increased system font size, 640px tiling and tab overflow remain usable.

### A8 — Medium: narrow-window secondary surfaces need sizing and state policy

**Confirmed layout risk, not yet a reproduced native overflow defect.** [History popover:991–997](<src/tabs.rs#L991-L997>) requests at least 420×320 content pixels, unlike the deliberately shrinkable Home and Find surfaces. In a narrow tiled window this is a constraint that needs explicit testing.

**Observed UX recommendation:** Find stayed open with its previous query when a new Home tab was selected, displaying “No page to search.” That feedback is truthful; preserving the query may be intentional. The state is nevertheless distracting on an otherwise minimal new-tab surface. The many-tab horizontal scrollbar works, but hidden-tab discovery can be clearer.

**Next agent:** bound history geometry to available window/monitor space and include an empty-history message. Decide and document whether Find is per-window, per-tab, or automatically hidden on Home; do not accidentally erase query state. Consider a lightweight tab-list affordance for overflow rather than a full chrome redesign.

**Acceptance:** history/find/menu work at 360, 480 and 640 logical-pixel widths and with large fonts; no inaccessible offscreen actions; test switching between searched pages and Home, closing the searched tab, and 20+ tabs. Preserve selected-tab reveal and keyboard cycling.

### A9 — Low: quality gates and module boundaries need maintenance

**Confirmed tooling debt.** Strict Clippy fails at [SearchEngine Default:10–14](<src/navigation.rs#L10-L14>) and [menu item tuple:920](<src/tabs.rs#L920>). rustfmt check fails. [Tabs module](<src/tabs.rs>) spans 2,557 lines and combines lifecycle, popup policy, find, shortcuts, history UI, status UI and tests, increasing re-entrancy review burden.

**Next agent:** make a formatting/lint-only change first; derive Default and introduce a clear menu-item type. Add reproducible validation scripts/CI when an authorized repository host exists. Require display-backed testing with `NODAYSIDLE_REQUIRE_DISPLAY=1`; [GTK test:2438–2455](<src/tabs.rs#L2438-L2455>) otherwise returns successfully when no display is available. Later extract cohesive find, popup and chrome modules in separate behavior-preserving changes. Keep RefCell borrows short across GTK/WebKit calls and preserve lifecycle/finalization regression tests.

**Acceptance:** locked release tests, fmt check and strict Clippy pass on a documented toolchain; headless CI cannot silently skip the GTK test; no behavior change in formatting commit; extracted modules preserve tab teardown, find lifetime, WebKit-created views and active-tab reveal.

## UI/UX recommendations that are not confirmed defects

1. **Home input guidance:** the runtime Home screenshot showed a blank focused search field, but [Home source:27–34](<src/home.rs#L27-L34>) explicitly sets “Search DuckDuckGo or type a URL.” GTK can hide placeholder text on focus, so do not claim the placeholder is missing from code. Consider a persistent accessible label or subtle helper outside the entry. Verify it at native desktop scale before changing it.
2. **Theme consistency:** dark app chrome and light native menus/titlebar were observed. [Theme policy:4–9](<src/theme.rs#L4-L9>) intentionally leaves dialogs in system colors. Respect that native integration choice; do not globally dark-style file choosers or permission dialogs. A scoped app-menu treatment is optional polish, not a blocker. Repairing the user's missing external GTK theme is outside this repository audit.
3. **Roadmap:** zoom controls, bookmarks, reopen-closed-tab and drag reordering would improve everyday browsing. They are optional feature work, not release regressions. Do not start a GTK4 rewrite or synchronization backend as an audit fix.

## Evidence index

Temporary evidence may disappear after cleanup. Preserve useful captures to an agreed artifact location before relying on them in a future review.

- [Home screenshot](</tmp/ndi-audit/01-home.png>): sparse Home/focused blank entry.
- [Loaded local page](</tmp/ndi-audit/02-page.png>): address/title layout.
- [No-match Find](</tmp/ndi-audit/03b-find-none.png>): inline feedback.
- [Many tabs](</tmp/ndi-audit/04-many-tabs.png>): overflow and Find state on Home.
- [Application menu](</tmp/ndi-audit/05-menu.png>): native menu/theme mix.
- [New-tab link result](</tmp/ndi-audit/06-blank-tab.png>): successful target=_blank tab.
- [Sized popup](</tmp/ndi-audit/07-popup.png>): separate window behavior.
- [Test page fixture](</tmp/ndi-audit/site/index.html>), [CDP driver](</tmp/ndi-audit/cdp.mjs>), [runtime log](</tmp/ndi-audit/app.log>), [formatting log](</tmp/ndi-audit/rustfmt.log>).

## Next-agent execution order

1. Read this report and the existing [architecture/lifecycle handoff](<docs/AGENT-HANDOFF.md>). Reconfirm HEAD and installed/build artifact identity. Back up only a disposable test profile; never test destructive actions on the real user profile.
2. Reproduce A1/A2 and agree on distribution support; implement verified build tooling and honest packaging contract in a small isolated change.
3. Add adversarial tests for A3/A4/A5 before changing behavior; harden URL presentation, consent attribution and profile failure handling. Do not assume a working HTTPS icon prevents spoofing.
4. Implement A6 privacy controls, then A7 native accessibility and A8 responsive secondary surfaces. Keep functional changes and visual polish reviewable separately.
5. Finish A9 quality gates and optional module extraction. Do not refactor callback ownership casually: the existing GTK regression explicitly checks teardown/finalization.
6. Validate on real Wayland/Hyprland and X11: keyboard shortcuts while page fields are focused; 20+ tabs; narrow/HiDPI layout; AT-SPI; fullscreen; failed TLS/network loads; crash recovery; throttled concurrent downloads, cancellation, overwrite and quit; popup/OAuth flows; restart persistence and clearing. None of these untested dimensions should be marked passed from the Broadway screenshots alone.

### Suggested validation commands

```bash
cargo fmt --check
cargo clippy --locked --offline --all-targets -- -D warnings
NODAYSIDLE_REQUIRE_DISPLAY=1 cargo test --locked --offline --release
# For CI, execute the last command under a managed Xvfb display if no native display exists.
# Build/package validation should use --locked and a defined native-library baseline.
```

Full download completion/cancel/quit flows, permission devices/frame behavior, hostile-IDN rendering, clean-distribution AppImage execution, restart cookie persistence and performance profiling were not exercised by this audit. Dependency advisory scanning was not performed; successful local linking and unit tests do not establish an up-to-date security baseline.
