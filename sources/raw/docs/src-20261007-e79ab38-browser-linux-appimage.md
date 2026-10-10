# AppImage packaging contract

The `.AppImage` produced by `scripts/package-appimage.sh` bundles the
`nodaysidle-browser` executable, launcher metadata, and icon. It does **not**
bundle GTK 3, WebKitGTK 4.1, JavaScriptCore, libsoup3, or WebKit helper
processes.

## Supported baseline

Treat the image as **host-dependent**: the target system must provide a
compatible WebKitGTK **4.1** stack (same major/minor family as the build host).
On Arch Linux and Omarchy this is typically:

```bash
sudo pacman -S --needed gtk3 webkit2gtk-4.1
```

Other distributions need equivalent packages (`webkit2gtk-4.1` / `libsoup-3.0`).
Building an AppImage on a developer machine is not a portability test; validate
on a clean system that only installs the documented dependencies.

## Security updates

WebKit security fixes reach users through their distribution (or manual
upgrades of system WebKitGTK packages), not through rebuilding this AppImage
alone.

## Build integrity

Release packaging uses `cargo build --release --locked`. The optional
`appimagetool` download is pinned by `scripts/appimagetool.sha256` and stored
under `target/appimagetool-cache/` (never trusted from `/tmp`).
