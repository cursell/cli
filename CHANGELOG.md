# Changelog

All notable changes to the `cursell` CLI are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [0.1.0] — 2026-04-17

Initial public release.

### Added

- `cursell hub init` — auto-detects Claude Code, Codex CLI, or Gemini CLI on
  your system and configures the MCP server + skill files.
- `cursell hub init --provider <name>` — skip detection, configure a specific
  provider (`claude`, `codex`, or `gemini`).
- `cursell hub init --with-statusline` — install a Claude Code statusline
  that shows the active agent per terminal session.
- `cursell hub update` — refresh skill / instruction files for detected
  providers.
- `cursell hub login` — authenticate with the Cursell Hub (email OTP).
- `cursell-mcp` — MCP server binary invoked by Claude Code / Codex / Gemini.
  Exposes three tools: `search_agents`, `load_agent`, `list_loaded`.
- `cursell-statusline` — per-session Claude Code statusline script.
- Local agent cache at `~/.cursell/cache/agents/`.
- Per-session state under `/tmp/cursell/` for statusline correlation.

[Unreleased]: https://github.com/cursell/cli/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/cursell/cli/releases/tag/v0.1.0
