# Sources

- **`index/`** — one Markdown stub per source (`source_id`, URL, accessed date, links to raw).
- **`raw/`** — web, docs, pdf, local captures. Never delete; supersede in index frontmatter.

Template: `_system/templates/research/source-index.md`.

Example layout (create on first ingest):

```text
sources/
├── index/src-20261007-example.md
└── raw/web/src-20261007-example-page.md
```

## Ingested sources

### nodaysidle-browser-linux (2026-10-07)

| Source | Kind | Tier | Note |
|--------|------|------|------|
| [[index/src-20261007-2d7bab4-browser-linux-readme]] | repo-readme | primary | README |
| [[index/src-20261007-030f677-browser-linux-audit]] | local-note | primary | `agenthandoff_audit.md` (no `AUDIT.md` in repo) |
| [[index/src-20261007-6223dc7-browser-linux-agent-handoff]] | local-note | secondary | ⚠️ **unreliable** — known partly wrong |
| [[index/src-20261007-e79ab38-browser-linux-appimage]] | official-doc | primary | `docs/APPIMAGE.md` |
| [[index/src-20261007-1764cc7-browser-linux-release-notes-v0-1-0]] | official-doc | primary | v0.1.0 release notes |
| [[index/src-20261007-e02f632-browser-linux-git-log]] | repo-history | primary | `git log --oneline` at `2fffaab` |

### kureksistant (local folder `../kurekizmo`, upstream repo `kureksistant`)

| Source | Kind | Tier | Note |
|--------|------|------|------|
| [[index/src-20261008-ae52ff2-kureksistant-readme]] | repo-readme | primary | **Active** — README at `d863922` (~333MB, 24 tools, CC BY-NC 4.0) |
| [[index/src-20261008-88302c2-kureksistant-agents]] | local-note | primary | **Active** — AGENTS.md at `d863922` (repo-relative, Muse Memory) |
| [[index/src-20261008-f95e626-kureksistant-sha256sums-v0-1-0]] | release-artifact | primary | **Active** — re-cut v0.1.0 release SHA256SUMS.txt (`a4085d73…`) |
| [[index/src-20261007-c1c7fe9-kureksistant-readme]] | repo-readme | primary | *Superseded* by `src-20261008-ae52ff2` (pre-audit ~55MB claim) |
| [[index/src-20261007-459dbb7-kureksistant-agents]] | local-note | secondary | *Superseded* by `src-20261008-88302c2` (JARVIS-era paths) |
| [[index/src-20261007-46ff002-kureksistant-release-notes-v0-1-0]] | official-doc | primary | `dist/RELEASE_NOTES.md` (v0.1.0 initial) |
| [[index/src-20261007-e1be179-kureksistant-sha256sums-v0-1-0]] | release-artifact | primary | *Superseded* by `src-20261008-f95e626` (re-cut release asset) |
| [[index/src-20261007-2aa023e-kureksistant-git-log]] | repo-history | primary | `git log --oneline` at `b072178` |

### nodaysidle-cascade-v3 (2026-10-07; cloned to `../nodaysidle-cascade-v3`, HEAD `20f7098`)

| Source | Kind | Tier | Note |
|--------|------|------|------|
| [[index/src-20261007-305a501-cascade-v3-readme]] | repo-readme | primary | README |
| [[index/src-20261007-c789017-cascade-v3-agents]] | local-note | primary | AGENTS.md |
| [[index/src-20261007-0937509-cascade-v3-design-spec-2026-08-29]] | official-doc | secondary | design spec 2026-08-29 |
| [[index/src-20261007-5351bd3-cascade-v3-github-releases]] | release-notes | primary | GitHub releases (API dump) |
| [[index/src-20261007-3f34f6c-cascade-v3-git-log]] | repo-history | primary | git log |

### nodaysidle-sonora (2026-10-07; cloned to `../nodaysidle-sonora`, HEAD `b2f9a2d`)

| Source | Kind | Tier | Note |
|--------|------|------|------|
| [[index/src-20261007-fa15609-nodaysidle-sonora-readme]] | repo-readme | primary | README |
| [[index/src-20261007-8d170be-nodaysidle-sonora-agents]] | local-note | primary | root AGENTS.md (source of truth) |
| [[index/src-20261007-7396417-nodaysidle-sonora-docs-agents]] | local-note | secondary | docs/AGENTS.md (= docs/AGENT.md) |
| [[index/src-20261007-02f8cee-nodaysidle-sonora-prd]] | official-doc | secondary | PRD |
| [[index/src-20261007-72f03ba-nodaysidle-sonora-ard]] | official-doc | secondary | ARD |
| [[index/src-20261007-6bd63ba-nodaysidle-sonora-trd]] | official-doc | secondary | TRD |
| [[index/src-20261007-db207e8-nodaysidle-sonora-tasks]] | official-doc | secondary | TASKS (historical) |
| [[index/src-20261007-c7ca7e6-nodaysidle-sonora-claude]] | local-note | secondary | docs/CLAUDE.md |
| [[index/src-20261007-0876748-nodaysidle-sonora-codemap]] | local-note | secondary | codemap |
| [[index/src-20261007-f4f351a-nodaysidle-sonora-plan-librespot]] | official-doc | secondary | librespot plan |
| [[index/src-20261007-91e96aa-nodaysidle-sonora-spec-librespot]] | official-doc | secondary | librespot design spec |
| [[index/src-20261007-4ac28d4-nodaysidle-sonora-github-releases]] | release-notes | primary | GitHub releases (API dump) |
| [[index/src-20261007-7234e1e-nodaysidle-sonora-git-log]] | repo-history | primary | git log |

### synapse-notes (2026-10-07; cloned to `../synapse-notes`, HEAD `a6e10fa`)

| Source | Kind | Tier | Note |
|--------|------|------|------|
| [[index/src-20261007-77e0f33-synapse-notes-readme]] | repo-readme | primary | README |
| [[index/src-20261007-67b1886-synapse-notes-agents]] | local-note | primary | root AGENTS.md |
| [[index/src-20261007-5fa8138-synapse-notes-docs-agents]] | local-note | secondary | docs/AGENTS.md |
| [[index/src-20261007-ce75492-synapse-notes-docs-readme]] | local-note | secondary | docs/README.md |
| [[index/src-20261007-edbf2ff-synapse-notes-internal-agents]] | local-note | secondary | docs/internal/AGENTS.md |
| [[index/src-20261007-28f622a-synapse-notes-internal-readme]] | local-note | secondary | docs/internal/README.md |
| [[index/src-20261007-6c69203-synapse-notes-internal-codemap]] | local-note | secondary | internal codemap |
| [[index/src-20261007-e444638-synapse-notes-plan-redesign-2026-01-25]] | official-doc | secondary | redesign plan 2026-01-25 |
| [[index/src-20261007-fd8a340-synapse-notes-plan-implementation-2026-01-25]] | official-doc | secondary | implementation plan 2026-01-25 |
| [[index/src-20261007-f818afc-synapse-notes-github-releases]] | release-notes | primary | GitHub releases (API dump) |
| [[index/src-20261007-ec9ad0c-synapse-notes-git-log]] | repo-history | primary | git log |
