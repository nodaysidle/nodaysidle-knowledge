---
type: source-readme
repo: "nodaysidle/nodaysidle-browser-linux"
visibility: "public"
fork: false
default_branch: "master"
source_commit: "7310f28817f088e1508752406c2328b751ada4c0"
source_commit_date: "2026-10-16T17:36:06+02:00"
readme_path: "README.md"
readme_blob_sha: "a2d39b2982a36f90dc0f42e6db2c611966611947"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/nodaysidle-browser-linux/blob/7310f28817f088e1508752406c2328b751ada4c0/README.md"
tags: [source, readme, nodaysidle-browser-linux]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/nodaysidle-browser-linux` at `7310f28` (2026-10-16T17:36:06+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<div align="center">
  <img src="https://raw.githubusercontent.com/nodaysidle/nodaysidle-browser-linux/7310f28817f088e1508752406c2328b751ada4c0/assets/icon.svg" alt="nodaysidle app logo" width="132" height="132">

  # nodaysidle (Linux)

  ![NODAYSIDLE Browser for Linux](https://raw.githubusercontent.com/nodaysidle/nodaysidle-browser-linux/7310f28817f088e1508752406c2328b751ada4c0/docs/browser-linux.gif)

  **A quiet, native Linux browser for focused browsing.**

  Minimal chrome. Native WebKit pages. Local-first privacy.

  <p>
    <a href="https://github.com/nodaysidle/nodaysidle-browser-linux/releases"><img src="https://img.shields.io/badge/version-0.1.0-8e8e96?style=flat-square" alt="Version 0.1.0"></a>
    <a href="https://www.kernel.org/"><img src="https://img.shields.io/badge/Linux-x86__64-151518?style=flat-square&logo=linux&logoColor=white" alt="Linux x86_64"></a>
    <a href="https://www.rust-lang.org/"><img src="https://img.shields.io/badge/Rust-2021-DEA584?style=flat-square&logo=rust&logoColor=white" alt="Rust 2021"></a>
    <a href="https://webkitgtk.org/"><img src="https://img.shields.io/badge/WebKitGTK-4.1-1f5b82?style=flat-square&logo=webkit&logoColor=white" alt="WebKitGTK 4.1"></a>
    <img src="https://img.shields.io/badge/telemetry-none-4c8c6b?style=flat-square" alt="No telemetry">
  </p>
</div>

## What is nodaysidle?

`nodaysidle` is a Rust + GTK 3 browser shell that renders pages with the system's WebKitGTK 4.1. The ~1.5 MB AppImage contains only that shell (binary, desktop file, icon); the web engine and toolkit come from your distribution. It keeps the browser controls close at hand and lets websites own the page experience—without an Electron runtime, heavy JavaScript chrome layer, start-page clutter, or application telemetry.

The visual language is warm charcoal, silver, and quiet motion: a focused surface for everyday browsing that stays out of the way.

## Highlights

- Native GTK 3 browser chrome backed by WebKitGTK 4.1 (`libsoup3`)
- Built-in search-first Home screen on new tabs with DuckDuckGo resolution
- Multi-tab browsing with auto-scrolling active pills, minimum-width shrinking, and tab tooltips
- Address bar with instant search / URL resolution, real-time HTTPS indicator, load progress, and decoded Unicode URLs
- `Ctrl+F` in-page find bar with accurate match counts and narrow tiling support
- Safe tab lifecycle and sized pop-up windows (e.g. OAuth sign-in) with error and crash surfaces
- Downloads with folder chooser, progress dialog, cancel protection, and close confirmation
- Local-first persistence: bounded history (`0600`) flushed on exit/signals, and persistent cookies (`0600` SQLite)
- Desktop integration with Wayland `app_id` and X11 `WM_CLASS` (`com.nodaysidle.Browser`)
- Slim host-dependent `.AppImage` (~1.5 MB; requires system GTK 3 and WebKitGTK 4.1; see [docs/APPIMAGE.md](https://github.com/nodaysidle/nodaysidle-browser-linux/blob/7310f28817f088e1508752406c2328b751ada4c0/docs/APPIMAGE.md)). Fully bundled AppImage: in progress.
- No application telemetry

## What's new in v0.2.0

- **Multiple windows:** `nodaysidle-browser --new-window` (`-n`), <kbd>Ctrl</kbd>+<kbd>N</kbd>, or **New Window** in the ☰ menu. Windows share one profile (cookies, site storage, history), and only closing the last window asks to confirm active downloads.
- **Hyprland corners:** the window frame insets itself to match Hyprland's `decoration:rounding`, read once at startup. The inset is 0 when the window is tiled, maximized or fullscreen. Set `NODAYSIDLE_CORNER_INSET=<px>` to override it.
- **History popover:** sized to fit narrow tiles, with an empty state. The find bar hides on Home and keeps its query.
- **Accessibility:** tabs are exposed as page tabs with names and selected state, close buttons are labelled "Close <title>", and the close icon has higher contrast (about 6:1).
- **Fish completion and desktop action:** the installer adds a fish completion and a **New Window** desktop action.
- **Hardening:** one shared URL display, with lookalike (mixed-script) hostnames kept in punycode and bidi or zero-width characters escaped. Clear Data now reports failures in a dialog.
- **AppImage packaging:** the pinned `appimagetool` download is checksum-verified before use, with offline regression tests (`scripts/test-package-appimage.py`).

## Install and run

### Download `.AppImage`

Download the [v0.2.0 AppImage](https://github.com/nodaysidle/nodaysidle-browser-linux/releases/download/v0.2.0/nodaysidle-browser-x86_64.AppImage) (previous: [v0.1.0 AppImage](https://github.com/nodaysidle/nodaysidle-browser-linux/releases/download/v0.1.0/nodaysidle-browser-x86_64.AppImage); or [see all releases](https://github.com/nodaysidle/nodaysidle-browser-linux/releases)). The AppImage bundles the browser binary and metadata only; **GTK 3 and WebKitGTK 4.1 must already be installed** on the system (see [docs/APPIMAGE.md](https://github.com/nodaysidle/nodaysidle-browser-linux/blob/7310f28817f088e1508752406c2328b751ada4c0/docs/APPIMAGE.md)):

```bash
chmod +x nodaysidle-browser-x86_64.AppImage
./nodaysidle-browser-x86_64.AppImage
```

SHA-256 (v0.2.0 AppImage): `02d7a85c3d99f5e395425722c57c46d12fabceccd063554b7f01c2b43229ad93` ([SHA256SUMS](https://github.com/nodaysidle/nodaysidle-browser-linux/releases/download/v0.2.0/SHA256SUMS)). Verify with `sha256sum -c SHA256SUMS` in the download folder.

Size: 1,530,360 bytes (~1.5 MB). This is the Rust + GTK shell only, not a self-contained browser. Runtime dependencies that must come from the system:

- WebKitGTK 4.1 (`libwebkit2gtk-4.1`, with `libjavascriptcoregtk-4.1` and `libsoup-3.0`)
- GTK 3 (`libgtk-3`, with GLib/GIO, Pango, Cairo, GDK-Pixbuf)

A fully bundled AppImage that includes GTK 3 and WebKitGTK 4.1 is in progress.

### Build `.AppImage` locally

```bash
./scripts/package-appimage.sh
# Outputs: dist/nodaysidle-browser-x86_64.AppImage
```

### Requirements (Arch / Omarchy)

```bash
sudo pacman -S --needed gtk3 webkit2gtk-4.1 base-devel
```

Requires Rust **1.88** or newer (`rust-version` in `Cargo.toml`).

### Run from source

```bash
git clone https://github.com/nodaysidle/nodaysidle-browser-linux.git
cd nodaysidle-browser-linux
cargo run --release
cargo test --release   # GTK tests run when a display is available
```

### Install launcher + icon

```bash
./scripts/install-desktop.sh
```

This builds a release binary and installs:
- `~/.local/bin/nodaysidle-browser`
- `${XDG_DATA_HOME:-~/.local/share}/applications/com.nodaysidle.Browser.desktop` (quoted only when path characters require it)
- `${XDG_DATA_HOME:-~/.local/share}/icons/hicolor/scalable/apps/nodaysidle-browser.svg` (plus 48/128/256 px PNGs when `rsvg-convert` is available)
- `${XDG_CONFIG_HOME:-~/.config}/fish/completions/nodaysidle-browser.fish`

The launcher name matches the application ID `com.nodaysidle.Browser`, so Hyprland window rules match `class:^(com\.nodaysidle\.Browser)$`.

#### Upgrading from `nodaysidle-browser.desktop`

Versions before the rename installed `nodaysidle-browser.desktop`. Running `./scripts/install-desktop.sh`:
- Migrates `nodaysidle-browser.desktop` entries in `mimeapps.list` files to `com.nodaysidle.Browser.desktop`.
- Updates `xdg-settings set default-web-browser com.nodaysidle.Browser.desktop` if the old name was previously default.
- Removes the old generated launcher.

## Keyboard shortcuts

| Action | Shortcut |
| --- | --- |
| New tab | <kbd>Ctrl</kbd>+<kbd>T</kbd> |
| New window | <kbd>Ctrl</kbd>+<kbd>N</kbd> |
| Close tab | <kbd>Ctrl</kbd>+<kbd>W</kbd>, <kbd>Ctrl</kbd>+<kbd>F4</kbd> |
| Next tab | <kbd>Ctrl</kbd>+<kbd>Tab</kbd>, <kbd>Ctrl</kbd>+<kbd>Page Down</kbd>, <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Page Down</kbd> |
| Previous tab | <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Tab</kbd>, <kbd>Ctrl</kbd>+<kbd>Page Up</kbd> |
| Select tab | <kbd>Ctrl</kbd>+<kbd>1</kbd>–<kbd>Ctrl</kbd>+<kbd>8</kbd>, <kbd>Ctrl</kbd>+<kbd>9</kbd> |
| Focus address bar | <kbd>Ctrl</kbd>+<kbd>L</kbd>, <kbd>Alt</kbd>+<kbd>D</kbd>, <kbd>F6</kbd> |
| Reload / stop | <kbd>Ctrl</kbd>+<kbd>R</kbd>, <kbd>F5</kbd> |
| Find in page | <kbd>Ctrl</kbd>+<kbd>F</kbd> |
| Navigate back / forward | <kbd>Alt</kbd>+<kbd>Left</kbd> / <kbd>Alt</kbd>+<kbd>Right</kbd> |
| Full screen | <kbd>F11</kbd> |

In the main window, shortcuts work wherever the focus is, including inside web pages. Tab titles can be reached with Tab and activated with Enter or Space.

## Pop-up windows

A pop-up window shows one page and a read-only address bar. It has:
- <kbd>Ctrl</kbd>+<kbd>W</kbd> or <kbd>Ctrl</kbd>+<kbd>F4</kbd> to close it, <kbd>Ctrl</kbd>+<kbd>R</kbd> or <kbd>F5</kbd> to reload, and <kbd>Esc</kbd> to close it unless the page handles the key itself.
- <kbd>Ctrl</kbd>+<kbd>L</kbd>, <kbd>Alt</kbd>+<kbd>D</kbd>, or <kbd>F6</kbd> to select the read-only address for copying with <kbd>Ctrl</kbd>+<kbd>C</kbd>; Tab can also focus it.
- Built-in dark error pages for failed loads and web process recovery.
- Pop-ups lack find, back/forward history, and editable address bar, and close with the parent window.

## Clearing browsing data

The app menu lets you clear history, cookies and site storage, cached files, and
session permission denials independently. A failure dialog reports unsuccessful
selected operations, including website-data failures reported asynchronously by
WebKit. Successfully cleared categories remain cleared when another category fails.

## Address bar input

URL presentation is shared by the address bar, popup addresses, tab URL tooltips,
fallback host titles, history rows, and error pages. Approved accented Latin labels (for example,
`bücher.de` and `café.fr`) and Han-only labels (`例子.测试`) display as Unicode.
Other international hosts remain in punycode, including Cyrillic and Greek names
that may resemble Latin names. Paths may display readable Unicode, while encoded
delimiters, bidi controls, and zero-width characters remain escaped. Stored history
URLs and navigation destinations stay canonical; submitting an unchanged displayed
address reuses the current URI.

- `http://`, `https://`, `file://` and `about:` URLs load as typed.
- `/absolute/path` and `~/path` open local files.
- `localhost`, `*.localhost`, a single-label `host:port`, and local addresses use `http://`: loopback, private IPv4 (`10/8`, `172.16/12`, `192.168/16`), link-local IPv4 (`169.254/16`), IPv6 loopback, unique local (`fc00::/7`) and link-local (`fe80::/10`) addresses. IPv6 literals such as `::1` are bracketed.
- Other input that looks like a domain (`example.com`, `en.wikipedia.org/wiki/Rust`) gets `https://`.
- Everything else is searched with DuckDuckGo, including text with spaces, file names such as `node.js` or `notes.txt`, numbers such as `3.14`, and `javascript:` / `data:` URLs.

## Command line

```bash
nodaysidle-browser [URL-or-file …]
nodaysidle-browser --new-window [URL-or-file …]   # -n
```

An argument naming an existing file (or starting with `./` or `../`) opens that file; anything else is resolved like address-bar input (e.g. `nodaysidle-browser wikipedia.org` opens `https://wikipedia.org`). Running the command again reuses the existing window unless `--new-window` (`-n`) is given, which opens a new window on the current workspace sharing the same profile (cookies, site storage and history). <kbd>Ctrl</kbd>+<kbd>N</kbd> and the ☰ menu's **New Window** do the same in-app.

## Privacy model

- No analytics, telemetry, or application-owned browsing backend.
- Website cookies persist locally in `~/.local/share/nodaysidle-browser/webkit-data/cookies.sqlite` (`0600`).
- Local browsing history is stored in `~/.local/share/nodaysidle-browser/history.json` (`0600`) and flushed atomically on exit or signals (`SIGTERM`, `SIGINT`, `SIGHUP`). Use **Menu → Clear Browsing Data** to erase history, site storage, cache, or remembered permission denials.
- Web content runs in WebKitGTK's own sandboxed web process; the app does not disable it.
- Site requests for location, camera, microphone, notifications, and pointer lock require explicit user permission.

## Related

- macOS app: [nodaysidle-browser](https://github.com/nodaysidle/nodaysidle-browser) (SwiftUI + WKWebView)
