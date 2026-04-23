# CLAUDE.md

## Project context

An Express.js API service in TypeScript, Node 20+, deployed as a Docker container.

## Stack & conventions

- Language: TypeScript 5.x, strict mode on
- Framework: Express 4.x with async route handlers
- Validation: `zod` for request body validation
- DB: `pg` (node-postgres) with raw SQL or a thin query builder
- Logging: `pino` for structured JSON logs
- Package manager: pnpm

## Commands

```bash
pnpm install
pnpm dev                      # tsx watch
pnpm build                    # tsc
pnpm start                    # node dist/server.js
pnpm test                     # vitest
pnpm lint                     # eslint
pnpm typecheck                # tsc --noEmit
```

## Code style

- Formatter: Prettier
- Linter: ESLint with `@typescript-eslint`
- Async/await everywhere; never raw promises
- Always return explicit response from handlers (`return res.json(...)`)
- Validate request bodies with `zod` schemas before touching them
- Comments: only when the *why* is non-obvious

## What to avoid

- Do not use callback-style APIs — use the promise variants (e.g., `fs/promises`)
- Do not put business logic in route handlers — extract to `services/`
- Do not throw plain strings — throw typed `Error` subclasses caught by error middleware
- Do not use `any` — use `unknown` and narrow with zod
- Do not call `process.exit` outside of startup error paths

## Important files

- `src/server.ts` — app setup, middleware chain, error handler
- `src/routes/` — route handlers (one file per resource)
- `src/services/` — business logic, side-effect-free where possible
- `src/db.ts` — connection pool
- `src/schemas/` — zod validation schemas
- `src/config.ts` — env-driven config
- `tsconfig.json` — strict mode required

---

<!-- Adapted from llmapi-pro/claude-md-templates -->
