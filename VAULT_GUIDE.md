# NODAYSIDLE Knowledge Vault Guide

> **Central Reference for Sibling Projects & Multi-Agent Collaboration**  
> Workspace Root: `/home/arch/dev/nodaysidle`  
> Vault Path: `/home/arch/dev/nodaysidle/nodaysidle-knowledge`  
> GitHub Org: [nodaysidle (40 public repos)](https://github.com/nodaysidle?tab=repositories)  
> Vault Repo: [nodaysidle-knowledge](https://github.com/nodaysidle/nodaysidle-knowledge)

---

## 1. Vault Purpose & Architecture

The `nodaysidle-knowledge` vault is the single source of truth for research, ideas, memory, and project briefs across all projects in the nodaysidle ecosystem (40 public GitHub repos as of 2026-10-16; see `_system/reference/github-org-repositories.md`). Sibling directories (e.g. `nodaysidle-prompt-optimizer`, `markdown-helper`, `skill-gallery`, `Portfolio`, `nodaysidle-browser-linux`) hold application source code; this vault holds **evidence, persistent memory, and handoffs**.

### Research Pipeline
```text
inbox/ idea → parallel research threads → sources/ (stubs & raw captures) 
  → wiki/ (atomic concept notes) → artifacts/ (audits & summaries) 
  → briefs/ (draft → in-review → approved) → [HUMAN PROMOTION GATE] → projects/
```

---

## 2. Mandatory First Reads for Any Agent

Before analyzing, creating, or editing code or research, every agent must read in this strict sequence:

1. `nodaysidle-knowledge/sessions/LATEST.md` — Resolves the primary active session.
2. Active session file (e.g. `nodaysidle-knowledge/sessions/2026-10-07-vault-operations-session.md`) — Current state, thread registry, decisions made, do-not-refetch rules.
3. `nodaysidle-knowledge/_system/reference/github-org-repositories.md` — Canonical index of published GitHub repositories.
4. `nodaysidle-knowledge/_system/templates/CATALOG.md` — Catalog template index and portfolio registry.
5. `nodaysidle-knowledge/README.md` — Operating rules and safety constraints.

---

## 3. Agent Integration & Auto-Loading

| Agent | Auto-Discovery Mechanism | Setup Required |
|---|---|---|
| **Cursor / cursor-cli** | `.cursorrules` in vault root | None when working in `nodaysidle-knowledge`. If working in parent directory, point Cursor to the vault or include `.cursorrules`. |
| **Pi (Oh-My-Pi)** | `AGENTS.md` in vault root | Run `pi` inside `nodaysidle-knowledge` or run `pi @nodaysidle-knowledge/AGENTS.md`. |
| **agy (Antigravity)** | Task bootstrap prompt | Paste `_system/config/agy-vault-bootstrap.md`. |
| **grokbot** | System/Session prompt | Provide the Grokbot Knowledge Prompt (see Section 6). |

---

## 4. Universal Operating Invariants

1. **Grounding & Sourcing**: Every statement regarding projects, history, ideas, and decisions must ground in `[nodaysidle-knowledge]` and `[vault]`.
2. **Attribution**: Inline tags must clearly indicate the source (e.g., `[nodaysidle-knowledge]` or `[vault]`).
3. **No External Guessing / Hallucination**: If information is missing or ambiguous, ask clarifying questions before proceeding.
4. **Safety & Deletions**: Never delete files under `sources/raw/`; mark superseded in frontmatter instead.
5. **Human Promotion Gate**: Never write under `projects/` or mark `review_status: approved` without the explicit human instruction: `"promote {brief} to project {slug}"`.
6. **Audit Ledger**: Major actions, syncs, and promotions must append to `_audit/log.md`.

---

## 5. Mandatory Response Structure

All agents must format their responses using this 3-section structure:

### Retrieved Information
- Bulleted facts and quotes tagged with `[nodaysidle-knowledge]` or `[vault]`.

### Analysis
- Synthesis, continuity checks, technical reasoning, and evaluations based strictly on retrieved facts.

### Next Steps
- Actionable steps, open questions, or recommendations awaiting human review.

---

## 6. Grokbot Knowledge Prompt

Copy and supply the prompt below to **grokbot** so he ingests all vault wiki notes, historical logs, and current memory:

```markdown
You are Grokbot, an intelligent coding and research assistant integrated with the nodaysidle knowledge vault.

Your memory and grounding sources are:
- Vault Root: /home/arch/dev/nodaysidle/nodaysidle-knowledge
- Monorepo Root: /home/arch/dev/nodaysidle

## Initial Memory & History Ingestion
To know exactly who we are, what we have built, and what we are currently doing, read these core vault files immediately:
1. Sessions & Current State:
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/sessions/LATEST.md
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/sessions/2026-10-07-vault-operations-session.md
2. Audit Trail & Accomplishments:
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/_audit/log.md (Contains the timeline of initial bootstrap, repository syncs, public GitHub releases, and agent alignments)
3. Wiki & Map of Content:
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/wiki/MOC/moc-nodaysidle-knowledge.md
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/wiki/concepts/knowledge-vault-overview.md
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/wiki/concepts/agent-entrypoint-checklist.md
4. Ecosystem Catalog & Repositories:
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/_system/reference/github-org-repositories.md
   - /home/arch/dev/nodaysidle/nodaysidle-knowledge/_system/templates/CATALOG.md

## Rules
- Tag all retrieved information with [nodaysidle-knowledge] or [vault].
- Ground all discussions regarding projects, ideas, memory, and code strictly on these files.
- Never delete sources under sources/raw/ or write to projects/ without explicit human approval.
- Format all responses using three clear sections:
  1. Retrieved Information
  2. Analysis
  3. Next Steps
```
