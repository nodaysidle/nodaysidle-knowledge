# Cascade v3.1.0: big-launch proposal (DRAFT)
Prepared by REACH, Fri 16 Oct 2026, 21:30 CEST. Drafts only. Nothing here gets posted or scheduled, and no GitHub or Vercel edits are made. Alan posts everything himself.

**Status:** Cascade v3.1.0 is released but not promoted. The Thu 15 Oct X post did **not** go live, and the 15 Oct 14:10 approval is stale. Alan, 16 Oct 10:26: "cascade will be the big launch later." This proposal replaces the earlier stub.

**Sources used:** the vault (`sessions/LATEST.md` with the 21:11 ATLAS audit, `wiki/concepts/cascade-v3-overview.md`, `sources/raw/docs/*cascade-v3*`, the catalog, `briefs/x-drafts/2026-10-15-cascade.md`). Also the GitHub Releases API and README for github.com/nodaysidle/nodaysidle-cascade-v3 (read 16 Oct 21:28 CEST) and https://nodaysidle-apps.vercel.app (card re-checked 15 Oct per the x-draft). Project-pages and showcase-v2 were not used.

## 0. Verified fact sheet (the only claims allowed in copy)
| Claim | Source | Status |
|---|---|---|
| Takes one software idea plus one stack and produces five docs: PRD, ARD, TRD, TASKS, AGENTS | v3.1.0 release notes, README | verified |
| Three stacks verified with real apps built from Cascade packets and "checked by using them, not only by their tests": SwiftUI desktop (ReceiptShelf), SwiftUI menu bar (PinBoard, Murmur), Tauri 2 (PromptShelf) | v3.1.0 release notes | verified. Attribute it to the notes. |
| Android (Compose) and Astro are available but **not verified** | v3.1.0 release notes | verified. Say this every time stacks come up. |
| Verified stacks export a tested starter kit under `kit/` | v3.1.0 release notes | verified |
| One model request for product meaning (at most one repair). A local deterministic compiler owns IDs, files and the markdown bytes. Preview bytes equal export bytes. | README | verified |
| Needs the user's own AI provider credentials (DeepSeek, per the README badge and layer table). Credentials are held in memory only. No accounts, no telemetry. | README, overview | verified. **Must be disclosed:** it is not offline or free of API cost. |
| macOS Apple Silicon (DMG) plus Linux x86_64 (AppImage, .deb, tar.gz). No Windows, no Intel Mac. | release assets, hub card | verified |
| MIT | repo LICENSE, README | verified |
| README badge and tagline mention "Arch, Omarchy, Ubuntu, Debian" | README | **unverified** as tested distros. No Arch package is attached (the tar.gz is the generic one). Say "Linux x86_64" only. |
| Linux assets were built from `d79ec73` (after the tag commit `6294841`) | release body, overview | verified. Disclose it if anyone asks. |
| Speed, RAM/CPU, "~0.8ms", "studio-grade", "works with any agent" | none | **banned** |
| "My agents kept building the wrong thing" (personal opener) | none | **unverified until Alan confirms it is his own experience** |

Asset SHA-256 (GitHub API digests, 16 Oct 21:28): DMG `1aec1ffd…3d9` (11.6 MB) · tar.gz `f3e7693d…3b3` (6.9 MB) · AppImage `fe784421…ac4` (86.4 MB) · deb `5dddd77a…297e` (8.6 MB). These match the hub per the ATLAS 21:11 audit.

## 1. Recommended window
**Recommendation: Tue 27 Oct, 17:30 local (CET; clocks go back on Sun 25 Oct).** Fallback: Thu 29 Oct, 17:30.

Reasons:
- It avoids WhisperBar (Sat 17) and Kurek (Wed 21) and leaves a clean gap. Kurek gets its full T+1/T+2 before Cascade starts its teasers, so the two launches don't compete for the same 41 followers.
- At 3–4 posts a week, the week of 19 Oct already holds Kurek and maybe one other post. Cascade's teaser (T-2, Sun 25) and main post fit the next week without breaking pace.
- 17:30 CET on 27 Oct is 12:30 ET and 09:30 PT (the US is still on summer time until 1 Nov). That catches US working hours for Hacker News and Reddit, and it keeps Alan's proven 17:30 slot and the EO 13:45 packet cutoff.
- Tuesday is a strong weekday for Show HN and Reddit, and it leaves Wed–Fri to answer questions.
- It gives REEL and SHIP 7+ days for a real generation clip and the README fixes (section 4), which the 15 Oct package didn't have.

## 2. Channels
| Channel | Call | Reason |
|---|---|---|
| X thread (@kaly_ndi) | **Recommend** (anchor) | It's Alan's home channel. A main post with a clip, then replies covering the link, the verified stacks and the honesty notes. Expect roughly 100–250 impressions given 41 followers. The thread matters more as a public record than for reach. |
| Hacker News, Show HN | **Recommend** (main reach bet) | The audience is developers, and the deterministic-compiler angle ("one model call, local code owns the bytes") is the kind of design detail HN rewards. Downsides: it needs Alan present for 3–4 hours to answer comments, and HN will poke at the API-key dependency and the "verified" wording, so the copy has to be plain. Title draft: "Show HN: Cascade – one app idea to PRD/ARD/TRD/TASKS/AGENTS docs for coding agents". |
| Reddit r/SideProject | **Recommend** | Self-promotion is allowed there and builders are the audience. The 15 Oct draft (x-draft section 8) can be reused, with the opener gated. |
| Reddit r/ChatGPTCoding or r/ClaudeAI | **Recommend one, optional** (check its self-promo rules first) | These are agent-driven coders, which is the exact user. Post once, T+0 or T+1, without cross-posting the same text. |
| Reddit r/opensource, r/linux, r/macapps | **Skip** | r/linux is hostile to promotion. The macOS build is Apple Silicon only and the tool needs a paid API, which r/macapps tends to criticise. r/opensource adds little. |
| Product Hunt | **Skip for now** | 41 followers and no hunter network means a likely low-ranked launch that burns the one-time PH slot. Revisit once there's an audience or a v3.2. |
| Newsletter | Skip (none exists) | — |

## 3. Timeline (T-0 = Tue 27 Oct)
| Day | Date | What happens | Owner |
|---|---|---|---|
| T-7 | Tue 20 Oct | Alan answers the open questions (section 7). SHIP starts its checks (section 4). REEL scripts the hero clip. No public post (Kurek is Wed). | EO → Alan, SHIP, REEL |
| T-6 | Wed 21 Oct | Kurek 17:30 goes ahead untouched. Nothing about Cascade goes public. | — |
| T-5 | Thu 22 Oct | SHIP reports results, and any README PRs are **opened only with Alan's yes**. REEL raw capture of a real generation (needs Alan's key on his machine or a screen recording from him). | SHIP, REEL, Alan |
| T-4 | Fri 23 Oct | REACH writes the full packet: X thread, Show HN title and first comment, Reddit body. Claim check against section 0. | REACH |
| T-3 | Sat 24 Oct | REEL delivers its cuts with a frame audit. Alan approves the copy. | REEL, Alan |
| T-2 | Sun 25 Oct | Optional single teaser on X (text or a 6 s clip, no new claims), e.g. "Tuesday: the tool I use to write the spec before my agent writes code." Only if Alan wants a post that day. | Alan posts |
| T-1 | Mon 26 Oct | SHIP final pass (release Latest, SHAs, hub card live, README links). Packet frozen. Alan reads the HN etiquette notes. | SHIP, EO |
| T-0 | Tue 27 Oct | **13:45** final packet to EO. **17:30** X main post plus link reply. **~17:40** Show HN. **~18:00** r/SideProject. Alan answers comments for 2–3 hours. REACH drafts replies on request; Alan posts them. | Alan, EO, REACH |
| T+1 | Wed 28 Oct | Optional second subreddit. MEASURE does public reads of X, HN rank and comments, Reddit, and GitHub stars and release downloads. REACH writes a short recap and FAQ from real questions. | MEASURE, REACH |

## 4. Agent needs
**REEL**
- **Hero cut, 16:9, 30–45 s** for X and the README/HN link: the idea typed in → the stack picked → Generate → the pipeline running → five tabs filled with **real content** → the export folder showing the five `.md` files plus `kit/`. Real generation only. The 15 Oct v2 clip shows an empty 0/11 pipeline and can't support a "docs out" claim.
- **1:1 cut, 15–20 s** for the X feed, and an optional **9:16** only if Alan wants it.
- **6 s teaser** for T-2 (UI plus wordmark, no claims).
- On screen: the version "v3.1.0", a real stack name (one of the three verified), the five tab labels, and ideally one second of the exported files. Credentials must **never** appear (key fields blank or masked). Burned-in captions must state only what the frame shows. The v1 `cascade.mp4` ("Five docs out" over an empty screen) stays retired.
- Deliver the sha256 for each file and a frame audit, as for Sonora.

**SHIP** (verify and report. Any PR needs Alan's yes, and no push or merge without one.)
- The release is v3.1.0 Latest with 4 assets. Re-confirm the SHAs above against the hub card on T-1.
- README: the "Linux: AppImage | deb | **Arch**" badge and "Arch, Omarchy, Ubuntu, Debian" line. Either point to a real Arch install path or soften it to "Linux x86_64". Also flag the "Rust – destructive free" badge as unclear.
- README must say plainly up front that you need your own AI provider credentials (paid API) before users download. Currently that's only implied by the DeepSeek badge.
- Bundling and dependency honesty: the AppImage is 86 MB versus a 6.9 MB tar.gz and 8.6 MB deb. Confirm whether the AppImage bundles WebKitGTK and what the deb/tar.gz need from the system (WebKitGTK 4.1?), and document it. This is the lesson from browser-linux and @probonopd.
- State that the Linux assets were built from `d79ec73` (it's in the release body already. Keep it).
- Hub card `#cascade`: v3.1.0, 4 files, macOS Apple Silicon / Linux x86_64, MIT. The link resolves.
- Confirm LICENSE is MIT at the repo root (the 15 Oct re-confirm request is still open).

## 5. Draft hook ideas (DRAFTS, not approved, nothing posted)
- **D1 (fact-first):** "Five docs before one line of code. Cascade takes one app idea and one stack and writes the PRD, ARD, TRD, TASKS and AGENTS.md a coding agent builds from. macOS (Apple Silicon) + Linux. MIT. Bring your own API key."
- **D2 (design angle, for HN/X replies):** "One model call for product meaning. Everything else (IDs, files, the exact markdown) comes from a local compiler, so the preview is byte-for-byte the export."
- **D3 (problem-first, neutral):** "A coding agent without a spec builds the wrong thing. Cascade writes the spec first."
- **D4 (personal, GATED):** "My coding agents kept building the wrong thing. My prompt was the spec." Use only if Alan confirms it's his own experience.
- **Honesty reply (every channel):** "Verified on three stacks with real apps (SwiftUI desktop, SwiftUI menu bar, Tauri 2), per the release notes. Android and Astro work but aren't verified yet. Needs your own provider key. Keys stay in memory, no telemetry."
- **Link reply:** https://nodaysidle-apps.vercel.app/#cascade · source: https://github.com/nodaysidle/nodaysidle-cascade-v3

## 6. Risks
| Risk | Mitigation |
|---|---|
| A repeat of the credibility correction (as with @probonopd on browser-linux) over "verified", platforms, or Linux packaging | Use section 0 wording only, attribute "verified" to the release notes, settle the AppImage bundling story before T-0, and drop "Arch" unless it's real. |
| API-key and cost surprise ("so it's a DeepSeek wrapper?") | Disclose it in the main post or first reply and answer with the D2 compiler angle. |
| A clip that overstates (v1 caption history) | Use only a real-generation hero clip, with a frame audit. |
| Low reach (41 followers) and an HN post that sinks unnoticed | Treat HN as a one-shot try and don't repost. Set expectations: the measure is quality replies, stars and downloads, not impressions. |
| Cascade's prep crowding Kurek (Wed 21) | No public Cascade activity before Sun 25. |
| The README "Apple Silicon only" contradiction comes back, or the docs drift | SHIP's T-1 check. |
| Alan unavailable on T-0 evening for HN comments | Move to the Thu 29 fallback. |
| Stale 15 Oct copy and approvals reused | Mark the 15 Oct packet as history. The new packet needs fresh approval. |

## 7. Open questions for Alan
1. Is Tue 27 Oct 17:30 OK, or Thu 29? Do you want a T-2 teaser on Sun 25?
2. Will you do Show HN and stay around to answer comments for about 2–3 hours? Which subreddits are OK: r/SideProject, plus r/ChatGPTCoding or r/ClaudeAI?
3. Product Hunt: skip for now, as recommended?
4. Is "my coding agents kept building the wrong thing" your own experience? (Unlocks D4.)
5. Can you record or allow a real generation run for REEL (with your key, masked)? Which idea and stack should the demo use?
6. README: should SHIP open a PR to soften "Arch, Omarchy…" and add a "bring your own API key" line up front?
7. Does the 86 MB AppImage bundle WebKitGTK? What do the deb and tar.gz need from the system?
8. Is v3.1.0 the launch version, or is a v3.2 (e.g. after `9e38b03`) coming that should be the big launch instead?
