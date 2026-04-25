# @cursell/cli

The Cursell command-line interface for the Agent Hub — discover, install, and
use specialized AI agents across Claude Code, Codex CLI, and Gemini CLI.

<p align="center">
  <img src="docs/demo.gif" alt="cursell demo" width="680" />
</p>

## Install

```bash
npm install -g @cursell/cli
```

Or run without installing (see [examples/npx-usage.md](examples/npx-usage.md)):

```bash
npx @cursell/cli hub init
```

## Quick start

Point Cursell at your AI CLI of choice:

```bash
cursell hub init
```

This detects Claude Code, Codex CLI, or Gemini CLI on your system and
configures the MCP server + skill files automatically. From then on, ask your
AI to load a Cursell agent:

```
Load the "vibesec" agent and review this code.
```

## Commands

| Command | What it does |
|---|---|
| `cursell hub init` | Configure your AI CLI to use the Cursell Hub |
| `cursell hub init --provider <name>` | Configure only for `claude`, `codex`, or `gemini` |
| `cursell hub init --with-statusline` | Also add a Claude Code statusline that shows the active agent per terminal |
| `cursell hub init --use-npx` | Write npx-based entries (for users who don't want to install globally — see [examples/npx-usage.md](examples/npx-usage.md)) |
| `cursell hub update` | Refresh skill / instruction files |
| `cursell hub login` | Authenticate with the Cursell Hub |
| `cursell --help` | Show all commands |
| `cursell --version` | Print the installed version |

## How it works

The `@cursell/cli` package ships three binaries:

- **`cursell`** — the CLI you run manually
- **`cursell-mcp`** — the MCP (Model Context Protocol) server your AI CLI
  talks to. It exposes three tools: `search_agents`, `load_agent`,
  `list_loaded`
- **`cursell-statusline`** — an optional per-session status line for Claude
  Code that shows which agent is currently loaded

When you load an agent, the MCP server fetches its instructions from the
Cursell Hub, caches it locally under `~/.cursell/cache/`, and your AI CLI
follows those instructions for the rest of the session.

## Documentation

- [Installation](docs/installation.md)
- [Configuration](docs/configuration.md)
- [Claude Code setup](docs/providers/claude-code.md)
- [Codex CLI setup](docs/providers/codex-cli.md)
- [Gemini CLI setup](docs/providers/gemini-cli.md)
- [Troubleshooting](docs/troubleshooting.md)

## Support

- **Bug reports / feature requests:** [open an issue](https://github.com/cursell/cli/issues)
- **Security vulnerabilities:** security@cursell.ai (see [SECURITY.md](SECURITY.md))
- **Hub / account questions:** https://cursell.ai/support

## License

This repository contains documentation, examples, and installation resources
only. The CLI runtime source code is not public.

Use of the `@cursell/cli` npm package is governed by
[Cursell's Terms of Service](https://cursell.ai/terms). See [LICENSE.md](LICENSE.md).
