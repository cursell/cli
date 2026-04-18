# Configuration

## Files Cursell touches

`cursell hub init` only touches these files. Nothing else is modified.

| Path | When | What is written |
|---|---|---|
| `~/.claude.json` | Claude Code detected | Adds `cursell-hub` under `mcpServers` |
| `~/.claude/settings.json` | `--with-statusline` | Adds `statusLine` command |
| `~/.claude/skills/cursell/SKILL.md` | Claude Code detected | The Cursell skill prompt |
| `~/.codex/config.toml` | Codex detected | Appends `[mcp_servers.cursell-hub]` block |
| `~/.codex/AGENTS.md` | Codex detected | Appends Cursell instructions |
| `~/.gemini/settings.json` | Gemini detected | Adds `cursell-hub` under `mcpServers` |
| `~/.gemini/GEMINI.md` | Gemini detected | Appends Cursell instructions |
| `~/.cursell/credentials.json` | `cursell hub login` | Hub API token (mode 0600) |

Files Cursell **creates on its own** at runtime:

| Path | Purpose |
|---|---|
| `~/.cursell/cache/agents/*.json` | Local cache of loaded agents |
| `/tmp/cursell/agent-<pid>.json` | Per-session active-agent marker (statusline) |

## Environment variables

| Variable | Default | Purpose |
|---|---|---|
| `CURSELL_API_URL` | `https://api.cursell.ai` | Hub API endpoint |
| `CURSELL_HUB_URL` | (falls back to `CURSELL_API_URL`) | Alias |
| `CURSELL_API_TOKEN` | — | Bypass `~/.cursell/credentials.json` |
| `NO_COLOR` | — | Disable ANSI colors in CLI output |

These are read by `cursell-mcp` at startup. To override them for the MCP
server, add an `env` block in your AI CLI's config:

```json
"cursell-hub": {
  "type": "stdio",
  "command": "cursell-mcp",
  "env": { "CURSELL_API_URL": "http://localhost:3001" }
}
```

## The local cache

Loaded agents are cached under `~/.cursell/cache/agents/` keyed by slug. The
cache is:

- **Version-aware** — re-fetches when the hub has a newer version
- **Offline-friendly** — serves the cached copy if the hub is unreachable
- **Safe** — file mode `0600`, slug validated to prevent path traversal

Clear the cache manually:

```bash
rm -rf ~/.cursell/cache/
```

It will be rebuilt the next time you load an agent.

## Authentication

The hub supports anonymous use (load public agents, track downloads
anonymously) out of the box. For private agents or publishing, authenticate
with:

```bash
cursell hub login
```

This runs an email OTP flow against `api.cursell.ai` and stores the session
token at `~/.cursell/credentials.json` (mode `0600`).

Alternatively, set `CURSELL_API_TOKEN` manually.
