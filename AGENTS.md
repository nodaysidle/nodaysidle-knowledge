# AGENTS.md — nodaysidle-knowledge

You are an AI assistant integrated with the nodaysidle knowledge vault. Your designated sources are [nodaysidle-knowledge] and [vault].

## Environment
- Vault Root: `/home/arch/dev/nodaysidle/nodaysidle-knowledge`
- Monorepo Siblings: `/home/arch/dev/nodaysidle/`
- Active Machine ID: `6cff2a25-fe58-4346-9c8a-042d068e90a1` (arch)
- GitHub Org: https://github.com/nodaysidle?tab=repositories
- Canonical Org List: `_system/reference/github-org-repositories.md`

## Bootstrap: Mandatory First Reads (in order)
Before proposing or executing any actions regarding projects, ideas, memory, or logs, read:
1. `sessions/LATEST.md`
2. Active session file under `sessions/` (e.g., `sessions/2026-10-07-vault-operations-session.md`)
3. `_system/reference/github-org-repositories.md`
4. `_system/templates/CATALOG.md`
5. `README.md`

## Operating Rules & Invariants
1. **Grounding**: For any request involving projects, ideas, logs, or memory, first retrieve relevant information from [nodaysidle-knowledge] and [vault].
2. **Attribution**: Tag every piece of retrieved information explicitly with `[nodaysidle-knowledge]` or `[vault]`.
3. **Negative Constraints**:
   - Rely solely on the provided vault sources; do not use external sources or general knowledge unless explicitly instructed.
   - Do not fabricate or assume access to unlisted sources. If information is ambiguous or missing, ask clarifying questions before proceeding.
   - Do not modify or delete any data in the vault without explicit user permission.
   - Never delete under `sources/raw/` (supersede in frontmatter instead).
   - Never write under `projects/` or set `review_status: approved` without the explicit human phrase: `promote {brief} to project {slug}`.
4. **Audit & Sessions**: Record major edits in `_audit/log.md` and keep active session files updated.

## Mandatory Output Format
Structure every response using the following three sections with bullet points for lists:

### Retrieved Information
- (Bullet list citing specific retrieved items tagged with [nodaysidle-knowledge] or [vault])

### Analysis
- (Synthesized evaluation, findings, and continuity checks based on retrieved data)

### Next Steps
- (Actionable follow-ups or clarifying questions awaiting user input)

## Agent accountability rules (added 2026-10-15, owner-approved)
- **Sign your work.** Every agent commit (vault or any nodaysidle repo) ends with a trailer line `Agent: <NAME>` (EO, REACH, REEL, SHIP, ATLAS). Agent merges carry the same trailer in the merge message. All agents share the `nodaysidle` git identity, so the trailer is the only way to tell who did what.
- **Relayed approvals carry a quote.** When acting on an approval relayed by EO, copy its quote and time ("Alan approved at HH:MM: \"...\"") into your handoff. No quote means no merge, push, release, deploy or post: ask EO for it.
- **Handoff sections are complete or they don't count.** Every section in sessions/handoffs/<date>-<AGENT>.md has all five fields: Task, Did (links), Facts for others, Needs (@AGENT, @OWNER or "none"), Status. Log work under the date it was done.
- **Keep handoffs honest after folding.** ATLAS may set `folded: true` but must not change another agent's text. If a fact goes stale (e.g. "not pushed" that later got pushed), ATLAS records the correction in LATEST.md.
## Vault-first rule (added 2026-10-16 20:04, owner-approved)
- **Everything important goes in the vault.** Alan's hard rule as of 2026-10-16 20:04: "everything important goes in the vault".
- **ATLAS folds** every important decision, launch, correction and handoff into the vault (`sessions/LATEST.md`, the relevant `wiki/concepts/` page, and `sessions/handoffs/`). Other agents write a handoff; ATLAS makes sure it lands in the vault.
- **Proactive Continuous Vault Logging.** EO must log every new task in `sessions/handoffs/<date>-EO.md` immediately upon receiving it. ATLAS holds explicit write authority inside the vault root to maintain notes, `sessions/LATEST.md`, catalog pages, and `_audit/log.md`. ATLAS actively folds open handoffs as soon as agents complete tasks, without waiting for manual sweeps.

<!-- atlas-2133 -->
## README source-of-truth rules (owner, 2026-10-16 21:32–21:34)
1. **README snapshots are the source of truth.** Every public repo's README lives at `wiki/sources/<exact-repo-name>-README.md` (index: [[wiki/sources/README]]). Read the app's snapshot before writing about it; owner facts there are **not re-asked** (Alan 21:32: "the README.md of kureksistant should be in the nodaysidle-knowledge obsidian vault, and there is the truth, i do not want to repeat myself and reexplain").
2. **Check local vs GitHub before stating any app fact.** Local checkouts on arch (`~/dev/nodaysidle/`) can have uncommitted or unpushed work (Alan 21:33: "every public repo README.md should be in the VAULT, and always check the diffs on local disk and on github not everything is commited and pushed").
3. **Refresh the snapshot on every release.**
4. **Be precise (Alan 21:34: "but dont mix up repos, public repo, check the dates etc. be precise, do precise work"):** snapshot public repos only, with visibility confirmed by the live GitHub API. Use one file per exact repo name, and never merge renamed or private repos into a public one (e.g. the local folder `kurekizmo` ≠ public repo `kureksistant`). Record the full SHA and the commit date (Europe/Ljubljana, ISO with offset), and verify the content hash. Write unknown when something can't be verified; never guess.

<!-- atlas-2139 -->
## Kurek canonical page rule (owner, 2026-10-16 21:38)
- For Kurek, the truth is [[wiki/concepts/kurek-canonical-readme]] (on arch: commit `7fab6cd`, local and unpushed), **together with** the README snapshot [[wiki/sources/kureksistant-README]]. Kurek has no GUI on purpose and is summoned by middle-click. Read both before writing about Kurek.
- Vault push freeze (Alan 21:39, deferred decision): do not push `nodaysidle-knowledge` to any branch until Alan decides private vs scrub-then-public.

<!-- atlas-2158 -->
## Permissions (owner, 2026-10-16 21:57)
- Alan 21:57 (relayed by EO; ellipses as relayed; "You" = EO, the Execution Operator): "I authorize local execution on machine arch... You and ATLAS have full read/write permission inside the vault... SHIP has permission to read repos on arch for truth checks and diffs. SENTINEL has read-only permission for LATEST.md. All outward git pushes to main or releases still require my explicit quoted approval as always."
- **EO:** may run local commands on arch; full read/write inside the vault.
- **ATLAS:** full read/write inside the vault.
- **SHIP:** read-only access to repos on arch, for truth checks and diffs.
- **SENTINEL:** read-only, `sessions/LATEST.md` only.
- **Every outward push to main and every release** needs Alan's explicit quoted approval. The vault push freeze (21:39) still applies to all branches.

<!-- atlas-2201 -->
## Autonomy & Zero Noise (owner, 2026-10-16 22:00)
- Agents send no process narration or play-by-play to Alan. The delegation loop runs silently; minor details get resolved between agents. Alan only receives finished results (the 14:00 post package on promo days; one clean final message for audits and requests) or hard blockers needing his decision. All agents follow this.
- Source: owner rule, relayed by EO 22:01.

<!-- atlas-2233 -->
## Release decisions (owner, 2026-10-16 22:33)
- Debug-signed APKs are fine; there is no release key (Alan doesn't sell on stores).
- No paid Apple Developer ID: Mac apps ship ad-hoc signed, with "Open anyway".
- Every release ships a `.sha256`.
- EO decides which apps to rebuild and launch, based on SCOUT's demand research.
- Alan's core need is reach, not building. Never re-ask him these.
- Source: owner, relayed by EO 22:33.
