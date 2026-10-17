---
title: "Vault audit method (nodaysidle-knowledge, 2026-10-17)"
author: Nodaysidle
date: 2026-10-17
branch: main
cost: { minutes: 5, tokens: 173352 }
touches:
  - AGENTS.md
  - VAULT_GUIDE.md
  - briefs/draft/nodaysidle-browser-linux-ux-findings-brief-v1.md
  - briefs/x-drafts/2026-10-17-poll.md
  - sources/README.md
  - sessions/LATEST.md
  - "_audit/log.md"
---

## Decided
- A vault audit is read-only. Report in the AGENTS.md 3-section format, with the user's requested sections nested inside it. Make no vault edits without the owner's explicit permission.
- "Grok Bot" is not a single agent. It is the shared runtime label ("ATLAS, Grok Bot", "REACH, Grok Bot", "Grok Bot executor", "Grok Bot box"). Audit every ledger entry that carries the label.
- Count wikilinks as broken only after resolving folder-relative links. [[index/...]] in sources/README.md and [[catalog/...]] in CATALOG.md resolve fine. {{placeholders}} under _system/templates/research/ are expected.

## Tried and ruled out
- Matching wikilinks naively on basename or full path gave 91 "broken" links. All were relative links or template placeholders; none was really broken.
- The dirty counts of 3 in sibling repos are trail/claude scaffolding (.trail/, .claude/, AGENTS.md), not real work. Only synapse-notes (43), chrome-extension (28) and browser-linux (23) have real uncommitted changes.

## Watch out
- The catalog layer (_system/templates/catalog/, CATALOG.md) lags behind sessions/LATEST.md and wiki/sources/. Check catalog status and version fields against LATEST before trusting them.
- Repo counts disagree: VAULT_GUIDE/README say 36, org-ref frontmatter says 38, there are 39 snapshots. F1-nodaysidle and openidle are missing from the org ref.
- In _audit/log.md, many entries since 2026-10-15 have no Actor field. There are duplicate, contradictory 21:25 entries and a truncated 2026-10-10 18:25 entry.
- The YAML frontmatter is invalid in briefs/x-drafts sonora, apps-hub and cascade, so Dataview can't read them.
