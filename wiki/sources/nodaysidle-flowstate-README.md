---
type: source-readme
repo: "nodaysidle/nodaysidle-flowstate"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "70552f8bb8c5298beb21de43fca1cdfc9a52d4d3"
source_commit_date: "2026-10-16T23:26:44+02:00"
readme_path: "README.md"
readme_blob_sha: "4f2149197432da6d390995e80f15665b068e3322"
fetched: "2026-10-16T23:30:12+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/nodaysidle-flowstate/blob/70552f8bb8c5298beb21de43fca1cdfc9a52d4d3/README.md"
tags: [source, readme, nodaysidle-flowstate]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/nodaysidle-flowstate` at `70552f8` (2026-10-16T23:26:44+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

<img src="https://raw.githubusercontent.com/nodaysidle/nodaysidle-flowstate/70552f8bb8c5298beb21de43fca1cdfc9a52d4d3/github/social-preview.png" alt="FlowState — NODAYSIDLE" width="100%">

# FlowState

> A smarter Pomodoro for developers who don't like timers.

![Platform](https://img.shields.io/badge/platform-macOS%2014%2B-black?style=flat-square&logo=apple)
![Swift](https://img.shields.io/badge/Swift-6.0-orange?style=flat-square&logo=swift)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

## Overview

Traditional Pomodoro timers interrupt you at fixed intervals regardless of your actual focus state. FlowState watches your keyboard and mouse activity, learns your work patterns, and only nudges you when you're genuinely losing focus. No arbitrary timers. No interruptions during flow.

FlowState v1 uses adaptive heuristics, not a trained ML model, for break suggestions.

## Features

- **Activity-based focus detection** — monitors keyboard and mouse activity to calculate a real-time focus score
- **Smart screen dimming** — gently dims your screen when focus drops, creating a subtle visual cue to take a break
- **Adaptive break suggestions** — uses recent session patterns and focus trends to suggest breaks when useful
- **Liquid-fill menu bar icon** — visualizes your current focus level with a smooth, filling indicator
- **Configurable settings** — fine-tune detection sensitivity, tint intensity, and break preferences
- **Privacy-first** — all processing happens on-device; no data leaves your Mac

## How It Works

1. **Focus Score Engine** — analyzes keyboard keystroke frequency and mouse movement patterns to generate a 0–100 focus score
2. **Idle Detection** — when focus drops below a threshold for a sustained period, the screen gradually dims
3. **Session Tracking** — tracks your work sessions and adapts to your recent behavior
4. **Break Suggestions** — uses historical patterns and live focus trends to suggest breaks, not fixed timers

## Technology

| Area | Technology |
|------|------------|
| Language | Swift 6 with strict concurrency |
| Interface | SwiftUI (settings), AppKit (menu bar, screen overlay) |
| Animation | Core Animation |
| State | Observation framework |
| Intelligence | Adaptive heuristics (on-device, no external APIs) |

## Requirements

- macOS 14.0 (Sonoma) or later
- Apple Silicon or Intel Mac

## Installation

The latest release ([v1.0.2](https://github.com/nodaysidle/nodaysidle-flowstate/releases/tag/v1.0.2)) has no downloadable assets. The newest pre-built app is [`FlowState-1.0.1.dmg`](https://github.com/nodaysidle/nodaysidle-flowstate/releases/download/v1.0.1/FlowState-1.0.1.dmg) ([SHA-256](https://github.com/nodaysidle/nodaysidle-flowstate/releases/download/v1.0.1/FlowState-1.0.1.dmg.sha256)) on [v1.0.1](https://github.com/nodaysidle/nodaysidle-flowstate/releases/tag/v1.0.1):

```bash
shasum -a 256 FlowState-1.0.1.dmg
# expected: 156993e518a9f21fffac53de7c8fc47afe9ebe427425ce63b1acf3eb7131cbe1
```

Build from source (macOS 14+):

```bash
git clone https://github.com/nodaysidle/nodaysidle-flowstate.git
cd nodaysidle-flowstate
./scripts/package-flowstate.sh   # builds dist/FlowState.app and dist/FlowState-1.0.1.dmg
```

### Accessibility Permission

FlowState needs Accessibility access to monitor keyboard and mouse activity:

1. Open **System Settings → Privacy & Security → Accessibility**
2. Add FlowState to the list of allowed apps
3. Restart the app if needed

## Configuration

Access settings via the menu bar dropdown → **Settings**.

| Tab | Options |
|-----|---------|
| Focus | Idle threshold (20/30/40), Idle trigger duration (5/10/15/30s), Recovery time (3/5/10s) |
| Tint | Dimming intensity (30–80%), Fade duration (10/30/60/120s) |
| Breaks | Smart break suggestions on/off, Default session length (25/45/50/60/90 min) |
| History | Session history and stats |
| General | Launch at login, Version info |

## Menu Bar

The menu bar icon shows your current focus state:

- **Empty circle** — Low activity / idle
- **Filling circle** — Actively working, fill level = focus score
- **Pause icon** — Break suggestion triggered

Click the icon to see your current focus score, keyboard and mouse activity indicators, break suggestions, and quick access to Settings and Quit.

## Architecture

```
Sources/FlowState/
├── FlowStateApp.swift              # @main app entry, MenuBarExtra, Settings scene
├── AppState.swift                  # Central @Observable state coordinator
├── Models/
│   ├── ActivitySample.swift        # Activity snapshot model
│   └── UserPreferences.swift       # Persisted app preferences
├── Services/
│   ├── ActivityMonitorService.swift      # Keyboard/mouse activity sampling
│   ├── AccessibilityPermissionChecker.swift # Accessibility permission polling
│   ├── FocusScoreEngine.swift            # Focus score calculation
│   ├── IdleDetector.swift                # Idle state detection
│   ├── SessionTracker.swift              # Session lifecycle + stats
│   ├── BreakPredictor.swift              # Adaptive break suggestion heuristic
│   ├── ScreenTintController.swift        # Tint overlay orchestration
│   └── ActivityDataStore.swift           # Session persistence
├── Views/
│   ├── MenuBarDropdown.swift       # Menu bar popover UI
│   ├── MenuBarIconRenderer.swift   # Custom menu bar icon drawing
│   ├── ScreenTintOverlay.swift     # Dimming overlay window
│   ├── SettingsView.swift          # Settings tabs
│   └── HistoryView.swift           # Session history view
```

## Privacy

FlowState operates entirely on your device:

- Activity data stored locally in `~/Library/Application Support/FlowState/`
- No network requests, no telemetry, no analytics
- Session history is used only for improving break predictions

## Status

Active — v1. Feature-complete focus-detection menu bar app.

## Contributing

This repository is not currently accepting external contributions.

## License

MIT
