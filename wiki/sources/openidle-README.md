---
type: source-readme
repo: "nodaysidle/openidle"
visibility: "public"
fork: false
default_branch: "main"
source_commit: "a623d5fcaae10d33cafdeaff2c2d6db80d4aaaec"
source_commit_date: "2026-10-14T07:52:13+02:00"
readme_path: "README.md"
readme_blob_sha: "edae812bf244a65a8149e82688842b8b8e08aff2"
fetched: "2026-10-16T21:43:33+02:00"
verified: "git blob sha1 of fetched bytes == GitHub tree blob at source_commit"
authority: "owner source of truth (Alan 21:32/21:33)"
url: "https://github.com/nodaysidle/openidle/blob/a623d5fcaae10d33cafdeaff2c2d6db80d4aaaec/README.md"
tags: [source, readme, openidle]
---

> Verbatim copy of `README.md` from **public** repo `nodaysidle/openidle` at `a623d5f` (2026-10-14T07:52:13+02:00). Relative links were rewritten to absolute GitHub URLs pinned to this commit. **Owner source of truth (Alan 21:32/21:33).** Refresh on every release. The local checkout may differ (uncommitted or unpushed work); check before stating facts.

# OpenIdle

A local messenger for the AI agents already installed on this machine. Each bot is a contact with its own personality, engine, model, working directory, and chat history. Replies stream. When a bot wants to run a command, edit a file, ask a question, drive a computer, or use a connected app, the chat shows an approval card: allow, deny, or answer in text.

The window is a GTK shell around a Bun server that listens on `127.0.0.1` only. Chats, tokens, and screenshots stay in `~/.local/share/openidle`. The agent CLIs you pick (Cursor, Codex, Antigravity, Command Code) still talk to their own providers. A local-model bot does not.

## Install

Needs `bun` 1.3 or newer, `python-gobject`, and `webkit2gtk-4.1`. Any of `agent` (Cursor), `codex`, `agy`, and `commandcode` that are already logged in. This PC's computer controls use `grim`, `wtype`, and `hyprctl`, which Omarchy ships. The pointer helper is built from `native/` and talks to Hyprland directly. `ydotool` is only a fallback.

```sh
packaging/install.sh
```

That installs dependencies, builds the UI and the pointer helper, and adds, per user and without root:

- a systemd user service, `openidle.service`, started with the graphical session
- `~/.local/bin/openidle`
- a desktop entry and icon

Launch **OpenIdle** from the app menu, or run `openidle`. The service keeps running after the window closes.

`install.sh` puts mise's real install directories ahead of `~/.local/bin`. mise wrapper scripts run `mise use` on every launch and stall under systemd. Run the script again after upgrading Codex, Command Code, or `gh`.

Without installing:

```sh
bun install
bun run build
native/build.sh          # needs gcc, wayland-scanner, wayland-client
bin/openidle             # starts the server if needed, then opens the window
bin/openidle --server    # server only, in the foreground
```

### Optional

Both scripts are safe to run again.

```sh
packaging/local-model.sh      # llama.cpp on 127.0.0.1:8080, user service openidle-llm
packaging/desktop/setup.sh    # Docker sandbox desktop, container openidle-desktop
```

`local-model.sh` downloads a current llama.cpp Vulkan build and Gemma 4 E4B (Q4, about 4.6 GB) into `~/.local`. The server unloads the model after 10 idle minutes. `setup.sh` needs Docker. The container is published on `127.0.0.1:6080` and starts the first time a bot uses the cloud desktop.

Hyprland with a Lua config: `packaging/hyprland.lua` binds Super+Alt+I and keeps the window opaque. The UI follows the active Omarchy theme (`~/.config/omarchy/current_theme`).

## Using it

The first launch creates five contacts: Juno (Cursor), Forge (Codex), Atlas (Antigravity), Quill (Command Code), and Pip (the local model). Edit a contact for its personality, model, permission mode, working directory, computer access, and connected apps.

| Key | Action |
|---|---|
| Alt+1…9 | Switch contact |
| Alt+↑ / Alt+↓ | Previous / next contact |
| Ctrl+N | New bot |
| Ctrl+. | Computer panel |
| Ctrl+, | Settings |
| Esc | Stop the current reply |
| Ctrl+Q | Close the window. The service keeps running |
| Super+Alt+I | Launch, after the Hyprland snippet is applied |

"Allow for this chat" is remembered on that bot and can be revoked in the bot editor. A fresh approval is always required for sending mail, posting, commenting, and opening issues.

## Engines

| Engine | How it runs | Approvals |
|---|---|---|
| Cursor | `agent acp` | Each of the agent's own tool calls, plus OpenIdle tools |
| Codex | `codex app-server` | Commands, file changes, questions, and MCP prompts. Sandboxed to the bot's workspace unless the mode is "full" |
| Command Code | `commandcode acp` | Same shape as Cursor. Modes: ask, accept edits, plan, auto |
| Antigravity | `agy` print mode, one process per turn | Headless agy cannot pause, so a denied action becomes a card and the turn resumes after you allow it. Each bot has a private agy home, so your global plugins and MCP servers are not loaded |
| Local model | OpenAI-compatible `/v1/chat/completions` | OpenIdle tools, when the model supports function calls. Default URL `http://127.0.0.1:8080/v1` |

A bot with no working directory uses `~/.local/share/openidle/workspaces/<bot-id>`.

## Computer

**This PC** screenshots with `grim`, focuses and launches through `hyprctl`, types with `wtype`, and clicks through `native/oi-pointer` (`zwlr_virtual_pointer_v1`). Every action asks first.

**Cloud desktop** is either the sandbox container from `packaging/desktop` (Debian, Openbox, Firefox, a noVNC view on localhost) or an SSH host you set in Settings. The SSH host needs key login and an X11 session with ImageMagick `import`, `xdotool`, and `wmctrl`. Remote shell access is a separate approval and is never granted for the whole chat.

## Connected apps

Credentials stay in the local database. Add client IDs under Apps. The OAuth redirect is `http://127.0.0.1:7787/oauth/callback`.

- **GitHub.** Uses `gh auth token`, so `GH_TOKEN` has to be visible to the systemd user service (`systemctl --user import-environment GH_TOKEN`), or paste a token.
- **Gmail.** A Google "Desktop app" OAuth client, Gmail API enabled, scope `gmail.modify`.
- **X.** OAuth 2.0 with PKCE. Whether posting works depends on the X API plan.
- **Reddit.** Needs an app approved under Reddit's Responsible Builder Policy. Self-service API keys are closed. Leave the secret empty for an installed app.

## Privacy

The server checks `Host` and `Origin`, and every API and WebSocket call needs the session token in `~/.local/share/openidle/token` (mode 0600). Each bot gets its own MCP bearer token, derived from a key that stays on disk, and can only call its own tools. OpenIdle does not add an account, telemetry, or a cloud of its own.

`OPENIDLE_PORT` (default 7787) and `OPENIDLE_DATA_DIR` override the listen port and the data directory.

## Development

```sh
bun install
bun run dev          # server with reload, and the Vite UI on :5173
bun run typecheck
bun run build        # writes ui/dist, which the server serves
```

```
shell/openidle.py            GTK3 + WebKit2 window
server/index.ts              HTTP, WebSocket, static UI
server/runtime.ts            one session per bot, streaming, approval cards
server/engines/              Cursor and Command Code (ACP), Codex, Antigravity, local
server/mcp.ts                per-bot MCP tools: ask_user, computer_*, connected apps
server/computer.ts           this PC and the cloud desktop
server/connectors/           GitHub, Gmail, X, Reddit
ui/                          React UI
native/                      pointer helper
packaging/                   user install, local model, sandbox desktop, Hyprland snippet
```
