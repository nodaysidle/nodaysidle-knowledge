---
type: convention
updated: 2026-10-15
---

# Handoffs

One file per agent per day: `sessions/handoffs/<YYYY-MM-DD>-<AGENT>.md` (AGENT = EO, REACH, REEL, SHIP, ATLAS). Append sections; never edit another agent's file.

Each entry:
- **Task:** one line
- **Did:** what changed, with links (PR, commit, file path)
- **Facts for others:** e.g. "release v1.2 of X ready" (REACH), "clip at path" (REACH/ATLAS)
- **Needs:** `@AGENT` + what, or `@OWNER` + decision
- **Status:** done / blocked / waiting

Readers: EO reads all of today's handoffs before delegating. Each agent reads entries addressed to it. ATLAS reads all, folds facts into LATEST.md and the repo pages, and marks a handoff `folded: true` in its frontmatter.
