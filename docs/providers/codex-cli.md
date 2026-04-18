# Codex CLI setup

## Automatic setup

```bash
cursell hub init --provider codex
```

This writes two files:

1. **`~/.codex/config.toml`** — appends an `[mcp_servers.cursell-hub]` block
2. **`~/.codex/AGENTS.md`** — appends Cursell's agent instructions

Restart Codex CLI afterward.

## What gets written

In `~/.codex/config.toml`:

```toml
[mcp_servers.cursell-hub]
command = "cursell-mcp"
```

In `~/.codex/AGENTS.md`: the Cursell skill prompt (teaches Codex how to use
the hub's MCP tools — same content as the Claude Code skill).

## Using agents

Ask Codex to load an agent by name. Codex will call `load_agent` on the MCP
server.

```
Use the tdd-coach agent.
```

```
Show me the security agents in the Cursell Hub.
```

## Troubleshooting

If Codex doesn't recognize `cursell-hub`:

- Verify `cursell-mcp` is on `PATH`: `which cursell-mcp`
- Check the TOML is valid: `cat ~/.codex/config.toml`
- Restart Codex CLI
- Check Codex logs for MCP connection errors

See [Troubleshooting](../troubleshooting.md) for more.

## Note on MCP in Codex

Codex CLI's MCP support is still evolving. If you hit issues that aren't
covered here, please [open an issue](https://github.com/cursell/cli/issues)
with the Codex version you're running.
