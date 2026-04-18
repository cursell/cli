# Claude Code setup

## Automatic setup

```bash
cursell hub init --provider claude
```

This writes two files:

1. **`~/.claude.json`** — adds a `cursell-hub` entry under `mcpServers`
2. **`~/.claude/skills/cursell/SKILL.md`** — the skill prompt that teaches
   Claude Code how to use the hub's MCP tools

Restart Claude Code afterward.

## With statusline

Add the `--with-statusline` flag to also register a custom statusline that
shows which agent is active in each terminal:

```bash
cursell hub init --provider claude --with-statusline
```

This writes `~/.claude/settings.json`:

```json
{
  "statusLine": { "type": "command", "command": "cursell-statusline" }
}
```

Each Claude Code terminal gets its own statusline — if you have 5 terminals
open with different agents loaded, each shows its own.

## Using agents

Once configured, ask Claude Code naturally:

```
What security agents are available in the hub?
```

Claude will call `search_agents`. To load one:

```
Load the vibesec agent.
```

Claude will call `load_agent({slug: 'vibesec'})`, render an activation
banner with the agent's mascot, and apply the agent's instructions for the
rest of the session.

To see what's currently active:

```
Which Cursell agent is loaded?
```

## MCP tool reference

The `cursell-mcp` server exposes three tools to Claude Code:

### `search_agents`

Search by query, category, or tag.

```
search_agents({
  query?: string,
  category?: "code" | "testing" | "devops" | "docs" | "security" | "general",
  tag?: string,
  limit?: number,     // default 20
  offset?: number
})
```

Returns a formatted list of matching agents.

### `load_agent`

Load an agent's instructions into the current session.

```
load_agent({
  slug: string,          // e.g. "vibesec"
  confirm_large?: boolean
})
```

Large agents (> 3000 words) return a size warning on the first call. Call
again with `confirm_large: true` to proceed.

### `list_loaded`

```
list_loaded({})
```

Returns the currently active agent plus cache statistics.

## Troubleshooting Claude Code integration

If `/mcp` doesn't show `cursell-hub`:

1. Verify `cursell-mcp` is on your `PATH`:
   ```bash
   which cursell-mcp
   ```
2. Check `~/.claude.json`:
   ```bash
   cat ~/.claude.json | jq .mcpServers
   ```
   You should see a `cursell-hub` entry with `command: "cursell-mcp"`.
3. Restart Claude Code fully (quit the app, not just close the tab).

For more, see [Troubleshooting](../troubleshooting.md).
