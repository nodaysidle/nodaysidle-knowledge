# Agent handoff — nodaysidle-browser-linux

Last updated: 2026-10-03, after the audit fix series on top of `30f00b6` and the follow-up series on top
of `9a179f0` (VIGIL v3 items V-1…V-10).

This file describes the code as it is now, plus the rules that keep it stable. The history of the
earlier P0 bug ("search does not leave the Home UI") is gone: it was fixed long ago, and the old
notes described code that no longer exists.

## Project

| Item | Path / note |
|------|-------------|
| Linux port | `~/dev/nodaysidle/nodaysidle-browser-linux` |
| macOS reference | `~/dev/nodaysidle/nodaysidle-browser` (SwiftUI + WKWebView) |
| Binary | `~/.local/bin/nodaysidle-browser` |
| Desktop entry | `${XDG_DATA_HOME:-~/.local/share}/applications/com.nodaysidle.Browser.desktop` (tracked as `desktop/com.nodaysidle.Browser.desktop`; the installer only rewrites `Exec=`, unquoted unless the path needs quoting, because xdg-settings 1.2.1 cannot use a quoted `Exec=`). Older versions installed `nodaysidle-browser.desktop`; the installer moves mimeapps.list entries and the xdg-settings default browser to the new name and removes the old file (only if it generated it), see README "Upgrading" |
| Icon | `~/.local/share/icons/hicolor/scalable/apps/nodaysidle-browser.svg` (+ PNGs if `rsvg-convert` exists); also embedded in the binary |
| Profile data | `~/.local/share/nodaysidle-browser/` (`0700`): `webkit-data/` (cookies in `cookies.sqlite`, `0600`), `webkit-cache/`, `history.json` (`0600`). Without an absolute XDG data dir / HOME: `$TMPDIR/nodaysidle-browser-$USER` only if it is a real dir owned by the user and `0700` after chmod, else a fresh randomly named `0700` dir for the session, else the app exits (`profile::temp_data_dir`) |

**Stack:** Rust 2021 (MSRV 1.88, `rust-version` in `Cargo.toml`), GTK 3 through gtk-rs 0.18,
WebKitGTK 4.1 through the `webkit2gtk` 2.0 crate (feature `v2_40`). Single-threaded,
`Rc<RefCell<…>>` state.

**GTK 4 / WebKitGTK 6.0 (X-29):** the `webkit6` crate exists, but this project stays on GTK 3. The
`webkit2gtk` crate pins gtk-rs 0.18, so gtk/glib/gdk cannot be upgraded independently; moving on
means a GTK 4 UI rewrite. Not planned.

**Identity:** GApplication ID `com.nodaysidle.Browser`. `main()` sets the program name and (in
`startup`) the GDK program class to the same string, so the Wayland app_id, the X11 `WM_CLASS`, the
desktop file name and `StartupWMClass` all match (GTK 3 takes the app_id from the program name, not
from the application ID). Hyprland rules: `class:^(com\.nodaysidle\.Browser)$`.

## Architecture

```
ApplicationWindow (.browser-window)
└── VBox
    ├── tab bar: ScrolledWindow → tab strip HBox of pills (+ "new tab" button)
    │       pill = HBox [EventBox title (focusable, tooltip = title + URL)] [close Button]
    ├── toolbar: Home, Back, Forward, Reload/Stop, URL entry (security icon + progress),
    │            History (popover), Menu (☰: New Tab, Find in Page, Full Screen, About)
    ├── find bar (hidden until Ctrl+F)
    └── GtkStack, one child per tab
        └── per tab: GtkStack page_stack
            ├── "home" → home::build_home_surface() (nodaysidle + search pill)
            └── "web"  → WebView (created lazily on first navigation)
```

Modules:

- `src/main.rs`: application setup, identity, command-line argument resolution, `open` handler.
- `src/tabs.rs`: `TabManager` (tab lifecycle, toolbar, shortcuts, find bar, fullscreen, pop-ups,
  error pages, Home/Back/Forward, history wiring) plus a GTK regression test (`gtk_tests`).
- `src/navigation.rs`: address-bar and command-line input resolution (`resolve`), DuckDuckGo search.
- `src/home.rs`: Home surface.
- `src/history.rs`: `HistoryStore` (batched, atomic, private writes; corrupt files set aside).
- `src/downloads.rs`: save dialog, progress window, single cancel, close confirmation.
- `src/permissions.rs`: permission prompts and per-session decisions.
- `src/error_page.rs`: HTML for failed loads and crashed web processes.
- `src/profile.rs`: data directory, shared `WebContext`, sandbox, cookie storage.
- `src/icon.rs`: window/default icon (theme icon, else the embedded SVG).
- `src/theme.rs`: CSS. `theme::install()` must run in `connect_startup`, never before GTK init.

## Behaviour (what the code really does)

- **New tabs** show the built-in Home surface; no page loads until the user searches or types a URL.
- **Home button:** on a Home tab it focuses the search; on a page it navigates the tab to
  `about:blank#nodaysidle-home` and shows the Home surface, so Back returns to the page.
- **Last tab:** closing the last tab that shows a page opens a fresh Home tab first. A lone,
  untouched Home tab has no close button; Ctrl+W there just focuses its search. Close the window to
  quit.
- **Address bar** (`navigation::resolve`): `http`, `https`, `file`, `about` load as typed;
  `/path` and `~/path` open files; localhost, `*.localhost`, single-label `host:port` and local
  addresses (IPv4 loopback, 10/8, 172.16/12, 192.168/16, 169.254/16; IPv6 `::1`, fc00::/7, fe80::/10,
  and IPv4-mapped forms of the IPv4 ranges) get `http://`; IPv6 literals are bracketed; plausible
  domains get `https://`; everything else (including `node.js`, `notes.txt`, `javascript:` and
  `data:`) is a DuckDuckGo search.
- **Command line / external opens:** an existing file (or a `./`, `../` path) opens as a file,
  anything else goes through `resolve`. A second launch raises the existing window (`present()`).
- **Shortcuts** are handled in the main window's `key-press-event` before the focused widget (pages
  cannot swallow them): Ctrl+T; Ctrl+W / Ctrl+F4; Ctrl+Tab / Ctrl+Page Down / Ctrl+Shift+Page Down;
  Ctrl+Shift+Tab / Ctrl+Page Up; Ctrl+1…8, Ctrl+9; Ctrl+L / Alt+D / F6; Ctrl+F; Ctrl+R / F5;
  Alt+Left / Alt+Right; F11. GTK `AccelGroup` cannot carry Tab, which is why they are not
  accelerators.
- **Find in page** is a bar under the toolbar. It asks the *current* WebView for its
  `FindController` on every use and never stores it: a `WebKitFindController` only holds a raw,
  non-owning pointer to its view, and the old non-modal dialog crashed once its tab was closed.
- **Fullscreen:** WebKit's `enter-fullscreen` / `leave-fullscreen` handlers hide/restore the chrome
  and return `false` so WebKit keeps driving element fullscreen. F11 leaves element fullscreen;
  closing or switching away from the fullscreen tab ends it.
- **Pop-ups:** `create` returns a related view; `ready-to-show` decides where it goes. A
  `window.open` with an explicit size (not a link click, geometry different from the opener's)
  opens in its own transient window with a read-only address bar; everything else becomes a tab.
  `close` is handled from an idle callback. Pop-up windows share the tabs' error and crash pages
  (`wire_error_pages`) and have their own keys (`wire_popup_keys`): Ctrl+W / Ctrl+F4 close and
  Ctrl+R / F5 reload before the page sees the key; Esc closes only if the page did not handle it
  (connected after the default handler). They have no find bar, Back/Forward, editable address bar
  or history recording.
- **Tab teardown:** `close_tab` removes the entry under the `RefCell` borrow, then removes widgets
  and drops the entry outside it. Dropping the last reference to the tab's `page_stack` makes GTK 3
  dispose it, which emits `destroy`; a destroyed container destroys its children, so the WebView is
  disposed and WebKit closes the page even if a closure still holds a reference to the view. There
  is no explicit destroy call and no `unsafe` outside the tests (`gtk_tests` uses `unsafe` for
  `set_data` and `destroy`).
- **Downloads:** the save and progress dialogs are parented to the main browser window
  (`browser_window_for` follows `transient_for` up from the downloading view, else uses the
  application's window), so closing a pop-up does not destroy the progress window and cancel the
  download. Cancel calls `webkit_download_cancel` at most once (it is asynchronous and the download
  emits `failed` afterwards); the window stays open, shows "Cancelling…", then "Download cancelled"
  with a Close button. Closing the progress window while a download runs asks whether to cancel; a
  finished, failed or cancelled download's window closes freely. Closing the main browser window while
  downloads run also asks for confirmation; confirmed quits stop unfinished downloads.
- **Permissions:** location, camera, microphone, notifications and pointer lock show
  "<top-level origin> (or a site embedded in it) requests …" (WebKitGTK 4.1 does not expose the
  requesting frame's origin) and require Allow. Allow/Deny is remembered per origin and permission
  until the browser exits; unknown request types are denied.
- **Error pages:** failed loads (not cancellations or policy interruptions) and crashed/killed web
  processes show a dark built-in page with Try again / Reload. Error pages are not added to history.
- **Address bar extras:** lock / "Not secure" icon from the TLS state, a progress bar, and Reload
  turning into Stop while loading. The URL bar does not overwrite text while focused.
- **History:** recorded when a load finishes and written in batches: the first unsaved visit arms
  one 2 s timer (later visits join that batch), a failed write is retried after 5 s, doubling up to
  60 s, and the app flushes on exit and on termination signals (SIGTERM, SIGINT, SIGHUP). Writes go through a `0600` temp file + fsync + rename. An
  unreadable file is renamed to `history.json.corrupt-<time>` instead of being overwritten.
- **Cookies** persist in `webkit-data/cookies.sqlite` (created `0600`).

## Rules that keep it stable

- Never hold a `RefCell` borrow of `TabManager` state across anything that can re-enter
  `TabManager` or emit GTK signals (`select_tab_id`, widget removal/destroy, `load_uri`, dialogs,
  `grab_focus`…). Copy what you need out of the borrow first.
- `gtk_tests` in `tabs.rs` (needs a display: `DISPLAY=:0 cargo test --release`) realises a window,
  loads pages in three tabs with real WebViews, and closes tabs through their close buttons and
  `run_shortcut(CloseTab)`. It covers closing the tab being searched (R-1), a `window.open` tab
  (R-2), the last-tab rule (N-2), and checks that every closed WebView is finalized. It catches a
  borrow held across `select_tab_id` in `close_tab` and a leaked WebView reference (both checked
  by deliberately breaking the code). Without a display it prints "SKIPPED …" and passes;
  `NODAYSIDLE_REQUIRE_DISPLAY=1` turns the skip into a failure (use that in CI).
- Don't panic in GTK callbacks (an unwind across FFI aborts).
- Never store `FindController`, `WebView` pointers in dialogs, or other objects that can outlive a tab.
- Keep the custom tab strip (no `GtkNotebook`).

## Build / test / install

```bash
cd ~/dev/nodaysidle/nodaysidle-browser-linux
./scripts/validate.sh           # fmt, clippy -D warnings, release tests (NODAYSIDLE_REQUIRE_DISPLAY=1)
cargo build --release --locked
./scripts/install-desktop.sh    # builds --locked, installs binary, desktop file and icons
```

Dependencies (Arch): `gtk3`, `webkit2gtk-4.1`, `base-devel`; optional `librsvg` for PNG icons.

AppImage packaging is host-dependent (see `docs/APPIMAGE.md`). Menu → **Clear Browsing Data** erases history,
site storage, cache, and session permission denials. URL display uses `url_display` (spoof-resistant IDN/path
policy). Permission allows are per-request; only denials are remembered. Profile setup fails closed on
untrusted paths.

## Open items

- No git remote and therefore no CI. When the user asks, add `origin` and push; a CI job would run
  `cargo build --release`, `cargo test --release` (under Xvfb for the GTK test) and clippy.
- macOS parity still missing: bookmarks, zoom, settings, Secure Sync, tab drag-reorder.
- The pop-up placement rule is a heuristic based on what WebKitGTK 2.54 reports; check it against
  real sign-in flows.
- Pop-up windows lack find, Back/Forward and history recording (see Behaviour).
- Wayland (Hyprland) behaviour of the app_id/icon has only been reasoned from the GTK source, not
  tested live.
