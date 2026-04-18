# Using Cursell without installing it globally (`npx`)

If you prefer not to `npm install -g cursell` — for example on a shared
machine, in a dev container, or just to try it out — you can run Cursell
entirely through `npx`.

## One-shot setup

```bash
npx cursell hub init
```

`cursell` auto-detects that it was launched via `npx` and writes
**npx-based** entries into your AI CLI configs, so the MCP server and
statusline don't need to be on your `PATH`.

For example, `~/.claude.json` gets:

```json
{
  "mcpServers": {
    "cursell-hub": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "-p", "cursell", "cursell-mcp"]
    }
  }
}
```

Every time your AI CLI launches, it runs `npx -y -p cursell cursell-mcp`.
The first run downloads and caches the package; subsequent runs use the
cache. Expect a ~1-second cold start on the first launch of each day.

## Force npx mode even if you have a global install

If you already installed `cursell` globally but want the config to use
`npx` anyway (for example to always get the latest version without
running `npm install -g cursell@latest`), pass `--use-npx`:

```bash
cursell hub init --use-npx
```

## Typical npx-only workflow

```bash
# Configure once (no global install)
npx cursell hub init --provider claude --with-statusline

# Restart Claude Code
# (quit and relaunch the app)

# Done — load agents as usual
#   "Load the vibesec agent"
#   "What hub agents can help me with testing?"
```

## Updates

With an npx-based config, you update simply by running any `cursell`
command — `npx` fetches the latest version automatically. To force a
refresh of the cache:

```bash
npx -y cursell@latest hub update
```

## Trade-offs versus global install

| | `npm install -g cursell` | `npx` only |
|---|---|---|
| One-time install | ✅ | ✅ |
| First-launch speed | instant | ~1s cold start |
| Subsequent launches | instant | instant (npx cache) |
| Needs `PATH` management | ✅ | ❌ |
| Needs `npm install -g` permissions | ✅ | ❌ |
| Auto-updates | ❌ (manual) | ✅ (each npx run) |

If you're unsure, `npm install -g cursell` is the simpler choice for
everyday use. Switch to `npx` only if that doesn't fit your environment.
