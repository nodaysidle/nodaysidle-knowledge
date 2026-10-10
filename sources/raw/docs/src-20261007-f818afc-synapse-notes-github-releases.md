# GitHub releases — nodaysidle/synapse-notes

Fetched 2026-10-07 from https://api.github.com/repos/nodaysidle/synapse-notes/releases (verbatim release bodies).

## v0.4.3 — Synapse Notes v0.4.3

- published_at: 2026-08-30T22:51:46Z
- prerelease: false
- assets: synapse-notes-0.4.3-debug.apk (sha256:cbedace5a2aa0c14320104cc884d042ebeca529b91966370c57de994261438cd)

Phone-tested on Xiaomi M2007J3SY (Android 12).

**This build**
- Compact Notes / Gallery (no sideways scroll)
- Bottom tabs stay tappable
- Android Back pops; only leaves the app from Home
- Home unchanged (void black, centered mic)

Debug APK (`com.synapse.notes` 0.4.3). Same file that is on the phone.

## v0.4.1 — Synapse Notes v0.4.1

- published_at: 2026-08-30T21:22:24Z
- prerelease: false
- assets: synapse-notes-0.4.1-debug.apk (sha256:fbd2b73ff882d91afcac767ce97b00262a216fa6e88811c9b9516bd262423716)

Android debug APK (`com.synapse.notes` 0.4.1). Same Home as 0.4.0 (centered mic, void black, muted green, header Synapse Notes). Non-graph screens now share that void-black background. Graph is unchanged.

## Flow
Tap mic → audio stored on Supabase → transcript + embedding + optional image → note on Home. Title is the first sentence. Related notes on the graph. No account.

## Models (OpenRouter)
- Transcribe: `openai/gpt-4o-mini-transcribe`, then `openai/whisper-large-v3`, `google/chirp-3`
- Embeddings: `google/gemini-embedding-001` (768-d)
- Image: `krea/krea-2-medium-turbo`, then `google/gemini-3.1-flash-lite-image`
- Ask notes (no UI): `openai/gpt-5.6-luna`, then `google/gemini-2.5-flash-lite`

Not iOS. Sideload debug build.

## v0.4.0 — Synapse Notes v0.4.0

- published_at: 2026-08-30T21:09:39Z
- prerelease: false
- assets: synapse-notes-0.4.0-debug.apk (sha256:2cf571e94cae2060a24dcd4aa5395f179de8d18742f1c919e4a0c2dfef888124)

Android debug APK (`com.synapse.notes` versionName 0.4.0). Centered mic, void-black Home, muted green, header Synapse Notes. No join. No empty-state copy.

## Flow
Tap mic → audio stored on Supabase → transcript + embedding + optional image → note on Home. Title is the first sentence. Related notes on the graph. No account.

## Models (OpenRouter)
- Transcribe: `openai/gpt-4o-mini-transcribe`, then `openai/whisper-large-v3`, `google/chirp-3`
- Embeddings: `google/gemini-embedding-001` (768-d)
- Image: `krea/krea-2-medium-turbo`, then `google/gemini-3.1-flash-lite-image`
- Ask notes (no UI): `openai/gpt-5.6-luna`, then `google/gemini-2.5-flash-lite`

Not iOS. Sideload debug build.

## v0.3.0 — Synapse Notes v0.3.0

- published_at: 2026-08-30T20:49:35Z
- prerelease: false
- assets: synapse-notes-0.3.0-debug.apk (sha256:cf39569367eabc9efcec872c4f488d5757c1e05270e0596a8a32a9a9a6bfa9a1)

Android debug APK (`com.synapse.notes`). Notes-first Home from main. No join.

## Flow
Tap mic → audio stored on Supabase → transcript + embedding + optional image → note on Home. Title is the first sentence of the transcript. Open the note, or related notes on the graph. No account. A My Notes workspace is created for you.

## Models (OpenRouter)
- Transcribe: `openai/gpt-4o-mini-transcribe`, then `openai/whisper-large-v3`, `google/chirp-3`
- Embeddings: `google/gemini-embedding-001` (768-d)
- Image: `krea/krea-2-medium-turbo`, then `google/gemini-3.1-flash-lite-image`
- Ask notes (function only, no UI): `openai/gpt-5.6-luna`, then `google/gemini-2.5-flash-lite`

Not iOS. Sideload debug build. Package versionName is still 0.2.0 in Gradle; this release is the notes-first Home + leftover join files removed.

## v0.2.0 — Synapse Notes v0.2.0

- published_at: 2026-07-31T06:45:43Z
- prerelease: false
- assets: debug.apk (sha256:09ddaa652cd8940b9fb7752a29deb7382933bbf4924169e76acc3d567c3c767d)

## Synapse Notes v0.2.0

The first release that feels like the complete Synapse experience: fast voice capture, dependable AI processing, a smooth knowledge graph, and generated visuals that can be saved directly to Android.

### Highlights

- OpenRouter-backed transcription, embeddings, image generation, semantic search, and note Q&A
- primary Krea 2 Medium Turbo visual generation
- clear Queued, Processing, Ready, and Failed states
- retry interrupted processing without recording again
- visible recording-save recovery
- native downloads into `Pictures/Synapse Notes`
- download shortcuts in Note Detail and Gallery
- refreshed launcher icon and repository branding
- Android version `0.2.0` / code `2`

### Compatibility

- Android 7.0 or newer (`minSdk 24`)
- targets Android 16 (`targetSdk 36`)
- debug-signed sideloading build; not a Play Store release

### Verified on

Redmi 15 4G (`creek`) running Android 16. Voice capture, authenticated workspace loading, notes, Gallery, graph, native MediaStore downloads, and cold launch were exercised on-device.

### APK integrity

`debug.apk` SHA-256:

```text
09ddaa652cd8940b9fb7752a29deb7382933bbf4924169e76acc3d567c3c767d
```


## v0.1.1 — NODAYSIDLE theme fleet v0.1.1

- published_at: 2026-07-23T22:39:21Z
- prerelease: false
- assets: 

## NODAYSIDLE public theme alignment

Aligns this public repository with the NODAYSIDLE theme fleet (2026-07-23).

### Included
- Public-facing theme/token alignment from the fleet theme branch merged to the default branch.

### Notes
- Scope is theme alignment only; no feature changelog beyond that merge.
- See the merged PR titled "chore: align public NODAYSIDLE theme" for the exact diff.

## v0.1.0 — Synapse Notes v0.1.0

- published_at: 2026-06-07T00:05:09Z
- prerelease: false
- assets: Synapse-Notes-0.1.0-debug.apk (sha256:b83ae21646873a00e3b2527a4846962f40aeda4f77a43bc2124fce7756d56b50)

# Synapse Notes v0.1.0

GitHub migration release for Synapse Notes.

## Download

- `Synapse-Notes-0.1.0-debug.apk` — Android debug APK for direct side-loading/testing.

## Verification

- `npm ci` completed.
- `npm run typecheck` passed.
- `npm run build` passed.
- `npx cap sync android` passed.
- `ANDROID_HOME=/Users/archuser/Library/Android/sdk ./gradlew assembleDebug` passed.
- APK SHA256: `b83ae21646873a00e3b2527a4846962f40aeda4f77a43bc2124fce7756d56b50`

## Caveat

This APK is a debug build. It is not Play Store signed and is intended for testing/side-loading.


