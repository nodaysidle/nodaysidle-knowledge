---
type: reference
source_url: https://github.com/nodaysidle?tab=repositories
synced: 2026-10-07
public_repo_count: 31
tags:
  - reference
  - github
---

# nodaysidle GitHub repositories

Canonical list from the [public repositories tab](https://github.com/nodaysidle?tab=repositories). Re-sync with:

```bash
curl -s "https://api.github.com/users/nodaysidle/repos?per_page=100&type=owner" \
  | jq -r '.[] | "- [\(.name)](\(.html_url))" + (if .homepage then " — " + .homepage else "" end)' | sort
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
- [monospace-notes](https://github.com/nodaysidle/monospace-notes)
- [nodaysidian](https://github.com/nodaysidle/nodaysidian)
- [nodaysidle](https://github.com/nodaysidle/nodaysidle) — profile README and public project index
- [nodaysidle-browser](https://github.com/nodaysidle/nodaysidle-browser)
- [nodaysidle-cascade-v3](https://github.com/nodaysidle/nodaysidle-cascade-v3)
- [nodaysidle-cistilka](https://github.com/nodaysidle/nodaysidle-cistilka)
- [nodaysidle-cloudscribe](https://github.com/nodaysidle/nodaysidle-cloudscribe)
- [nodaysidle-echocore-pro](https://github.com/nodaysidle/nodaysidle-echocore-pro)
- [nodaysidle-flowstate](https://github.com/nodaysidle/nodaysidle-flowstate)
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
- [scribeflowpro](https://github.com/nodaysidle/scribeflowpro)
- [small-count](https://github.com/nodaysidle/small-count)
- [synapse-notes](https://github.com/nodaysidle/synapse-notes)
- [whisper-bar](https://github.com/nodaysidle/whisper-bar)

## Local workspace, not on GitHub (yet)

These exist under `/home/arch/dev/nodaysidle/` with verified Vercel or local builds; **no matching public repo** as of 2026-10-07:

| Local folder | Product | Live site |
|--------------|---------|-----------|
| `markdown-helper` | AI Rules Builder | https://markdown-helper.vercel.app |
| `skill-gallery` | Agent Gallery | https://agent-gallery.vercel.app |
| `Portfolio` | Editorial portfolio (build from profile JSON) | https://nodaysidle-portfolio-nine.vercel.app |
| `nodaysidle-browser-linux` | Linux WebKit browser | releases pending public repo |

When published, add rows to `catalog/` and move entries into the list above.
