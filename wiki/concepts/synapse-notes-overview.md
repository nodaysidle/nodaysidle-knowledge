---
type: wiki-note
note_kind: concept
topic_slug: synapse-notes
status: draft
created: 2026-10-07
updated: 2026-10-07
tags:
  - wiki
  - synapse-notes
---

# Synapse Notes — overview

## Summary

Synapse Notes is a voice-first Android notes app (Capacitor 8, `com.synapse.notes`, debug APK sideload only). A recording is uploaded to Supabase Storage, transcribed via OpenRouter, embedded as a 768-d vector, optionally given a generated image, and lands on Home. A separate Three.js Graph screen links notes that share at least 2 keywords. Licence: MIT.

## Details

- **Backend:** Supabase (Postgres, Storage, Realtime, Edge Functions). All AI calls run in Edge Functions, so the OpenRouter key is never in the APK.
- **Models:**
  - transcription: gpt-4o-mini-transcribe, with whisper-large-v3 and chirp-3 as fallbacks;
  - embeddings: gemini-embedding-001;
  - images: krea-2-medium-turbo, with gemini-3.1-flash-lite-image as fallback.
- **Embedding use:** embeddings power only "similar notes" on the note detail screen. The Notes list filter is a substring match, the graph uses keywords, and ask-notes has no UI.
- **Releases:** seven, v0.1.0 (2026-06-07) to v0.4.3 (2026-08-30), all debug APKs. v0.4.3 was phone-tested on a Xiaomi M2007J3SY with Android 12.
- **History:** 40 commits, `79fc7d1` to `a6e10fa` (2026-09-18).

## Contradictions & gaps

1. **Distribution and graph:** the internal codemap says it ships as a web app and Android app and links notes via semantic search. The README says Android only, with keyword graph edges.
2. **Design plans (2026-01-25):** they describe glassmorphism with teal/cyan, workspace collaboration and Vercel deployment. The shipped app is void-black with muted green and has no join/workspace onboarding. The plans predate the repo's first commit.
3. **Status names:** v0.2.0 uses Queued/Processing/Ready/Failed; the README uses Queued/Live/Ready/Failed.
4. **Feature claims:** v0.2.0 lists "semantic search and note Q&A", but later notes and the README say ask-notes has no UI and list search isn't semantic.
5. **Versioning:** the v0.3.0 notes say the Gradle versionName was still 0.2.0. v0.1.1 has no asset.
6. **Doc pointers:**
   - root AGENTS.md lists PRD/ARD/TRD/TASKS/TODO/CHANGELOG, none of which exist;
   - docs/internal/AGENTS.md says the codemap is "in the project root", but it's in `docs/internal/`;
   - docs/AGENTS.md lists no child docs, though `docs/internal/AGENTS.md` exists.
7. **Not ingested:** `frontend/`, `shared/`, `supabase/` and `assets/` AGENTS.md files, and `prompts/release-check.md`. All are outside `docs/` and the root.

## Claims & citations

| Claim | Source |
|-------|--------|
| Pipeline, Graph, screens, models, stack, Android-only | [[sources/index/src-20261007-77e0f33-synapse-notes-readme]] |
| Agent rules, missing PRD/ARD etc. | [[sources/index/src-20261007-67b1886-synapse-notes-agents]] |
| docs contract, child index "None" | [[sources/index/src-20261007-5fa8138-synapse-notes-docs-agents]] |
| docs/internal is an archive | [[sources/index/src-20261007-ce75492-synapse-notes-docs-readme]], [[sources/index/src-20261007-28f622a-synapse-notes-internal-readme]] |
| Codemap "in project root" | [[sources/index/src-20261007-edbf2ff-synapse-notes-internal-agents]] |
| Web + Android, semantic linking | [[sources/index/src-20261007-6c69203-synapse-notes-internal-codemap]] |
| Glassmorphism, collaboration, Vercel | [[sources/index/src-20261007-e444638-synapse-notes-plan-redesign-2026-01-25]], [[sources/index/src-20261007-fd8a340-synapse-notes-plan-implementation-2026-01-25]] |
| Releases, status names, versionName | [[sources/index/src-20261007-f818afc-synapse-notes-github-releases]] |
| Commits | [[sources/index/src-20261007-ec9ad0c-synapse-notes-git-log]] |

## Related

- [[wiki/MOC/moc-nodaysidle-knowledge]]
- [[_system/templates/catalog/synapse-notes]]

## Decisions and fixes (user, 2026-10-07 14:07 UTC+2; commit `d659005`, push pending authentication)

- **#1:** the internal codemap now says Android APK only, with a history note that the project evolved from a web plan.
- **#2:** both January plans have a "superseded" banner, which also states the README status names (Queued → Live → Ready / Failed).
- **#3 Status names:** no current repo doc used "Processing" apart from the superseded plans, so the banners cover it. The v0.2.0 GitHub release text still says "Processing"; it can't be edited without `gh`.
- **#4 Q&A and semantic search: user decision conflicts with the code, so no doc change was made.**
  - Semantic search has a screen: "similar notes" on `NoteDetail.tsx:167`, which the README already says.
  - `ask-notes` exists only as an Edge Function (`supabase/functions/ask-notes`). No frontend file calls it (`rg ask-notes|askNotes frontend/src` returns nothing).
  - So the README's "no screen calls it" is accurate at HEAD and was left unchanged, to avoid writing false docs. Needs the user to confirm.
- **#5 Versioning:** accepted, no change.
- **#6 Doc pointers:** all three fixed (root AGENTS.md reading list, the docs/internal/AGENTS.md codemap location, the docs/AGENTS.md child index).
