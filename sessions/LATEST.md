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
- [handoff 2026-10-15] **Operative code access tools added (`ab1420a` on main):** `actions/codebase.py` (#26) and `actions/run.py` (#27). Ground-truth inspection (ripgrep search, tree, line ranges, symbols, index, status) and sandboxed, allowlisted execution (git status/diff/log, build/test commands, timeouts, capping, secret redaction, audit log `~/.local/state/kurek/run_audit.log`). Tool count at runtime is now **27 active actions**. Tested live over Tailscale Android APK. Local commit `ab1420a` on `main` (`kurekizmo`).
- [vault] Open issues: #17 "Confirmed and executed" reported before anything ran; #18 service near MemoryHigh 512M; #20 open; #21 blocked on owner decisions (below).
- [vault] **Sandbox decision: NO sandbox.** Owner decided 2026-10-15. Do not re-propose sandboxing agent commands.
- [vault] Still pending owner: 2 skipped tests, 08:30 morning summary schedule, merge-gate `--comment` on PRs, idle watchdog schedule.

- [handoff 2026-10-15] **X post slot: Wed 2026-10-21 17:30 Europe/Ljubljana: CONFIRMED by owner (01:01).** REACH's v0.2.1 draft replaces the planned Kurek launch copy in that slot. Main post has no link; first reply links the v0.2.1 release and the apps card. See [[sessions/handoffs/2026-10-15-REACH]].
- [owner 2026-10-15 01:31] ✅ **Slot conflict resolved:** Adlof, via EO: "Wed Oct 21, 17:30, as planned". The Kurek v0.2.1 post stays on **Wed 21 Oct 17:30**. Thu 15 Oct 17:30 stays with the Cascade v3.1.0 thread. [[inbox/2026-10-15-kurek-v0-2-1-x-launch-moved-to-today-thu]] is marked `status: void`, and [[inbox/2026-10-15-x-launch-locked-kurek-v0-2-1-wed-21-oct-]] is marked `status: confirmed`. PR #5 is merged (`a60d93a`), so it isn't a blocker.
- [owner 2026-10-15 01:33] Owner's words, via EO: "1 soften to observed, 2 yes open the PR, 3 merge #6, 4 yes push all three."
- [handoff 2026-10-15] ✅ **Card claims fixed:** [nodaysidle-apps PR #6](https://github.com/nodaysidle/nodaysidle-apps/pull/6) was merged as `85eaf50` by EO and deployed to prod. ATLAS checked the live card at 01:41: it shows '25 tools' once, with no '24 tools' and no '0.8ms'.
- [handoff 2026-10-15] **Claims facts:** the tool count is **25** at runtime (verified by SHIP). "~0.8ms median" is **unproven**: it comes only from a mock-daemon bench and is never recorded by CI. Don't quote latency or trigger numbers anywhere. "~450MB peak RAM" is stated only as "observed". Stale prose remains in kureksistant `README.md` (128/135/140), `AGENTS.md:58` and `CHANGELOG.md:61`. See [[sessions/handoffs/2026-10-15-SHIP]].
- [owner 2026-10-15 01:42] Owner's words, via EO: "Merge both #7 and #22"
- [handoff 2026-10-15] ✅ **RAM claim softened:** [nodaysidle-apps PR #7](https://github.com/nodaysidle/nodaysidle-apps/pull/7) was merged as `6ff1968` and deployed to prod. ATLAS checked the live card at 01:45: it reads "~450MB peak RAM observed with Whisper loaded". Posts should call it observed too.
- [handoff 2026-10-15] ✅ **kureksistant docs fixed:** [PR #22](https://github.com/nodaysidle/kureksistant/pull/22) was merged as `149d2c5` (docs only: 25 tools; `bench_trigger.py` is an informational mock-daemon benchmark, no 0.8ms). The merge gate passed before the merge. The live kurek service was untouched. The local `kurekizmo` checkout isn't synced to `149d2c5`, which isn't needed for docs.
- [vault] Kurek card/docs claims: **all closed** (2026-10-15 01:42). No pending owner items here.
- [handoff 2026-10-15] ✅ **Apps `#kurek` card is on v0.2.1:** [nodaysidle-apps PR #5](https://github.com/nodaysidle/nodaysidle-apps/pull/5) was merged as `a60d93a` with owner OK (01:16) and the Vercel prod deploy succeeded. The live card shows the v0.2.1 tag, tarball and SHA256SUMS, with no v0.2.0 or `.apk` links. The card gap is closed. REACH's first reply can link the card. See [[sessions/handoffs/2026-10-15-EO]].
- [handoff 2026-10-15] Clip for the post: `/workspace/clips/kurek-remote/kurek-remote-v021.mp4` (+ `kurek-remote-v021.gif`) on the Grok Bot box, with the end card fixed ("Debug APK: download from the v0.2.1 release"). The originals `kurek-remote.mp4/.gif` are kept but stale. Real phone+PC footage is still pending from the owner. See [[sessions/handoffs/2026-10-15-REEL]].

### Cascade (nodaysidle-cascade-v3), today's X slot
- [handoff 2026-10-15] **X post: Thu 2026-10-15 17:30 Europe/Ljubljana**, Cascade v3.1.0 (Latest; tag `2bf0e8c`; assets: aarch64 DMG, AppImage, deb, linux tar.gz; MIT). REACH drafted it: main post with no link; first reply links the apps card [nodaysidle-apps #cascade](https://nodaysidle-apps.vercel.app/#cascade), which resolves and matches v3.1.0. Drafts only. See [[sessions/handoffs/2026-10-15-REACH]].
- [handoff 2026-10-15] Reddit draft for r/SideProject, Thu ~18:30 or Sat 17 Oct US morning. `@OWNER` confirms the subreddit and timing.
- [handoff 2026-10-15] Clip: `/workspace/clips/cascade/cascade.mp4` (11.4 s, 1920x1080) + `cascade.gif` on the Grok Bot box. It's real footage of the v3.1.0 AppImage, with a card reading "v3.1.0 · macOS + Linux · MIT". No documents are generated in it (that needs API keys).
- [handoff 2026-10-15] **Use `cascade-v2.mp4` / `cascade-v2.gif`** for 17:30 (re-captioned "Five doc tabs", approved 02:11; originals kept). Copy is limited to what's on screen, with no claim of generation or a live demo (owner, 02:08/02:11). The final draft is in the new standing format at [[briefs/x-drafts/2026-10-15-cascade]]. `@OWNER` picks the main post or a variant. Open: whether to record a run with keys that clicks Generate, for real proof.
- [handoff 2026-10-15] README check (SHIP): it has a direct DMG link (README:94) and SHA-256 for the AppImage, deb and tar.gz (README:130-136). ⚠️ Gaps: no DMG checksum, and the Linux links go to the tag page, not direct asset URLs. Optional owner decision to fix them. ✅ **Closed** by cascade-v3 #5 (`3edd3cc`, merged 02:29).
- [handoff 2026-10-15] Claims left out of the copy (unverified in the notes): speed claims and "one request". Verified stacks: SwiftUI desktop, SwiftUI menu bar, Tauri 2. Android and Astro are not verified yet.

### README sweep, batch 1 (direct download links + SHA-256)
- [owner 2026-10-15] Plan approved at 02:13 ("Approve all 5, Kurek APK wording as SHIP recommends"). Plan: [[briefs/draft/readme-sweep-brief-v1]]. Merges approved at 02:29, Alan via EO: "Merge Cascade #5, Sonora #3, Browser #5 and nodaysrammar #3 now".
- [handoff 2026-10-15] ✅ **Merged** by EO (squash). ATLAS checked via gh at 02:30:
  - nodaysidle-cascade-v3 [#5](https://github.com/nodaysidle/nodaysidle-cascade-v3/pull/5) as `3edd3cc` (DMG SHA-256 + direct Linux links, v3.1.0). This closes the Cascade README gaps before today's 17:30 post.
  - nodaysidle-sonora [#3](https://github.com/nodaysidle/nodaysidle-sonora/pull/3) as `f8b45ba` (SHA-256 table + direct Linux links, v0.1.1).
  - nodaysidle-browser-linux [#5](https://github.com/nodaysidle/nodaysidle-browser-linux/pull/5) as `ca1bc3e` (v0.2.0 AppImage SHA-256).
  - nodaysrammar [#3](https://github.com/nodaysidle/nodaysrammar/pull/3) as `1de303b` (direct v1.0.1 links + SHA-256).
- [handoff 2026-10-15] ✅ **kureksistant [#23](https://github.com/nodaysidle/kureksistant/pull/23) merged** as `e5341b7` (head `b8d18f0`; Alan at 02:30: "yes to both"). README: v0.2.1 bundle + a note that the debug APK is attached to the release (no direct APK link). The gate FAILED at `802d810` (Codex: `sha256sum -c --ignore-missing` silently skips a missing tarball). SHIP fixed it with a grep-filtered SHA256SUMS check + a pinned hash, chained with &&. At `b8d18f0`, verify passed and the gate PASSED (codex and agy both said MERGE). **Batch 1: 5/5 merged.**
- [handoff 2026-10-15 02:27] ⚠️ **Unreviewed local Kurek change, live on the PC:** an entry in the SHIP handoff file (credited to Antigravity in the wiki) adds tools #26 `codebase` and #27 `run` (an allowlisted command runner), committed as `ab1420a` on the local `kurekizmo` main. Not pushed, no PR, no merge gate. It **set `KUREK_REMOTE_ALLOW_EXEC=1` in `.env`** and restarted `kurek.service`, so remote exec from Tailscale devices is now ON. That reverses the PR #11 default (remote shell/code blocked). No quoted owner approval found. The tool count is now 27 locally; public v0.2.1 and the apps card say 25 and are still correct for the release. Real Tailscale IPs in the entry were redacted by ATLAS.
- [vault] **Owner decisions:** (a) keep or revert `KUREK_REMOTE_ALLOW_EXEC=1`; (b) whether `ab1420a` goes through a PR + merge gate. SHIP is approved (02:30) to fix the `--ignore-missing` line in the v0.2.1 release notes; still to be done.
- [vault] Deferred: whisper-bar and shareguard (macOS-only, already have a direct DMG link + SHA-256).

### nodaysidle-browser-linux
- [handoff 2026-10-15] v0.2.0 released 2026-10-14 (Latest; PRs #3 `88e6074` and #4 `2d96195`). It ships an AppImage that needs GTK 3 + WebKitGTK 4.1. Screen-reader output is covered by unit tests only.
- [owner 2026-10-15 01:50] ✅ **Reinstall/update owner-confirmed.** Adlof, relayed by Fabić via EO: "i did reoptimize it and today i posted it on X the newest version". (He installed v0.2.0 on Oct 14; "works perfectly".)
- [vault] **Still open: local WIP cleanup.** ATLAS checked at 01:55 (git only, nothing launched): the local repo `nodaysidle-browser-linux` is still at `a813e70` with 20 uncommitted entries. A backup exists in `~/dev/nodaysidle/backups/`. Owner decides.

### prompt-optimizer
- [vault] Internal tool. Audit fixes are live on Vercel but **unmerged**: source lives only in OpenCode worktree `~/.local/share/opencode/worktree/6f72e1/optimizer-audit-fixes` (branch `audit/nodaysidle-logo`); `master` is still `818eed1`. See [[2026-10-14-prompt-optimizer-session]]. Low promo priority.

### Official sites
- [vault] Official: **Portfolio** and **nodaysidle-apps**.
- [vault] Stale: `nodaysidle-project-pages`, showcase-v2. Do not cite them as current or link them in posts.

### Promo assets
- [vault] Clips (MP4) are for **X posts** (REACH/REEL). GIFs are for **repo READMEs**. They sit on the **Grok Bot box** under `/workspace/clips/<app>/` (corrected 2026-10-15; this line used to say "owner's computer") and are **not yet committed** to any app repo.

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
- 2026-10-15 01:45 (ATLAS): folded the owner's 01:42 approval: #7 merged (`6ff1968`), kureksistant #22 merged (`149d2c5`). The claims items are closed. Still open: browser-linux reinstall/WIP cleanup.
- 2026-10-15 01:55 (ATLAS): folded the sync-test entries from EO, REACH, REEL and SHIP. Added the Cascade Thu 17:30 section, recorded the owner's browser-linux confirmation (01:50), and corrected where the clips are kept. Still open: browser-linux WIP cleanup; the Cascade README gaps (optional); confirming the Reddit timing.
- 2026-10-15 02:30 (ATLAS): logged README sweep batch 1 (4 merged, kureksistant #23 open, gate PASS at `b8d18f0`). Folded the REACH/REEL Cascade copy and clip-v2 entries. Update: #23 merged (`e5341b7`), batch 1 5/5. Still open: the release-notes fix (approved, SHIP doing it), the KUREK_REMOTE_ALLOW_EXEC decision, the Cascade post pick, and the browser-linux WIP cleanup.

## Rule for every agent
Read this file at the start of every task. When you finish, write `sessions/handoffs/<YYYY-MM-DD>-<AGENT>.md`. Only ATLAS edits this file (owner may too).
