# Troubleshooting

## `cursell: command not found`

The install probably completed but the npm global `bin` directory isn't on
your `PATH`.

```bash
npm config get prefix
# e.g. /usr/local
# add /usr/local/bin to PATH in ~/.bashrc or ~/.zshrc
```

Or use `npx`:

```bash
npx @cursell/cli hub init
```

## Claude Code doesn't show `cursell-hub` under `/mcp`

1. Run `cursell-mcp` manually. It should print a startup message to stderr
   and stay running (waiting on stdio). Press `Ctrl+C` to exit.
2. Check `~/.claude.json`:
   ```bash
   cat ~/.claude.json | jq .mcpServers["cursell-hub"]
   ```
3. Restart Claude Code fully (quit the app, not just close the tab).

## The MCP server crashes on startup

Run it directly to see the error:

```bash
cursell-mcp 2>&1 | head -20
```

Common causes:

- Wrong Node version — Cursell requires Node 20+
- Corrupted cache — `rm -rf ~/.cursell/cache/`
- Hub API unreachable — try `curl https://api.cursell.ai/health`

## "Agent is large" warning keeps appearing

Some agents are > 3000 words and trigger a size warning on the first
`load_agent` call. Confirm by calling `load_agent` again with
`confirm_large: true`. Most AI CLIs do this automatically after the warning.

## Statusline shows the wrong agent

If you have multiple Claude Code terminals open and the statusline shows the
wrong agent:

1. Close the terminal and re-open it
2. Clear per-session state:
   ```bash
   rm -f /tmp/cursell/agent-*.json
   ```
3. Load an agent again in the terminal you care about

Each terminal's agent is keyed by the PID of the `claude` CLI that spawned
both the MCP server and the statusline. If those don't match (e.g. the
state file is stale), you may see the wrong agent.

## Hub is offline / timeouts

The MCP server falls back to the local cache (`~/.cursell/cache/agents/`)
when the hub is unreachable. You can keep using cached agents while the hub
is down.

Status page: https://status.cursell.ai (if available) / [@cursell on
Twitter](https://twitter.com/cursell).

## Reporting a bug

Include in the issue:

```bash
cursell --version
node --version
uname -a
```

Plus the command that failed and the full error output. [Open an issue](https://github.com/cursell/cli/issues).

## Getting unstuck

- Issues: https://github.com/cursell/cli/issues
- Discussions: https://github.com/cursell/cli/discussions
- Account / billing: https://cursell.ai/support
- Security: security@cursell.ai
