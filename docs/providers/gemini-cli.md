# Gemini CLI setup

## Automatic setup

```bash
cursell hub init --provider gemini
```

This writes two files:

1. **`~/.gemini/settings.json`** — adds a `cursell-hub` entry under `mcpServers`
2. **`~/.gemini/GEMINI.md`** — appends Cursell's instructions

Restart Gemini CLI afterward.

## What gets written

In `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "cursell-hub": {
      "command": "cursell-mcp"
    }
  }
}
```

Note: Gemini uses a slightly different config format than Claude Code — no
`type: "stdio"` field. Cursell writes the correct shape for each provider.

In `~/.gemini/GEMINI.md`: the Cursell skill prompt.

## Using agents

```
Load the readme-writer agent.
```

```
What hub agents can help me with testing?
```

## Troubleshooting

If Gemini doesn't show Cursell tools:

- Verify `cursell-mcp` is on `PATH`: `which cursell-mcp`
- Check the settings.json is valid: `cat ~/.gemini/settings.json | jq .`
- Restart Gemini CLI
- Check Gemini logs for MCP errors

See [Troubleshooting](../troubleshooting.md) for more.
