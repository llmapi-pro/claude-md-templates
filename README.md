# CLAUDE.md Templates

> Opinionated `CLAUDE.md` templates for popular stacks, drop into your project root.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## What is `CLAUDE.md`?

[`CLAUDE.md`](https://docs.anthropic.com/claude/docs/claude-code) is a project-level instructions file that [Claude Code](https://docs.anthropic.com/claude/docs/claude-code) automatically reads when you start a session in your project. It tells Claude:

- The project's tech stack and conventions
- Build, test, and lint commands
- What patterns to follow and what to avoid
- Where the important code lives

A good `CLAUDE.md` cuts your time-to-productive-Claude-session from minutes to seconds.

## Available Templates

| Stack | Template |
|---|---|
| Next.js (App Router, TypeScript) | [templates/nextjs/CLAUDE.md](templates/nextjs/CLAUDE.md) |
| FastAPI (Python 3.12, async) | [templates/fastapi/CLAUDE.md](templates/fastapi/CLAUDE.md) |
| Express + TypeScript | [templates/express-typescript/CLAUDE.md](templates/express-typescript/CLAUDE.md) |
| Go (stdlib + minimal deps) | [templates/go/CLAUDE.md](templates/go/CLAUDE.md) |
| Generic scaffold | [templates/_scaffold/CLAUDE.md](templates/_scaffold/CLAUDE.md) |

## How to use

1. Find the template that matches your stack (or start from `_scaffold`).
2. Copy its `CLAUDE.md` to your project root.
3. Customize the sections marked `<!-- EDIT: ... -->`.
4. Commit it.

Claude Code automatically loads `CLAUDE.md` from the project root on every session.

## Template structure

Each template follows the same six-section structure:

1. **Project context** — what this is, who uses it
2. **Stack & conventions** — language, framework, key dependencies
3. **Commands** — install, dev, build, test, lint, typecheck
4. **Code style** — formatting, naming, comment policy
5. **What to avoid** — anti-patterns specific to this stack
6. **Important files** — entry points, configs, gotchas

This consistent structure makes it easy to swap templates as your stack evolves.

## Contributing

PRs adding new stacks welcome. To contribute:

1. Copy `templates/_scaffold/` to `templates/<stack-name>/`
2. Fill out all six sections with stack-specific content
3. Add an entry to the table above
4. Open a PR

Stack-specific judgment calls (e.g., "use this ORM, not that one") should be defensible — explain in PR.

## Related

- [llmapi-pro/claude-code-setup](https://github.com/llmapi-pro/claude-code-setup) — One-line installer for Claude Code with the LLM API relay backend.
- [llmapi-pro/awesome-claude-code](https://github.com/llmapi-pro/awesome-claude-code) — Curated resources for Claude Code users.

## License

[MIT](LICENSE) © 2026 Yazhou Hu
