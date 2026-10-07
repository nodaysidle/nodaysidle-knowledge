<p align="center">
  <h1 align="center">nodaysidle-knowledge</h1>
</p>

<p align="center">
  <strong>Obsidian-native research vault for AI agents: parallel threads, cited sources, atomic wiki notes, review-gated briefs, and promotion into real projects. Plain Markdown only—portable across Cursor, Codex, agy, and deepseek-harness.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Format-Markdown%20%2B%20YAML-000000?style=flat-square&logo=markdown&logoColor=white" alt="Markdown">
  <img src="https://img.shields.io/badge/Links-Obsidian%20wikilinks-7C3AED?style=flat-square" alt="Wikilinks">
  <img src="https://img.shields.io/badge/Agents-Cursor%20%7C%20Codex%20%7C%20agy-4E6EF2?style=flat-square" alt="Agents">
  <img src="https://img.shields.io/badge/telemetry-none-4c8c6b?style=flat-square" alt="No telemetry">
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License">
</p>

---

> **The Problem:** Research scattered across chat logs, bookmarks, and ad-hoc notes does not survive the next agent session. Promoting an idea into a repo without citations, review, or audit trail creates rework and untrusted briefs.
>
> **The Result:** A single vault with a **linear pipeline**—inbox → sources → wiki → artifacts → brief → human approval → `projects/`—plus session files so any agent resumes from `sessions/LATEST.md` without re-fetching everything. Raw sources are never deleted; they are superseded in frontmatter. Promotion is blocked until a human completes the review checklist.

---

## What is nodaysidle-knowledge?

Team research operating system for [nodaysidle](https://github.com/nodaysidle): wikilinks, YAML frontmatter, catalog templates for every portfolio repo, and an append-only `_audit/log.md`. Application code stays in sibling repositories; this repo holds **evidence, notes, and handoffs**.

**Org index (31 public repos):** [_system/reference/github-org-repositories.md](_system/reference/github-org-repositories.md) · [github.com/nodaysidle?tab=repositories](https://github.com/nodaysidle?tab=repositories)

## Pipeline

```text
inbox idea → research (parallel threads) → sources/ → wiki/ → artifacts/
  → brief (draft → in-review → approved) → human gate → projects/
```

## Open as Obsidian vault

Clone beside your code monorepo (sibling paths like `../nodaysidle-prompt-optimizer` are referenced in catalog templates):

```bash
git clone https://github.com/nodaysidle/nodaysidle-knowledge.git
```

In Obsidian: **Open folder as vault** → select the clone root.

## Directory map

```text
nodaysidle-knowledge/
├── README.md
├── _system/templates/     # catalog + research scaffolds
├── _system/reference/     # GitHub org mirror
├── _system/config/        # agy bootstrap prompt
├── inbox/                 # rough topics
├── sessions/              # resume here (LATEST.md)
├── sources/               # index stubs + raw captures
├── wiki/                  # MOC + atomic notes
├── briefs/                # draft | in-review | approved
├── artifacts/             # summaries, audits, queries
├── projects/              # promoted briefs only
└── _audit/log.md          # append-only
```

## Templates

| Path | Use |
|------|-----|
| [_system/templates/CATALOG.md](_system/templates/CATALOG.md) | Index of nodaysidle apps/repos |
| [_system/templates/research/](_system/templates/research/) | Copy-from scaffolds (inbox, session, brief, …) |
| [_system/config/agy-vault-bootstrap.md](_system/config/agy-vault-bootstrap.md) | Paste-ready **agy** orchestrator prompt |

**Add a catalog entry:** duplicate a file under `_system/templates/catalog/`, set frontmatter (`name`, `status`, `repo_url`, `site_url`), add a row to `CATALOG.md`.

**Add a research topic:** copy `research/inbox-idea.md` → `inbox/YYYY-MM-DD-{slug}-idea.md`, then `session.md` and `moc.md` with the same `topic_slug`.

## Agent entrypoint

```bash
export VAULT_ROOT="$(pwd)"   # vault root after clone
```

1. Read `sessions/LATEST.md`
2. Read the active session under `sessions/`
3. Read `_system/reference/github-org-repositories.md` when linking repos
4. Never set `review_status: approved` or write under `projects/` without an explicit human **promote** instruction

## Safety

- No promotion without checklist + human approval
- Never delete under `sources/raw/`; mark `status: superseded` in index frontmatter
- Log promotions in `_audit/log.md`

## Related nodaysidle surfaces

| Surface | Repo | URL |
|---------|------|-----|
| Profile index | [nodaysidle](https://github.com/nodaysidle/nodaysidle) | — |
| Showcase | [nodaysidle-project-pages](https://github.com/nodaysidle/nodaysidle-project-pages) | https://nodaysidle-showcase-v2.vercel.app |
| Editorial portfolio build | [Portfolio](https://github.com/nodaysidle/Portfolio) | https://nodaysidle-portfolio-nine.vercel.app |

## License

MIT © [nodaysidle](https://github.com/nodaysidle)
