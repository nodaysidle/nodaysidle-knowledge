---
type: wiki-note
note_kind: concept
topic_slug: nodaysidle-knowledge
status: active
created: 2026-10-07
updated: 2026-10-07
tags:
  - wiki
  - meta
  - agent
  - bootstrap
---

# Agent entrypoint checklist

## Summary

Standard bootstrap sequence and invariant checklist for any AI coding agent operating inside the `nodaysidle-knowledge` vault. Adhering to this order guarantees context continuity across agent sessions and protects promotion safety boundaries.

## First-read order

Agents must read the following vault paths in exact sequence before proposing or executing research operations:

1. `[[sessions/LATEST.md]]` — Active session pointer. Resolves the current primary research thread.
2. Active session file (e.g. `[[sessions/2026-10-07-vault-operations-session.md]]`) — Captures thread registry, decisions made, do-not-refetch constraints, and open next actions.
3. `[[_system/reference/github-org-repositories.md]]` — Canonical inventory of public organization repositories across GitHub.
4. `[[_system/templates/CATALOG.md]]` — Catalog index and template references across nodaysidle applications and research scaffolds.
5. `[[README.md]]` — Vault architecture, pipeline definitions (`inbox` → `sources` → `wiki` → `briefs` → `projects`), and rules of engagement.

## Operating invariants

- **Wikilinks & Markdown**: Plain Markdown with YAML frontmatter and `[[wikilinks]]` only.
- **Source preservation**: Never delete files under `sources/raw/`; mark superseded in frontmatter index notes instead.
- **Promotion barrier**: Never write under `projects/` or mark `review_status: approved` without an explicit human command: `promote {brief} to project {slug}`.
- **Audit trail**: Append all promotions and major vault edits to `[[_audit/log.md]]`.
- **Session state**: Always update the active session file with progress, `last_agent`, and thread status upon completion.

## Related

- `[[wiki/MOC/moc-nodaysidle-knowledge]]`
- `[[wiki/concepts/knowledge-vault-overview]]`
