---
type: source
source_id: "catalog-audit-2026-10-16"
title: "Catalog audit 2026-10-16 (macOS signing + README demo GIFs)"
author: SHIP
date: "2026-10-16"
source_commit: "f099e04"
source_note: "SHIP handoff commit f099e04; read-only audit of live public GitHub"
folded_by: ATLAS
folded: "2026-10-16 23:03 (EO 23:03, requested by Alan 23:00)"
tags: [source, audit, catalog, macos, readme]
---

# Catalog audit 2026-10-16 (SHIP, read-only)

Sources: live GitHub (unauthenticated: `users/nodaysidle/repos` API, `releases/latest` redirects, expanded_assets HTML, `git ls-remote`, raw README at HEAD). Signatures checked with rcodesign 0.29.0 on the box; DMGs extracted with 7zz 24.09.

## Index reconciliation

- Live public repos: **40** (38 own + 2 forks: hermes-agent, hermes-gpt). EO said 39.
- Vault index `wiki/sources/README.md`: 39 rows. The only repo missing from the index is **nodaysidle-knowledge**, which is public and is the vault itself (excluded on purpose). That explains 40 vs 39.
- Nothing is extra in the index; no renamed or private repos. All 39 pinned SHAs equal the live HEAD (synapse-notes de5e583 and cliprail d8ad7ba are already refreshed).

## (1) macOS apps

| Repo | Tag | Asset | sha256 | Signing class | Team ID | Notes |
|---|---|---|---|---|---|---|
| batchrename-pro | v0.1.0 | `BatchRename-Pro-0.1.0-aarch64.dmg` | `ef6e33a03881430c329fd9fd888cf4010142598010a89b535cf0eb2c3948309b` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| cliprail | v1.2.0-dmg.20260727 | `ClipRail-1.2.0.dmg` | `a83120148c67d7a33fb191ae2a373f237c80313b4e584471db29aae464115c0d` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| cursorpad | v1.0.0 | `CursorPad.dmg` | `9708d2e79857fe67f94f09b35eb68a5fa0fd4258f9d54fc29f8e69af6672a963` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| excalidays | v0.1.0 | `Excalidays-0.1.0.dmg` | `3754b52338f6c8262a794413d12c43a708b0a8dfe002d3d39156e764570f2d56` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none | universal (x86_64+arm64) |
| monospace-notes | v1.0.0 | `Monospace.Notes.dmg` | `dea6e2b794cd8be6f85a1ea0b588f6541dbf737c27620077ce6ba3f0dd82f1f9` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| nodaysidle-cascade-v3 | v3.1.0 | `NODAYSIDLE-Cascade-V3-3.1.0-aarch64.dmg` | `1aec1ffd45ce4dde171210a3ad1a0b195da0214316b2d1adb27e2657979ed3d9` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| nodaysidle-cistilka | v0.1.0 | `Cistilka-0.1.0.dmg` | `b6bf849952aa108f6bb8db5fb6135819fd33412817abaa9721a81fb571607608` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| nodaysidle-shareguard | v0.1.2 | `ShareGuard-0.1.0.dmg` | `590bd3e066ecd30fa998c38755647264affb571680de6b494055b620a84ce8fd` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none | v0.1.2 ships 0.1.0 build (parked) |
| nodaysidle-sonora | v0.1.1 | `Sonora_0.1.1_aarch64.dmg` | `85bb22139854ac444524fee4c76769c755cf86f01f991de43dd1d0cdcd559727` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none | ad-hoc **linker-signed only**: main binary has no sealed resources (no _CodeSignature/CodeResources) |
| nodaysidle-vois | v0.2.0 | `NODAYSIDLE-Voice-0.2.0.dmg` | `25b4536bbb11d8ba146737978eae8c225411b6ab7cd48c91d05d6f1ac938854b` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| nodaysrecording | v0.1.0 | `NoDaysRecord-0.1.0.dmg` | `5a7ffec30a99e7ec7bfb179726ff390b70c16b1972f95314ff1455ff9262182c` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| nodaystypst | v0.1.0 | `Nodaystypst-0.1.0-macOS-arm64.dmg` | `09423e04581fbb1659326c11ca4483cb636dddd06facac925605c639b643daed` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| pocket-drafts | v1.0 | `PocketDrafts-1.0-macos-universal.zip` | `4017e2f892f9311f37ddc104d4b37c8a86c6cdf556d9d2615bb352e2199c4cf7` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none | zip, universal |
| scribeflowpro | v1.0.0-dmg.20260727 | `ScribeFlowPro-1.0.0.dmg` | `291e82cb553f56e1ba1936dd8e464e088769951e6f74aa05788f7abfea949f86` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| small-count | v0.1.0 | `Small-Count-v0.1.0-macos.dmg` | `be9e50d7b0191623226f5f1f63ff765696d2a82bf908e399c7cdb5a464eaae6e` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| whisper-bar | v1.1.2 | `WhisperBar.dmg` | `7db0c6d57afac590615b02545ac3198e72754e10eeff587172158adb018b84da` | ad-hoc (CMS null, no Developer ID); container unsigned, no stapled ticket | none |  |
| BrewLedger | v2026.7.23 | no asset | — | no asset | — | README: native macOS app; latest release has no mac asset |
| nodaysidian | v0.1.1 | no asset | — | no asset | — | README: native macOS app; latest release has no mac asset |
| nodaysidle-browser | v2026.7.23 | no asset | — | no asset | — | README: native macOS browser; latest release has no mac asset |
| nodaysidle-cloudscribe | v0.1.1 | no asset | — | no asset | — | README: macOS dictation; latest release has no mac asset |
| nodaysidle-flowstate | v1.0.2 | no asset | — | no asset | — | README: platform macOS 14+; latest release has no mac asset |
| nodaysidle-lumiere | v0.1.1 | no asset | — | no asset | — | README: native macOS; latest release has no mac asset |
| nodaysidle-echocore-pro | NONE | no asset | — | no asset | — | README badge Linux | macOS; latest release has no mac asset |
| kureksistant | v0.2.1 | no asset | — | no asset | — | README: macOS menu-bar client in menubar/ (Linux assets only); latest release has no mac asset |

Signing evidence: for every app, `rcodesign print-signature-info` on the main executable shows `CodeSignatureFlags(ADHOC…)` with `cms: null`, so there is no certificate chain and no Team ID. No app has `Contents/CodeResources` (stapled notarization ticket). Every DMG shows `code_signature_size: 0, signature: null`, so none is signed or stapled. The pocket-drafts zip has no container signature.

## (2) README top-level demo (on HEAD)

| Repo | Type | HEAD SHA | Demo | Media | Line / first Install-type heading | HTTP | Frames |
|---|---|---|---|---|---|---|---|
| batchrename-pro | app | `bff7b4763f53478ce6b7c6309c5ae44fbec82216` | no | `src-tauri/icons/128x128.png` L2 200 PNG/1fr | — / L60 | — | — |
| BrewLedger | app | `0a0d5b430db6dc4da1a44ed58ffc41ffd5d84fad` | no | `.github/social-preview.png` L1 200 PNG/1fr | — / L39 | — | — |
| cliprail | app | `d8ad7badf1a55d6d05bc8662fb3a55e65fe85685` | no | `.github/social-preview.png` L1 200 PNG/1fr | — / L39 | — | — |
| cursorpad | app | `0347fbf41db21ef4cfbd8a82b763fc532b70ceca` | no | `Resources/AppIcon.png` L4 200 PNG/1fr | — / L160 | — | — |
| excalidays | app | `2e3a41a1e14822b52b1a0556890f374b7d67d029` | no | `Excalidays/Resources/Assets.xcassets/AppLogo.imageset/AppLogo.png` L2 200 PNG/1fr, `docs/screenshots/packaged-release-working.png` L28 200 PNG/1fr | — / Lnone | — | — |
| F1-nodaysidle | app | `f3ff0a5ce5cb57ad481b315ff48a1012cef0f2b5` | no | `docs/screenshots/lap-analysis.png` L28 200 PNG/1fr, `docs/screenshots/session-replay.png` L45 200 PNG/1fr | — / L68 | — | — |
| hermes-agent | fork | `80d16e3312069619ff973e1842afe6c5458146f4` | no | `.github/social-preview.png` L1 200 PNG/1fr, `assets/banner.png` L4 200 PNG/1fr | — / L36 | — | — |
| hermes-gpt | fork | `60762520bb4b5de478ecc19a5a9f22aee01131b1` | no | `assets/hermes-gpt-v0.5.0-two-way-codex-bridge.png` L6 200 PNG/1fr | — / Lnone | — | — |
| kureksistant | app | `09e3c7dd4a7b522448b78ccacd8745cb16c25f48` | no | `desktop/kurek.png` L2 200 PNG/1fr | — / L81 | — | — |
| markdown-helper | app | `6b6558a5726807315fb50aac5bb633c63ab13467` | no | no media | — / L48 | — | — |
| monospace-notes | app | `948471102e17086b366045b25757ec2fdca56e97` | no | `docs/AppIcon.png` L4 200 PNG/1fr, `docs/screenshots/editor.png` L20 200 PNG/1fr | — / Lnone | — | — |
| nodaysidian | app | `9baad48728b9c1e034204cdfdf9b8fd11ffb773a` | no | `.github/social-preview.png` L1 200 PNG/1fr | — / L38 | — | — |
| nodaysidle | profile README | `e7b9d2bc6b8cafcc36e87e18b992b793439bbafa` | no | `./assets/hero-dark.svg` L15 200 image/svg+xml, `./assets/stats-card-dark.svg` L192 200 image/svg+xml | — / Lnone | — | — |
| nodaysidle-apps | catalog hub | `6b9314673f26e3c94c11842380ee69db74e5d67d` | no | no media | — / Lnone | — | — |
| nodaysidle-browser | app | `93b0380077150cc6748137f9299b4f0a0b236a15` | no | `Assets/icon.svg` L2 200 image/svg+xml | — / L51 | — | — |
| nodaysidle-browser-linux | app | `7310f28817f088e1508752406c2328b751ada4c0` | **yes** | `docs/browser-linux.gif` | L6 / L51 | 200 | GIF/194fr |
| nodaysidle-cascade-v3 | app | `3edd3cc26c7535b95b17b988847df2b27932c0a1` | **yes** | `docs/cascade.gif` | L7 / L90 | 200 | GIF/137fr |
| nodaysidle-cistilka | app | `1f8196a1e8968ce15f33e580b013f59034da019c` | no | `assets/icon-1024.png` L2 200 PNG/1fr | — / L42 | — | — |
| nodaysidle-cloudscribe | app | `34934ae223762acb280cadd1f8775c1c7d45b80a` | no | `.github/social-preview.png` L1 200 PNG/1fr | — / L40 | — | — |
| nodaysidle-echocore-pro | app | `55949d8a4b484683dfe61935aa04842169d72750` | no | `assets/echocore-icon.svg` L2 200 image/svg+xml | — / L104 | — | — |
| nodaysidle-flowstate | app | `dd38c786ec5d9a67a46db2b6727d47bff979583f` | no | `.github/social-preview.png` L1 200 PNG/1fr | — / L48 | — | — |
| nodaysidle-knowledge | vault | `e9f67db59f828e9e1390f576203b317dec65c48d` | no | no media | — / Lnone | — | — |
| nodaysidle-lumiere | app | `642c21e82e146fc3a4db17bff7368517a44325cd` | no | `.github/social-preview.png` L1 200 PNG/1fr, `Lumiere/Resources/Brand/LumiereLogo.svg` L11 200 image/svg+xml | — / L46 | — | — |
| nodaysidle-project-pages | pages site | `8c7eb16d36bcdfaa6dfd2d95369c9de4ac85d746` | no | no media | — / Lnone | — | — |
| nodaysidle-prompt-optimizer | app | `7eacdfb318e773b64e116f45607d37f685f7e374` | no | no media | — / L94 | — | — |
| nodaysidle-shareguard | app | `43320299b1690ee5826006487425cf340020ca34` | **yes** | `docs/shareguard.gif` | L3 / L52 | 200 | GIF/144fr |
| nodaysidle-sonora | app | `f8b45ba8b1015b81577837968727958f7a6e0e97` | **yes** | `docs/sonora.gif` | L7 / L150 | 200 | GIF/163fr |
| nodaysidle-voice-anywhere-v2 | app | `9136ae1a1ac9b82cb116738f7adf601628e1d71b` | no | `.github/social-preview.png` L1 200 PNG/1fr | — / L101 | — | — |
| nodaysidle-vois | app | `1f637dbf0ff84d9b531c457b1de7579a24983bea` | no | `Assets/AppIcon.png` L2 200 PNG/1fr, `Artifacts/UI-Audit/01-control-center-dark.png` L25 200 PNG/1fr | — / L91 | — | — |
| nodaysrammar | app | `1de303bbd1f94ff7c8f9a65a5cf6ba80dcdaa4bc` | **yes** | `docs/media/nodaysrammar.gif` | L22 / L75 | 200 | GIF/156fr |
| nodaysrecording | app | `840610a45541adf95b931eb9ef9f22205ac3b655` | no | `Resources/NoDaysRecordIcon.svg` L2 200 image/svg+xml | — / L54 | — | — |
| nodaystypst | app | `336aa8c011830d876e914c9198a7f0a2edcd8fa8` | no | `Resources/AppIcon.png` L2 200 PNG/1fr | — / Lnone | — | — |
| openidle | app | `a623d5fcaae10d33cafdeaff2c2d6db80d4aaaec` | no | no media | — / L7 | — | — |
| pocket-drafts | app | `0edb61ed569d6ed8d0a5bd7a2ce7ed6ec64774e2` | no | `PocketDrafts/Assets.xcassets/AppIcon.appiconset/icon_512x512@2x.png` L2 200 PNG/1fr | — / L84 | — | — |
| Portfolio | portfolio site | `42a20c3b6ab0f2cd981053a2ffc4bc1f0623532a` | no | no media | — / Lnone | — | — |
| scribeflowpro | app | `f14bd55571bb9dd287a3ca2717a34ef2a891d73d` | no | `.github/social-preview.png` L1 200 PNG/1fr, `docs/20260228_053941.png` L11 200 PNG/1fr | — / L45 | — | — |
| skill-gallery | app | `e035a2e93f08e422f1f39ffe893613f900b56db0` | no | no media | — / L43 | — | — |
| small-count | app | `414942c04734e891e6d02c0638d18379037a7934` | no | `Resources/AppIcon.svg` L2 200 image/svg+xml, `Resources/SmallCount-Settings.png` L34 200 PNG/1fr | — / L77 | — | — |
| synapse-notes | app | `de5e5830458dd41f193f7069fcc6ea8e7e7ce6b7` | no | no media | — / L116 | — | — |
| whisper-bar | app | `2108144fc603ae605273d18f8f5b834918404437` | **yes** | `docs/whisperbar.gif` | L3 / L155 | 200 | GIF/144fr |

## Summary

- Total public repos: 40 (index 39 + vault). App repos: 33; non-app: 7 (2 forks, profile, hub, vault, pages, portfolio).
- macOS apps: 24. With an asset: 16, all **ad-hoc** (Developer ID + notarized 0; Developer ID not notarized 0; unsigned 0; UNKNOWN 0). No asset: 8.
- Demo on README (animated, before Install-type heading, HTTP 200): yes 6 (nodaysidle-browser-linux, nodaysidle-cascade-v3, nodaysidle-shareguard, nodaysidle-sonora, nodaysrammar, whisper-bar); no 27 of 33 app repos.
- Static screenshot or icon counts as no. SVG hero images were not frame-checked, because they are not GIF/video/APNG/WebP.
