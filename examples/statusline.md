# Statusline setup (Claude Code)

The Cursell statusline shows the currently active agent as a line below the
Claude Code chat, per terminal session. If you have 5 Claude Code terminals
open with different agents loaded, each shows its own.

## Install

```bash
cursell hub init --provider claude --with-statusline
```

This adds to `~/.claude/settings.json`:

```json
{
  "statusLine": {
    "type": "command",
    "command": "cursell-statusline"
  }
}
```

Restart Claude Code.

## What it looks like

With no agent loaded:

```
(empty — statusline hides itself)
```

With `vibesec` loaded:

```
Cursell · VibeSec v1.0.0
```

## How it works

- When you `load_agent(...)`, the Cursell MCP server writes the active
  agent's metadata to `/tmp/cursell/agent-<claude_pid>.json`.
- Claude Code invokes `cursell-statusline` after each assistant message
  (debounced ~300 ms) with session info on stdin.
- The statusline script reads `process.ppid` (the `claude` CLI that spawned
  it — same PID as the MCP server's parent) and looks up the matching state
  file.
- No file = no statusline shown.

## Removing the statusline

Edit `~/.claude/settings.json` and delete the `statusLine` block, or set it
to an empty object:

```json
{ "statusLine": {} }
```

Restart Claude Code.

## Troubleshooting

- **Statusline doesn't appear at all:** confirm `cursell-statusline` is on
  your `PATH` (`which cursell-statusline`). Restart Claude Code.
- **Statusline shows the wrong agent:** likely a stale state file. Run
  `rm -f /tmp/cursell/agent-*.json` and load an agent again.
- **Multiple terminals showing the same agent:** this shouldn't happen — each
  Claude CLI process has a different PID. If it does, please [open an
  issue](https://github.com/cursell/cli/issues) with your OS and Claude Code
  version.
