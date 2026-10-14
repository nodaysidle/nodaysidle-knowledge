---
type: catalog-entry
name: Prompt Optimizer
status: completed
short_description: Preservation-first desktop prompt workbench with DeepSeek Flash/Pro, app-server heuristics, explicit external diagnostics, editable candidates, frozen diff, paired text evaluation and versioned visual prompting profiles.
updated: 2026-10-14
deployed_commit: 03aac470b7a07601d0bf8aaee32bca3f479fd894
source_branch: audit/nodaysidle-logo
repo_url: https://github.com/nodaysidle/nodaysidle-prompt-optimizer
site_url: https://nodaysidle-prompt-optimizer.vercel.app
local_path: ../nodaysidle-prompt-optimizer
stack:
  - Next.js 16
  - React 19
  - Tailwind CSS v4
  - Microsoft-Decision-1 (OpenRouter)
  - TypeSafe Jev
tags:
  - catalog
  - web
  - ai-tools
  - video-gen
  - decision-models
---

# Prompt Optimizer

[vault] Desktop-first editor for user, system, image and video prompt text. Minimal/structured/creative modes preserve constraints without missing-context placeholders. Default diagnostics are app-server heuristics with no AI-provider transmission; OpenRouter/TypeSafe are explicit options. DeepSeek Flash/Pro rewrites, editable candidates, frozen-original diff, actionable questions, versioned history and paired text evaluation are implemented. Visual profiles are guidance only, not image/video rendering integrations. Header uses the owner's silver N logo.

- **Repo:** [github.com/nodaysidle/nodaysidle-prompt-optimizer](https://github.com/nodaysidle/nodaysidle-prompt-optimizer)
- **Local clone:** `../nodaysidle-prompt-optimizer`
- **Live:** [nodaysidle-prompt-optimizer.vercel.app](https://nodaysidle-prompt-optimizer.vercel.app)
- **Concept Note:** [[wiki/concepts/nodaysidle-prompt-optimizer-overview]]
- **Change record:** [[artifacts/prompt-optimizer/audit-fixes-and-deploy-2026-10-14]]
- **Resume:** [[sessions/2026-10-14-prompt-optimizer-session]]
- **Deployed source:** `03aac47` in `/home/arch/.local/share/opencode/worktree/6f72e1/optimizer-audit-fixes`, retained by local `audit/nodaysidle-logo`; not merged/pushed. Original `master` remains `818eed1`.
- **Verification:** 90 unit tests, 5 mocked browser tests, lint/typecheck/build and production audit passed locally. No paid-model quality benchmark; no GitHub CI run claimed.
- **Credentials:** BYOK or explicit legacy-key import in Settings; no production server variables configured at deployment check. Shared server keys require owner configuration and private access token.
