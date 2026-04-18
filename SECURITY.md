# Security Policy

We take security seriously. Please help us keep Cursell users safe.

## Reporting a vulnerability

**Do not open a public GitHub issue for security vulnerabilities.**

Send a detailed report to **security@cursell.ai** with:

- A description of the issue
- Steps to reproduce (or proof of concept)
- Impact assessment
- Your contact information

We aim to acknowledge every report within **48 hours** and to issue a fix or
mitigation within **14 days** for confirmed high-severity issues.

## Scope

In scope:

- The `cursell` npm package (all three binaries: `cursell`, `cursell-mcp`,
  `cursell-statusline`)
- The Cursell Hub API (`api.cursell.ai`)

Out of scope:

- Social engineering / phishing
- Denial of service via rate limits
- Issues in third-party MCP clients (Claude Code, Codex CLI, Gemini CLI)
- Issues already disclosed publicly

## Supported versions

Only the latest minor release of `cursell` receives security updates. We
recommend always running `npm install -g cursell@latest`.

## Responsible disclosure

We ask that you:

- Give us reasonable time to fix the issue before public disclosure
- Do not access, modify, or delete other users' data
- Do not perform testing that degrades service for other users

We'll credit reporters in release notes unless you prefer to remain anonymous.
