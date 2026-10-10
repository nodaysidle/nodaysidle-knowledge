# nodaysidle-browser (Linux) v0.1.0

A quiet, native Linux WebKit browser designed for focused browsing.

## Assets

| File | Type | Description |
| --- | --- | --- |
| **`nodaysidle-browser-x86_64.AppImage`** | Standalone Executable | Portable Linux x86_64 AppImage |

### Verification
```bash
sha256sum nodaysidle-browser-x86_64.AppImage
# 06a91e470c0ed8b592341d09557bb0c7190858f3928a4807d778ec696dcabd48
```

## Quick Start

Download the `.AppImage`, make it executable, and run:

```bash
chmod +x nodaysidle-browser-x86_64.AppImage
./nodaysidle-browser-x86_64.AppImage
```

To install the desktop launcher, binary, and icons permanently for your user:
```bash
git clone https://github.com/nodaysidle/nodaysidle-browser-linux.git
cd nodaysidle-browser-linux
./scripts/install-desktop.sh
```

---

## What's New in v0.1.0

### Browsing & Chrome
- **Custom Tab Strip**: Smooth tab strip with active tab auto-scrolling, minimum-width shrinking, and tab tooltips showing the full title and URL.
- **Search-First Home**: Built-in dark home surface with DuckDuckGo search. Home tabs consume zero web process resources until a page loads.
- **Address Bar**:
  - Automatically resolves hostnames, localhost, IP addresses, file paths, and searches.
  - Human-readable Unicode URLs for internationalized domain names (IDN punycode) and non-English paths/queries (CJK, Cyrillic, accented Latin).
  - Real-time HTTPS security indicator and progress bar; security icon clears immediately while editing.
- **Find in Page (`Ctrl+F`)**: Non-blocking in-window find bar with accurate match counts that persist across match stepping, auto-clears on tab switch, and supports narrow window tiling.

### Stability & Lifecycle
- **Window Teardown & Navigation**:
  - Safe tab closure with complete WebView disposal and no re-entrancy panics.
  - Sized `window.open` pop-ups (e.g. OAuth sign-in) open in dedicated transient pop-up windows with custom close keys (`Ctrl+W`, `Esc`) and built-in error/crash handling.
  - HTML5 video and element fullscreen support, plus `F11` window fullscreen.

### Downloads & Data Management
- **Downloads with Close Confirmation**:
  - Destination file chooser and dedicated progress window parented to the browser window.
  - Safe single-flight cancellation.
  - Closing the browser window during active downloads prompts for confirmation before cancelling.
- **Atomic Local History**:
  - Saved to `~/.local/share/nodaysidle-browser/history.json` with strict `0600` permissions.
  - Batched writes with retry backoff.
  - Flushed synchronously on exit and on termination signals (`SIGTERM`, `SIGINT`, `SIGHUP`).
- **Persistent Cookies**:
  - WebKit cookie database saved to `~/.local/share/nodaysidle-browser/webkit-data/cookies.sqlite` (`0600`).
- **Idempotent Desktop Integration**:
  - Installs launcher as `com.nodaysidle.Browser.desktop` matching the Wayland `app_id` and X11 `WM_CLASS` (Hyprland / GNOME / KDE dock integration).
  - Automatically migrates existing default browser settings cleanly and idempotently.

---

## System Requirements

- **Architecture:** `x86_64` Linux
- **Libraries:** GTK 3 (`libgtk-3.so.0`), WebKitGTK 4.1 (`libwebkit2gtk-4.1.so.0`)
