---
type: session-pointer
updated: 2026-10-15
---

# Active session — read this first

Resume here: [[2026-10-08-kureksistant-session]] (primary thread: Kurek)
Umbrella for vault-wide work: [[2026-10-07-vault-operations-session]]
Handoffs between agents: `sessions/handoffs/` (see [[sessions/handoffs/README]])

## Current true state (2026-10-15)

### Kurek (kureksistant) — primary focus
- [vault] v0.2.1 released 2026-10-14 (target `3761c78`), PC voice control incl. remote Android APK over Tailscale.
- [vault] Open issues: #17 "Confirmed and executed" reported before anything ran; #18 service near MemoryHigh 512M; #20 open; #21 blocked on owner decisions (below).
- [vault] **Sandbox decision: NO sandbox.** Owner decided 2026-10-15. Do not re-propose sandboxing agent commands.
- [vault] Still pending owner: 2 skipped tests, 08:30 morning summary schedule, merge-gate `--comment` on PRs, idle watchdog schedule.

- [handoff 2026-10-15] **X post slot: Wed 2026-10-21 17:30 Europe/Ljubljana: CONFIRMED by owner (01:01).** REACH's v0.2.1 draft replaces the planned Kurek launch copy in that slot. Main post has no link; first reply links the v0.2.1 release and the apps card. See [[sessions/handoffs/2026-10-15-REACH]].
- [handoff 2026-10-15] ✅ **Apps `#kurek` card is on v0.2.1:** [nodaysidle-apps PR #5](https://github.com/nodaysidle/nodaysidle-apps/pull/5) was merged as `a60d93a` with owner OK (01:16) and the Vercel prod deploy succeeded. The live card shows the v0.2.1 tag, tarball and SHA256SUMS, with no v0.2.0 or `.apk` links. The card gap is closed. REACH's first reply can link the card. See [[sessions/handoffs/2026-10-15-EO]].
- [handoff 2026-10-15] Clip for the post: `/workspace/clips/kurek-remote/kurek-remote-v021.mp4` (+ `kurek-remote-v021.gif`) on the Grok Bot box, with the end card fixed ("Debug APK: download from the v0.2.1 release"). The originals `kurek-remote.mp4/.gif` are kept but stale. Real phone+PC footage is still pending from the owner. See [[sessions/handoffs/2026-10-15-REEL]].

### nodaysidle-browser-linux
- [handoff 2026-10-15] v0.2.0 released 2026-10-14 (Latest; PRs #3 `88e6074` and #4 `2d96195`). It ships an AppImage that needs GTK 3 + WebKitGTK 4.1. Screen-reader output is covered by unit tests only. The installed PC build still shows About 0.1.0. Owner to decide: reinstall from v0.2.0, and clean up the local WIP (backed up in `~/dev/nodaysidle/backups/`).

### prompt-optimizer
- [vault] Internal tool. Audit fixes are live on Vercel but **unmerged**: source lives only in OpenCode worktree `~/.local/share/opencode/worktree/6f72e1/optimizer-audit-fixes` (branch `audit/nodaysidle-logo`); `master` is still `818eed1`. See [[2026-10-14-prompt-optimizer-session]]. Low promo priority.

### Official sites
- [vault] Official: **Portfolio** and **nodaysidle-apps**.
- [vault] Stale: `nodaysidle-project-pages`, showcase-v2. Do not cite them as current or link them in posts.

### Promo assets
- [vault] Clips (MP4) are for **X posts** (REACH/REEL). GIFs are for **repo READMEs**. Both currently sit on the owner's computer and are **not yet committed** to any app repo.

### Parked candidates (no push since mid-September; not archived, owner decides)
- hermes-agent, nodaysidle-flowstate, nodaysidian, BrewLedger, nodaysidle-cloudscribe (last push 2026-07-23), hermes-gpt (07-25), nodaysidle-project-pages (09-06, stale site).
- Watch list (last push 2026-09-17..24): excalidays, pocket-drafts, nodaysidle-vois, nodaysidle-voice-anywhere-v2, batchrename-pro, small-count, nodaysidle-cistilka, nodaysrecording, scribeflowpro, cliprail, nodaysidle-browser, nodaystypst, nodaysidle-lumiere, cursorpad, monospace-notes.
- Source: GitHub `pushed_at` checked 2026-10-15.

## Handoffs folded

- 2026-10-15 00:43 (ATLAS): folded [[sessions/handoffs/2026-10-15-EO]], [[sessions/handoffs/2026-10-15-REACH]], [[sessions/handoffs/2026-10-15-REEL]]. Owner decisions (1) Oct 21 slot, (2) card update, (3) end-card re-render: **all resolved, approved 01:01.**
- 2026-10-15 01:07 (ATLAS): folded the follow-ups in [[sessions/handoffs/2026-10-15-EO]], [[sessions/handoffs/2026-10-15-SHIP]] and [[sessions/handoffs/2026-10-15-REEL]]. Still open: browser-linux reinstall/WIP cleanup.
- 2026-10-15 01:16 (ATLAS): folded EO's PR #5 merge entry. The card gap is closed; apps main is `a60d93a`.

## Rule for every agent
Read this file at the start of every task. When you finish, write `sessions/handoffs/<YYYY-MM-DD>-<AGENT>.md`. Only ATLAS edits this file (owner may too).
