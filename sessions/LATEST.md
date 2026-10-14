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
- [owner 2026-10-15 01:31] ✅ **Slot conflict resolved:** Adlof, via EO: "Wed Oct 21, 17:30, as planned". The Kurek v0.2.1 post stays on **Wed 21 Oct 17:30**. Thu 15 Oct 17:30 stays with the Cascade v3.1.0 thread. [[inbox/2026-10-15-kurek-v0-2-1-x-launch-moved-to-today-thu]] is marked `status: void`, and [[inbox/2026-10-15-x-launch-locked-kurek-v0-2-1-wed-21-oct-]] is marked `status: confirmed`. PR #5 is merged (`a60d93a`), so it isn't a blocker.
- [owner 2026-10-15 01:33] Owner's words, via EO: "1 soften to observed, 2 yes open the PR, 3 merge #6, 4 yes push all three."
- [handoff 2026-10-15] ✅ **Card claims fixed:** [nodaysidle-apps PR #6](https://github.com/nodaysidle/nodaysidle-apps/pull/6) was merged as `85eaf50` by EO and deployed to prod. ATLAS checked the live card at 01:41: it shows '25 tools' once, with no '24 tools' and no '0.8ms'.
- [handoff 2026-10-15] **Claims facts:** the tool count is **25** at runtime (verified by SHIP). "~0.8ms median" is **unproven**: it comes only from a mock-daemon bench and is never recorded by CI. Don't quote latency or trigger numbers anywhere. "~450MB peak RAM" is stated only as "observed". Stale prose remains in kureksistant `README.md` (128/135/140), `AGENTS.md:58` and `CHANGELOG.md:61`. See [[sessions/handoffs/2026-10-15-SHIP]].
- [handoff 2026-10-15] **RAM claim PR open, not merged:** [nodaysidle-apps PR #7](https://github.com/nodaysidle/nodaysidle-apps/pull/7) (`a5ed687`) changes the bullet to "~450MB peak RAM observed with Whisper loaded". The live card still has the old wording. The source is only an observation (kureksistant AGENTS.md:3, CHANGELOG.md:60), so posts should call it observed too.
- [handoff 2026-10-15] **kureksistant docs PR open, not merged:** [kureksistant PR #22](https://github.com/nodaysidle/kureksistant/pull/22) (`eeb8b66`, docs only) sets 25 tools and describes `bench_trigger.py` as an informational mock-daemon benchmark, with no 0.8ms. The `[0.2.0]` changelog entry is kept as history. CI is green. **Merge gate PASSED**: verify passed on the 2nd run (the 1st failed `daemon_auth` because the test daemon was slow to start, a flake), and codex and agy both said MERGE on `eeb8b66`. The live kurek service was untouched.
- [vault] **Still pending owner:** merge nodaysidle-apps PR #7; merge kureksistant PR #22. The ~450MB and docs-PR decisions are resolved (01:33).
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

## Team rules (AGENTS.md `b586c41`, from 2026-10-15 01:24)
1. Sign every commit with an `Agent: <NAME>` trailer.
2. Every relayed approval quotes the owner's exact words and the time.
3. Every handoff entry fills all five fields: Task / Did / Facts for others / Needs / Status.
4. A question such as "what do you recommend?" is never a yes.

## Handoffs folded

- 2026-10-15 00:43 (ATLAS): folded [[sessions/handoffs/2026-10-15-EO]], [[sessions/handoffs/2026-10-15-REACH]], [[sessions/handoffs/2026-10-15-REEL]]. Owner decisions (1) Oct 21 slot, (2) card update, (3) end-card re-render: **all resolved, approved 01:01.**
- 2026-10-15 01:07 (ATLAS): folded the follow-ups in [[sessions/handoffs/2026-10-15-EO]], [[sessions/handoffs/2026-10-15-SHIP]] and [[sessions/handoffs/2026-10-15-REEL]]. Still open: browser-linux reinstall/WIP cleanup.
- 2026-10-15 01:16 (ATLAS): folded EO's PR #5 merge entry. The card gap is closed; apps main is `a60d93a`.
- 2026-10-15 01:30 (ATLAS): folded EO's team-rules section and SHIP's card-claims entry (PR #6). Flagged the conflicting inbox slot captures. Still open: PR #6 merge, the ~450MB claim, a kureksistant docs PR, and browser-linux reinstall/WIP cleanup.
- 2026-10-15 01:31 (ATLAS): recorded the owner's slot decision (01:31, quoted) and marked the two inbox captures void/confirmed. Superseded at 01:33, see below.
- 2026-10-15 01:41 (ATLAS): folded the owner's 01:33 answers: PR #6 merged (`85eaf50`), PR #7 and kureksistant PR #22 opened, merge gate PASS on #22, vault push done (`978bb0f`). Still open: merge #7, merge #22, and browser-linux reinstall/WIP cleanup.

## Rule for every agent
Read this file at the start of every task. When you finish, write `sessions/handoffs/<YYYY-MM-DD>-<AGENT>.md`. Only ATLAS edits this file (owner may too).
