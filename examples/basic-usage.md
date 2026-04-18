# Basic usage

End-to-end walkthrough of installing Cursell, configuring Claude Code, and
loading your first agent.

## 1. Install

```bash
npm install -g cursell
```

Verify:

```bash
cursell --version
# cursell 0.1.0
```

## 2. Configure Claude Code

```bash
cursell hub init --provider claude
```

Output:

```
  Cursell Agent Hub — Setup

  Provider: claude (specified)

  ✓ Added MCP server 'cursell-hub' to ~/.claude.json
  ✓ Wrote skill to /Users/you/.claude/skills/cursell/SKILL.md

  Done! Restart your AI CLI to activate Cursell.
```

## 3. Restart Claude Code

Quit and relaunch Claude Code (not just close the tab).

## 4. Verify the MCP connection

In Claude Code:

```
/mcp
```

You should see `cursell-hub` listed with three tools: `search_agents`,
`load_agent`, `list_loaded`.

## 5. Find an agent

```
What security agents are in the Cursell Hub?
```

Claude calls `search_agents` and lists matches.

## 6. Load an agent

```
Load the vibesec agent.
```

Claude calls `load_agent({slug: 'vibesec'})`. You'll see an activation
banner with the agent's mascot, then the agent's instructions take over.

## 7. Use the agent

Just ask in plain language:

```
Review this code for security issues:

app.get('/user/:id', (req, res) => {
  const user = db.query(`SELECT * FROM users WHERE id = ${req.params.id}`);
  res.send(`<h1>Hello ${user.name}</h1>`);
});
```

VibeSec's framework kicks in — Claude will flag SQL injection, XSS, and
other issues per the agent's rules.

## 8. Switch to another agent

```
Unload VibeSec. Load the tdd-coach agent instead.
```

Claude calls `load_agent({slug: 'tdd-coach'})`. Only one agent is active
at a time; loading a new one replaces the previous.
