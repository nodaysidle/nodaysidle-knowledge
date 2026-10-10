---
type: wiki-note
note_kind: concept
topic_slug: x-promo
status: draft
created: 2026-10-08
updated: 2026-10-08
tags:
  - wiki
  - x-promo
---

# X promo calendar, October 2026 (with drafts)

## Summary

This is the posting calendar for 7–23 Oct 2026 (Europe/Ljubljana) with ready-to-post copy. Adlof posts manually. The weekly REACH routine (Mondays 09:17) extends the calendar from the week of 26 Oct, based on results and under-seen apps.

## Calendar

> **Update 2026-10-09 (REACH):** the week of 12 Oct is revised in [[wiki/concepts/x-promo-strategy-2026-10-12]] (nodaysrammar Tue 13, browser Wed 14, Cascade thread Thu 15, Sonora + showcase roundup Fri 16, Kurek recap Wed 14 evening). Rows below are kept for history.

| Day | Time | Post | Link | Visual |
|-----|------|------|------|--------|
| Wed 7 Oct | 15:15 | Kurek launch | github.com/nodaysidle/kureksistant/releases/tag/v0.1.0 | `docs/demo.gif` (repo) |
| Thu 8 Oct | 15:15 | WhisperBar | WhisperBar.dmg v1.1.2 | REEL `whisperbar.mp4` |
| Fri 9 Oct | 15:15 | ShareGuard | nodaysidle-shareguard/releases | REEL `shareguard.mp4` |
| Fri 9 Oct | 18:15 | Weekly roundup | portfolio (in reply) | — |
| Tue 13 Oct | 15:15 | Linux browser launch | nodaysidle-browser-linux | REEL `browser-linux.mp4` |
| Wed 14 Oct | 15:15 | Cascade thread | nodaysidle-cascade-v3 v3.1.0 | REEL `cascade.mp4` |
| Thu 15 Oct | 15:15 | Sonora | nodaysidle-sonora | REEL `sonora.mp4` (title blurred) |
| Fri 16 Oct | 18:15 | Kurek week-1 recap (no link) | — | screenshot |
| Tue 20 Oct | 15:15 | Synapse Notes | synapse-notes | clip still to request |
| Wed 21 Oct | 15:15 | Browser build thread | nodaysidle-browser-linux | reuse REEL footage |
| Thu 22 Oct | 15:15 | ClipRail | ClipRail DMG | clip still to request |
| Fri 23 Oct | 18:15 | "36 public repos" thread | portfolio | — |

## Drafts

### Kurek, Wed 7 Oct

> Most AI assistants are a 500MB window that steals your RAM and your focus.
>
> I shipped Kurek: a ~55MB local daemon. Middle-click to talk, it can see my screen, and its memory doesn't rot into one giant prompt.
>
> v0.1.0 for Linux is out 👇
> https://github.com/nodaysidle/kureksistant/releases/tag/v0.1.0
>
> #buildinpublic #linux

First reply: "Built on top of FatihMakes' JARVIS. Kurek is my take on it, licensed CC BY-NC 4.0."

### WhisperBar, Thu 8 Oct

> I talk faster than I type, so I built WhisperBar.
>
> Hold Ctrl+Option+D, speak, and it transcribes live and pastes the text right where your cursor is, in any Mac app.
>
> Free DMG 👇
> https://github.com/nodaysidle/whisper-bar/releases/download/v1.1.2/WhisperBar.dmg
>
> #buildinpublic #macapps

### ShareGuard, Fri 9 Oct

> I almost pushed a .env to a public repo once. So I built ShareGuard.
>
> Drop files or folders on it before you share, zip, or push. It flags API keys, private keys, emails, and local paths, and it all runs on your Mac with zero network calls.
>
> Free DMG on GitHub 👇
> https://github.com/nodaysidle/nodaysidle-shareguard/releases
>
> #buildinpublic #macapps

Use the first line only if it's true; otherwise use "One leaked API key ruins your week."

### Roundup, Fri 9 Oct

> This week I shipped/showed off 3 apps:
>
> 🐔 Kurek: a ~55MB local AI daemon for Linux
> 🎙 WhisperBar: menu-bar dictation for Mac
> 🛡 ShareGuard: a leak check before you share files
>
> All free to download. Everything I've built is here 👇

Reply: https://nodaysidle-portfolio-nine.vercel.app

### Linux browser, Tue 13 Oct

> I got tired of browsers that feel like a second OS, so I built my own for Linux.
>
> It's written in Rust on GTK3 and WebKitGTK. A 1.5MB AppImage. Needs GTK3 and WebKitGTK 4.1 on your system.
>
> v0.1.0 👇
> https://github.com/nodaysidle/nodaysidle-browser-linux
>
> #buildinpublic #rustlang

### Cascade thread, Wed 14 Oct

1. Every project I start dies in the same place: the vague idea before any code. So I built Cascade. 🧵
2. You give it one idea and it writes the PRD, the architecture doc, the technical spec, the task list, and an AGENTS file your coding agent can follow. Bring your own API key.
3. (clip or screenshot of the five doc tabs)
4. It runs on macOS and Linux, v3.1.0 👇 https://github.com/nodaysidle/nodaysidle-cascade-v3/releases/tag/v3.1.0

### Sonora, Thu 15 Oct

> I wanted one player for all my music, so I built Sonora.
>
> Spotify, YouTube Music and local files in one library. It controls Spotify through Spotify Connect; YouTube needs yt-dlp.
>
> v0.1.1 👇
> https://github.com/nodaysidle/nodaysidle-sonora
>
> #buildinpublic

### Synapse Notes, Tue 20 Oct

> Ideas show up while I'm walking, not at my desk. So I built Synapse Notes, an Android app where you just talk and it saves the note.
>
> 👇 https://github.com/nodaysidle/synapse-notes
>
> #buildinpublic #androiddev

### Kurek recap, Fri 16 Oct (no link)

> Kurek launched a week ago: [X] views, [Y] downloads, and the #1 request was [Z]. Here's what I'm building next. 👇

## Copy caveats (from clip review, 2026-10-07)

- Before posting Sonora and Synapse, confirm that each has a release you can download. Swap the post if it doesn't.
- Browser: not self-contained. It needs system GTK3 and WebKitGTK 4.1.
- Cascade: docs are generated only with API keys. The clip shows the UI tabs, not real output.
- Sonora: the YouTube fallback needs yt-dlp. An explicit track title was blurred in the clip.
- WhisperBar and ShareGuard are macOS-only, so their clips are icon plus README text, not screen recordings.

## Related

- [[wiki/MOC/moc-x-promo]]
- [[wiki/concepts/x-promo-strategy]]
- [[wiki/concepts/reel-clip-workflow]]
- [[wiki/concepts/kureksistant-overview]] · [[wiki/concepts/cascade-v3-overview]] · [[wiki/concepts/nodaysidle-sonora-overview]] · [[wiki/concepts/synapse-notes-overview]] · [[wiki/concepts/nodaysidle-browser-linux-overview]]

## Open questions

- Actual results per post (views, replies, downloads after 24h).
- Request clips for Synapse Notes and ClipRail before 20 and 22 Oct.
