---
type: artifact
artifact_kind: catalog-sweep
source: SWEEP weekly sweep (box /workspace/sweep-reports/2026-10-11-sunday-catalog-sweep.md)
created: 2026-10-11
updated: 2026-10-11
recorded_by: ATLAS
---

# SWEEP weekly catalog — Sunday 2026-10-11 ~18:17 CEST

**Main finding:** Three Oct 8 SHIP gaps are fixed (whisper-bar install, shareguard install, sonora notes). ShareGuard and browser-linux remain missing from the portfolio (unchanged). New gaps: nodaysrammar and kureksistant shipped on the apps site but absent from the portfolio; portfolio entry NODAYSIDLE Browser (macOS `nodaysidle-browser`) has no downloadable release asset and no demo GIF; synapse-notes has no demo GIF.

Canonical portfolio: https://nodaysidle-portfolio-nine.vercel.app (200 OK). Ignored stale showcases. Apps site (context): https://nodaysidle-apps.vercel.app (200 OK) lists Cascade, Sonora, WhisperBar, Browser for Linux, nodaysrammar, Kurek.

Wiki note: user machine `arch` (78b9b106…) was disconnected — could not write Obsidian LLM wiki this run.

---

## 1. Scope

| Metric | Count |
| --- | ---: |
| Repos listed (`user:nodaysidle` search) | 48 (mix public/private) |
| Treated as catalog apps this pass (portfolio ∪ apps site ∪ prior-tracked ShareGuard) | 9 |
| Other public repos with a latest release + ≥1 asset (out of curated catalog; not full 7-check) | ~15 (e.g. monospace-notes, cursorpad, cliprail, scribeflowpro, …) |
| Portfolio apps found | 5: Cascade, WhisperBar, Sonora, Synapse Notes, NODAYSIDLE Browser |
| Apps-site apps | 6: Cascade, Sonora, WhisperBar, Browser for Linux, nodaysrammar, Kurek |

**Visibility notes:** All 9 catalog apps are **public**. Oct 8 already recorded cascade-v3 / sonora / kureksistant public flips. synapse-notes is public now (Oct 7 memory had it private; not in Oct 8 “became public” list — noted as context, not re-routed).

---

## 2. Per-app status (catalog set)

Legend: Y=yes, N=no, P=partial. Install+link means Install/Getting Started section links the **current release asset URL** (not only `/releases` index).

| repo | public? | latest tag | notes OK? | asset? | README install+link? | GIF OK? | on portfolio? | live URL OK? |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| nodaysidle-cascade-v3 | Y | v3.1.0 | Y | Y (4) | Y (DMG + Linux assets) | Y `docs/cascade.gif` 200 | Y | n/a (no product homepage; GH/portfolio OK) |
| whisper-bar | Y | v1.1.2 | Y | Y (1 DMG) | Y → WhisperBar.dmg | Y `docs/whisperbar.gif` 200 | Y | n/a |
| nodaysidle-sonora | Y | v0.1.1 | Y | Y (5) | Y → DMG + AppImage | Y `docs/sonora.gif` 200 | Y | n/a |
| synapse-notes | Y | v0.4.3 | Y | Y (debug APK) | Y → APK URL | **N** (no GIF in README/docs) | Y | n/a |
| nodaysidle-browser | Y | v2026.7.23 | **N** (theme-only) | **N** (0 assets) | **N** (source build only) | **N** | Y (as NODAYSIDLE Browser / Swift) | n/a |
| nodaysidle-browser-linux | Y | v0.1.0 | Y | Y (AppImage) | **P** (Install exists; links `/releases` + filename, not asset URL) | Y `docs/browser-linux.gif` 200 | **N** | n/a |
| nodaysidle-shareguard | Y | v0.1.2 | Y | Y (DMG + sha256) | Y → ShareGuard-0.1.0.dmg on v0.1.2 | Y `docs/shareguard.gif` 200 | **N** | n/a |
| nodaysrammar | Y | v1.0.1 | Y | Y (zip + sha256) | Y (Install + Releases; versioned zip pattern) | Y `docs/media/nodaysrammar.gif` 200 | **N** | apps homepage 200 |
| kureksistant | Y | v0.2.0 | Y | Y (tar.gz + SUMS) | Y → v0.2.0 tarball URL | Y `docs/demo.gif` 200 | **N** | GH homepage 200 |

Portfolio “NODAYSIDLE Browser” copy is Swift/WebKit → **macOS `nodaysidle-browser`**, not `nodaysidle-browser-linux`.

---

## 3. NEW findings only (route)

1. **nodaysrammar** — shipped v1.0.1 (2026-10-09), on apps site, **not on portfolio**. → **ATLAS**
2. **kureksistant** — shipped v0.2.0 (2026-10-10), on apps site, **not on portfolio**. → **ATLAS**
3. **nodaysidle-browser** — on portfolio but latest release has **0 downloadable assets**; body is theme-alignment only; README install is source-only. → **SHIP** (+ status change **ATLAS**)
4. **nodaysidle-browser** — **no demo GIF** in README. → **REEL**
5. **synapse-notes** — on portfolio; README/docs have **no demo GIF** (docs has AGENTS/README/plans only). → **REEL**
6. **nodaysidle-browser-linux** — Install links releases index, not `.../download/v0.1.0/nodaysidle-browser-x86_64.AppImage` (filename only in chmod). Mild gap, not in Oct 8 SHIP list. → **SHIP** (optional / low priority)

---

## 4. Previously known UNCHANGED (do NOT re-route)

- **ATLAS:** ShareGuard (`nodaysidle-shareguard`) still missing from portfolio
- **ATLAS:** browser-linux (`nodaysidle-browser-linux`) still missing from portfolio

---

## 5. Previously known now FIXED (status change → ATLAS clear / clear SHIP)

- **SHIP clear:** `whisper-bar` — README now has Installation linking v1.1.2 `WhisperBar.dmg`
- **SHIP clear:** `nodaysidle-shareguard` — README Installation links v0.1.2 DMG (+ checksum)
- **SHIP clear:** `nodaysidle-sonora` — latest release body has real notes (Linux Spotify fix, downloads, SHA-256); not empty/placeholder

---

## 6. Recommendation

**Message ATLAS** (portfolio + status): add nodaysrammar + kureksistant (and optionally ShareGuard / browser-linux remain open but do not re-ping as new); flag `nodaysidle-browser` as portfolio item without a shippable download; note SHIP clears for whisper-bar / shareguard / sonora.  
**Message SHIP:** `nodaysidle-browser` needs a real release asset + README download Install; optional tighten browser-linux Install asset URL.  
**Message REEL:** demo GIFs for `nodaysidle-browser` and `synapse-notes`.  
Do not re-message SHIP for the three Oct 8 install/notes items.

Artifact: `/workspace/sweep-reports/2026-10-11-sunday-catalog-sweep.md`
