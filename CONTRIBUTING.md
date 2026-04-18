# Contributing

Thanks for the interest in improving Cursell!

## What this repository contains

This repository holds the **public-facing documentation, examples, and
installation resources** for the Cursell CLI. The runtime source code of the
CLI is maintained separately and is not published here.

## Accepted contributions

- **Bug reports** — something not working as documented
- **Feature requests** — ideas for new commands or capabilities
- **Documentation improvements** — PRs against `docs/`, `README.md`,
  `examples/`
- **Typo / clarity fixes** — anywhere in the Markdown content

## Not accepted

- Pull requests that attempt to modify CLI runtime behavior. The source isn't
  here to change.
- Contributions that depend on reverse-engineered details of the CLI binary.
  Please don't decompile the npm package to propose fixes — open an issue
  describing the behavior you see and we'll investigate internally.

## Filing a bug

Open an issue at https://github.com/cursell/cli/issues with:

- **Cursell version:** `cursell --version`
- **Node version:** `node --version`
- **OS:** macOS / Linux / Windows + version
- **AI CLI in use:** Claude Code / Codex / Gemini + version
- **What you ran:** full command
- **What happened:** actual output (including any error messages)
- **What you expected:** briefly

If the issue involves the MCP integration, include the `mcpServers` block
from your AI CLI's config (redact any tokens).

## Documentation PRs

For changes to docs/examples:

1. Fork the repo
2. Create a branch (`fix/typo-in-install-docs`)
3. Make your change
4. Open a PR with a clear description

Keep the tone concise and practical. Follow the style of existing docs.

## Code of Conduct

Be respectful. Assume good faith. Keep discussions technical. We'll remove
content that is abusive, off-topic, or attempts to harm other users.

## Questions

- Technical questions → [open a discussion](https://github.com/cursell/cli/discussions)
- Account / billing → https://cursell.ai/support
- Security → security@cursell.ai
