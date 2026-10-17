---
type: artifact
artifact_kind: audit
topic_slug: vault-operations
generated: 2026-10-17
generator_agent: Claude Opus
verified_at: 2026-10-17T03:18:00+02:00
scope:
  - nodaysidle-knowledge (whole vault)
  - "_audit/log.md entries labelled Grok Bot, ATLAS, REACH, Execution Operator"
  - "sibling folders under ~/dev/nodaysidle/ (local git metadata only)"
tags:
  - artifact
  - audit
  - vault-health
  - agent-compliance
---

# Vault and Grok Bot audit, 2026-10-17

**How this was checked:** read-only. I read the vault files, ran local `git` on arch and used local scripts to check wikilinks and YAML. I made **no GitHub, X or Vercel calls**, so every GitHub fact here is what the vault records, not something re-checked live. Remediation done after the audit (owner-approved the same day) is listed in §6.

**Read in this order:** `VAULT_GUIDE.md`, `README.md`, [[sessions/LATEST]], [[sessions/2026-10-08-kureksistant-session]], [[sessions/2026-10-07-vault-operations-session]], [[_audit/log]], [[_system/reference/github-org-repositories]], [[_system/templates/CATALOG]], every file under `_system/templates/catalog/`, [[wiki/MOC/moc-nodaysidle-knowledge]], `wiki/concepts/`.

## 1. Executive summary

- **Vault health: 6/10.** The hard rules hold, and no wikilinks are really broken. But the catalog, the repo counts and the session pointers have fallen behind the 2026-10-16 work, and nobody uses the brief stage of the pipeline.
- **Grok Bot compliance: 8/10.** It broke no hard rule, and it corrected most of its own errors. The weak points are a few claims that were never checked, unclear labels on who did what, and no attribution tags in its early ledger entries.
- **Verdict:** safe and auditable, but split in two speeds. [[sessions/LATEST]] and `wiki/sources/` are current to 2026-10-16 23:27. The catalog, the guide documents and the session files are 1 to 9 days stale.
- **Who "Grok Bot" is:** it is not one agent. The ledger uses it as a shared runtime label: "ATLAS, Grok Bot", "REACH, Grok Bot", "Execution Operator, Grok Bot", "Grok Bot executor", and "the Grok Bot box" for the machine that holds the clips. This audit covers every entry with the label.

## 2. Evidence ledger [nodaysidle-knowledge]

- **Promotion gate:** `projects/` holds only `README.md`. No file has `promoted: true`. Every `review_status: approved` match is the rule's own text (e.g. `briefs/draft/readme-sweep-brief-v1.md:147`).
- **Raw sources:** 43 raw files and 43 index stubs. `git log --diff-filter=D` shows no deletion under `sources/raw/` or `projects/`. Superseded files are marked in frontmatter (log 2026-10-08 05:54).
- **Grok Bot entries, 2026-10-07:**
  - It stated its inferences openly ("31 + 5 = 36. Inferred, not confirmed").
  - It refused workarounds when pushes failed ("No retry or token workaround was attempted", 13:17 and 13:24).
  - It confirmed the owner's pushes with `git fetch` (14:19:52).
- **Self-corrections:**
  - 2026-10-09 10:32 reported the "could of" rule missing. It actually exists as a regex; corrected at 10:34.
  - 2026-10-10 05:11 flagged "24 tools stale". Corrected at 06:11.
- **Security item closed without a check:** 2026-10-12 05:31: "Not re-verified by ATLAS (cheap mode)".
- **Repo counts before remediation:**
  - `VAULT_GUIDE.md` and `README.md` said 36 public repos.
  - The org-reference frontmatter said 38.
  - `wiki/sources/` has 39 README snapshots; the vault itself is public but not snapshotted, so the total is 40. `F1-nodaysidle` and `openidle` were missing from the org list.
  - `VAULT_GUIDE.md` said "70+ projects". The ledger total is 48, and that figure is unverified.
- **[[sessions/LATEST]] [vault]:**
  - Frontmatter says `updated: 2026-10-16 21:11` and "on branch atlas/fold-2026-10-16 (not main yet)". The body runs to 23:27, and the branch is `main`.
  - "Resume here" still points to the Kurek session, but Kurek was parked at 21:46.
- **Local disk (git only) [local disk, not vault]:**
  - `nodaysidle-prompt-optimizer` local `master` is at `d57a093` (2026-10-15 21:29), 1 commit ahead of its last-fetched upstream. The vault says `master` is still `818eed1`.
  - Uncommitted entries: `synapse-notes` 43, `chrome-extension` 28, `nodaysidle-browser-linux` 23. The other repos show only trail/claude scaffolding.

## 3. Critical findings

### Hard rules
- None broken: promotion gate, raw sources and the append-only rule all hold.

### Ledger problems (`_audit/log.md`)
- **Truncated entry:** 2026-10-10 18:25 (Antigravity). "Created / Edited:" was empty, and the next heading started on the following line. *(Fixed, §6.)*
- **Duplicate 21:25 headings that contradict each other.** One said the Cascade plan was "presented to Alan". The other said it "had not been shown to Alan". The first was also inserted into the middle of the 21:11 entry (commit `7fab6cd`). *(Fixed, §6.)*
- **25 entries since 2026-10-15 02:22 had no `Actor` field.** *(Back-filled, §6.)* Several older ones are loose bullets with no heading (2026-10-10 16:28, 2026-10-11 to 10-14 ATLAS lines). These were left as written.
- **Entries out of time order:** 22:35 comes before 22:32, 17:40 before 17:35, and 15:34 before 15:10. Left as written, because reordering would rewrite history.

### Stale catalog entries (`_system/templates/catalog/`)
- `nodaysidle-shareguard.md`: says `completed`, but ShareGuard is parked (its release ships a stale 0.1.0 DMG).
- `synapse-notes.md`: lists v0.4.3; v0.4.5 is Latest (2026-10-16 22:58).
- `whisper-bar.md`: no "unmaintained Mac build" note, though it posts on 2026-10-17.
- `kurekizmo.md`: nothing on the headless no-GUI daemon identity (2026-10-16 21:32), the parking (21:46) or PR #24.
- `CATALOG.md`: the Kurek row was flagged stale (v0.2.0 against v0.2.1) but not fixed. The nodaysrammar row mixes v1.0.0 and v1.0.1.
- `portfolio-site.md`: `repo_url` points to the stale `nodaysidle-project-pages`.
- `local_path` is still a placeholder for cascade-v3, sonora and synapse-notes, though all three are cloned on arch.
- **ClipRail has no catalog entry** although its launch slot is confirmed for Tue 3 Nov.

### Local folders vs the vault
- **No vault documentation, no git remote:** `david_bumbleblack`, `graft`, `klemen-caj`, `loop-skill`, `nodalaya`, `nodayshop`, `nodaysign`, `nodayung`, `nodotsidle`, `nostyleguide`, `tools`, `artifacts`.
- `sugarbots` is a clone of `nitrictech/sugabots`, not an org repo.
- `F1-nodaysidle` and `openidle` have a snapshot only: no catalog entry, and they were not in the org list.
- **The other direction is clean:** every catalog entry without a local checkout (apps, shareguard, whisper-bar) is a real public repo.

### Pipeline blockages
- `briefs/in-review/` and `briefs/approved/` are empty. No brief has ever been reviewed. Real work runs through handoffs and direct PRs and skips the brief stage.
- `readme-sweep-brief-v1` was carried out in full (5 of 5 PRs merged) but still reads `draft`/`pending`.
- In `inbox/`, two ideas from 2026-10-07 and 10-08 are still `open`. Two Kurek slot records (`void` and `confirmed`) are decisions, not ideas.
- Uncommitted for about 2 days: [[briefs/draft/nodaysidle-browser-linux-ux-findings-brief-v1]] and [[briefs/x-drafts/2026-10-17-poll]].
- **Risk for 2026-10-17:**
  - The WhisperBar 17:30 draft (due to Alan by 14:00) is not in the vault. Under the vault-first rule it should be.
  - A Sat 17:00 poll draft exists that [[sessions/LATEST]] never mentions. That could mean two posts within 30 minutes.

### Links and MOC
- **No real broken wikilinks.** A naive scan finds 91 misses, but they are links written relative to their folder (`[[index/…]]`, `[[catalog/…]]`, which resolve) plus `{{template}}` placeholders.
- The MOC does not link [[wiki/concepts/kurek-canonical-readme]] (the required Kurek truth page) or [[wiki/sources/README]].
- Nothing links to `briefs/x-drafts/2026-10-21-kurek.md` or `briefs/x-drafts/2026-10-16-PACKETS.md`.

### Frontmatter
- The YAML was invalid in `briefs/x-drafts/2026-10-16-sonora.md`, `2026-10-16-apps-hub.md` and `2026-10-15-cascade.md`. *(Fixed, §6.)*
- `2026-10-16-PACKETS.md` and `briefs/launch/cascade-big-launch-PLAN.md` have no frontmatter.
- Status words vary (`copy-approved`, `approved-locked`). `approved-locked` on Cascade is stale, because the post never went live.
- Only 1 of 14 catalog files has `updated`. Both MOCs and `kurek-canonical-readme` lack `updated`.

## 4. Grok Bot performance review

**Strengths**
- It respected the gate in every entry ("Nothing under `projects/`").
- It recorded contradictions instead of quietly resolving them (e.g. private vs public, 2026-10-07 13:50).
- It did not attempt workarounds when pushes failed.
- It corrected itself in the append-only style.
- It handled secrets carefully: it checked only whether `api_keys.json` exists and its date, never the contents, and it removed Tailscale IPs from vault files.

**Blindspots and errors**
- **Repo count:** at 2026-10-07 14:18 it marked the org count "Resolved" on the basis of the owner's own repo list, which was never checked against the API. The 48 total is still unverified.
- **Search miss:** it searched for the literal text "could of" when the rule is a regex, and reported the rule missing (2026-10-09 10:32).
- **Stale GIF claim:** "real demo GIF" (2026-10-10 07:35) is now stale. The README at `09e3c7d` has no GIF.
- **Unverified security closure:** the 2026-10-12 05:31 closure was taken on EO's word.
- **No attribution tags:** none of its ledger lines from 2026-10-07 to 10-12 carry `[vault]` or `[nodaysidle-knowledge]`.
- **Uncommitted work:** it kept leaving the vault uncommitted ("Nothing committed in this vault").
- **Unclear authorship:** the shared "Grok Bot" label makes it impossible to tell agents apart before the `Agent:` trailer rule of 2026-10-15.
- **Catalog not updated:** the 2026-10-16 truth went to LATEST and the wiki, never to the catalog.

## 5. Remediation plan

- **P0:**
  - Put the WhisperBar 17:30 draft into `briefs/x-drafts/` before 14:00, and confirm whether the 17:00 poll runs too.
  - Fix the [[sessions/LATEST]] frontmatter and its "Resume here" pointer.
  - ✅ Clean up the ledger (§6).
- **P1:**
  - Update the catalog: ShareGuard parked, Synapse v0.4.5, Kurek headless / v0.2.1 / parked, WhisperBar unmaintained, portfolio `repo_url`, the three `local_path` placeholders.
  - Add a ClipRail catalog entry.
  - ✅ Add `F1-nodaysidle` and `openidle` to the org list and align the counts (§6).
  - Re-check prompt-optimizer `master`.
  - Decide whether the 11 local folders without remotes belong in the vault.
- **P2:**
  - ✅ Fix the x-draft YAML (§6).
  - Add `updated` to the MOCs and catalog files.
  - Link the Kurek canonical page and [[wiki/sources/README]] from the MOC.
  - Require an `Actor` field on every new ledger entry.
  - Close or review `readme-sweep-brief-v1`.
  - Turn the two inbox slot records into decision notes.

## 6. Remediation done 2026-10-17 (owner-approved in chat)

- **x-drafts YAML now parses** with `yaml.safe_load`:
  - `2026-10-16-sonora.md` and `2026-10-16-apps-hub.md`: the `> STATUS 10:26 …` blockquote line moved, unchanged, from inside the frontmatter to just below it.
  - `2026-10-15-cascade.md`: the `approved`, `signoff.media`, `signoff.claims` and `signoff.copy-sync` values are now single-quoted. Their text is unchanged; one apostrophe was doubled as YAML escaping.
- **Org reference:**
  - [[_system/reference/github-org-repositories]] now lists `F1-nodaysidle` and `openidle`.
  - `public_repo_count` changed from 38 to 40, with a dated Update section explaining the source.
  - `VAULT_GUIDE.md` and `README.md` now say 40 public repos (as of 2026-10-16). "70+ projects" was replaced with a pointer to the org reference.
- **`_audit/log.md` cleanup (nothing deleted):**
  - The truncated 2026-10-10 18:25 entry is closed with a "not recorded" note.
  - The 21:25 pair is labelled part 1 of 2 and part 2 of 2. The contradicted "presented to Alan" line has a correction marker.
  - The stray 21:11 line was moved back into its entry, with a note (blame: commit `19cc732`).
  - 25 missing `Actor` fields were back-filled from each heading and the commit's `Agent:` trailer.
  - Out-of-order entries were left in place.
