# Installation

## Requirements

- **Node.js** 20 or later
- At least one supported AI CLI:
  - [Claude Code](https://docs.claude.com/en/docs/claude-code)
  - [Codex CLI](https://github.com/openai/codex)
  - [Gemini CLI](https://github.com/google-gemini/gemini-cli)

## Install globally (recommended)

```bash
npm install -g cursell
```

This installs three binaries onto your `PATH`:

| Binary | What it is |
|---|---|
| `cursell` | The CLI you run manually (`cursell hub init`, etc.) |
| `cursell-mcp` | The MCP server — your AI CLI launches it as a subprocess |
| `cursell-statusline` | Optional statusline script for Claude Code |

Verify:

```bash
cursell --version
```

## Run without installing

If you prefer not to install globally:

```bash
npx cursell hub init
```

`cursell` detects that it was launched via `npx` and writes npx-based
entries into your AI CLI configs automatically (your `cursell-hub` server
runs as `npx -y -p cursell cursell-mcp`).

The first launch of each day has a ~1-second cold start while npx
refreshes its cache. Subsequent launches are instant.

You can also force npx mode even after installing globally:

```bash
cursell hub init --use-npx
```

See [examples/npx-usage.md](../examples/npx-usage.md) for the full
walkthrough and trade-offs versus a global install.

## Updating

```bash
npm install -g cursell@latest
```

All three binaries update together. Restart your AI CLI afterward so it
picks up the new MCP server version.

## Uninstalling

```bash
npm uninstall -g cursell
```

After uninstalling, your AI CLI configs still reference `cursell-hub`. To
clean them up manually:

- `~/.claude.json` — remove the `cursell-hub` entry under `mcpServers`
- `~/.claude/settings.json` — remove the `statusLine` entry if present
- `~/.codex/config.toml` — remove the `[mcp_servers.cursell-hub]` block
- `~/.gemini/settings.json` — remove the `cursell-hub` entry

## Next steps

- [Configuration](configuration.md)
- [Claude Code setup](providers/claude-code.md)
- [Codex CLI setup](providers/codex-cli.md)
- [Gemini CLI setup](providers/gemini-cli.md)
