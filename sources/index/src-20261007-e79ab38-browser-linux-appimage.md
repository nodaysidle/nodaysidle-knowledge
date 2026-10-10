---
type: source
source_id: "src-20261007-e79ab38"
retrieval_method: local-file
url: "https://github.com/nodaysidle/nodaysidle-browser-linux"
title: "AppImage packaging contract"
author: ""
published: ""
accessed: "2026-10-07"
status: active
supersedes: ""
superseded_by: ""
topic_slug: "nodaysidle-browser-linux"
original_path: "../nodaysidle-browser-linux/docs/APPIMAGE.md"
repo_head: "2fffaab"
tags:
  - source
  - primary
  - nodaysidle-browser-linux
  - packaging
---

# Source: AppImage packaging contract

## Metadata

- **Kind:** official-doc
- **Trust tier:** primary
- **Catalog:** [[_system/templates/catalog/nodaysidle-browser-linux]]

## Raw artifact

- File: `sources/raw/docs/src-20261007-e79ab38-browser-linux-appimage.md` (verbatim copy at repo HEAD `2fffaab`, 2026-10-07)

## Key excerpts

> Treat the image as **host-dependent**: the target system must provide a compatible WebKitGTK **4.1** stack

- Covers: what the AppImage bundles (binary, metadata, icon) vs. not (GTK 3, WebKitGTK, JSC, libsoup3, helpers); security updates arrive via the distro; `--locked` builds and sha256-pinned `appimagetool` cache.

## Used by wiki notes

- (none yet)
