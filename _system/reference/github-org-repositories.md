---
type: reference
source_url: https://github.com/nodaysidle?tab=repositories
synced: 2026-10-07
public_repo_count: 36
tags:
  - reference
  - github
---

# nodaysidle GitHub repositories

Canonical list from the [public repositories tab](https://github.com/nodaysidle?tab=repositories). Re-sync with:

```bash
curl -s "https://api.github.com/users/nodaysidle/repos?per_page=100&type=owner" \
  | jq -r '.[] | "- [\(.name)](\(.html_url))" + (if .homepage != null and .homepage != "" then " — " + .homepage else "" end)' | sort
```

## Published on GitHub

- [batchrename-pro](https://github.com/nodaysidle/batchrename-pro)
- [BrewLedger](https://github.com/nodaysidle/BrewLedger)
- [cliprail](https://github.com/nodaysidle/cliprail)
- [cursorpad](https://github.com/nodaysidle/cursorpad)
- [excalidays](https://github.com/nodaysidle/excalidays)
- [hermes-agent](https://github.com/nodaysidle/hermes-agent) — https://hermes-agent.nousresearch.com
- [hermes-gpt](https://github.com/nodaysidle/hermes-gpt) — https://hermes-gpt.tonysimons.dev
- [kureksistant](https://github.com/nodaysidle/kureksistant) — https://github.com/nodaysidle/kureksistant
- [markdown-helper](https://github.com/nodaysidle/markdown-helper) — https://markdown-helper.vercel.app
- [monospace-notes](https://github.com/nodaysidle/monospace-notes)
- [nodaysidian](https://github.com/nodaysidle/nodaysidian)
- [nodaysidle](https://github.com/nodaysidle/nodaysidle) — profile README and public project index
- [nodaysidle-browser](https://github.com/nodaysidle/nodaysidle-browser)
- [nodaysidle-browser-linux](https://github.com/nodaysidle/nodaysidle-browser-linux)
- [nodaysidle-cascade-v3](https://github.com/nodaysidle/nodaysidle-cascade-v3)
- [nodaysidle-cistilka](https://github.com/nodaysidle/nodaysidle-cistilka)
- [nodaysidle-cloudscribe](https://github.com/nodaysidle/nodaysidle-cloudscribe)
- [nodaysidle-echocore-pro](https://github.com/nodaysidle/nodaysidle-echocore-pro)
- [nodaysidle-flowstate](https://github.com/nodaysidle/nodaysidle-flowstate)
- [nodaysidle-knowledge](https://github.com/nodaysidle/nodaysidle-knowledge) — research vault (this repo)
- [nodaysidle-lumiere](https://github.com/nodaysidle/nodaysidle-lumiere)
- [nodaysidle-project-pages](https://github.com/nodaysidle/nodaysidle-project-pages) — https://nodaysidle-showcase-v2.vercel.app
- [nodaysidle-prompt-optimizer](https://github.com/nodaysidle/nodaysidle-prompt-optimizer)
- [nodaysidle-shareguard](https://github.com/nodaysidle/nodaysidle-shareguard)
- [nodaysidle-sonora](https://github.com/nodaysidle/nodaysidle-sonora)
- [nodaysidle-voice-anywhere-v2](https://github.com/nodaysidle/nodaysidle-voice-anywhere-v2)
- [nodaysidle-vois](https://github.com/nodaysidle/nodaysidle-vois)
- [nodaysrecording](https://github.com/nodaysidle/nodaysrecording)
- [nodaystypst](https://github.com/nodaysidle/nodaystypst)
- [pocket-drafts](https://github.com/nodaysidle/pocket-drafts)
- [Portfolio](https://github.com/nodaysidle/Portfolio) — https://nodaysidle-portfolio-nine.vercel.app
- [scribeflowpro](https://github.com/nodaysidle/scribeflowpro)
- [skill-gallery](https://github.com/nodaysidle/skill-gallery) — https://agent-gallery.vercel.app
- [small-count](https://github.com/nodaysidle/small-count)
- [synapse-notes](https://github.com/nodaysidle/synapse-notes)
- [whisper-bar](https://github.com/nodaysidle/whisper-bar)

## Local clones (sibling monorepo)

When using a multi-repo checkout under `~/dev/nodaysidle/`, catalog `local_path: ../{folder}` may differ from the GitHub repo name (e.g. `kurekizmo` → `kureksistant`).
