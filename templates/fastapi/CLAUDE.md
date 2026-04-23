# CLAUDE.md

## Project context

A FastAPI service running on Python 3.12 with async-first design, served behind nginx in production. Uses PostgreSQL and Redis.

## Stack & conventions

- Language: Python 3.12, type hints required on all public functions
- Framework: FastAPI (async route handlers)
- Async runtime: `asyncio` + `uvicorn`
- Validation: Pydantic v2 models for request/response bodies
- Package manager: `uv` (replaces pip + venv)
- Important libraries: `fastapi`, `pydantic`, `sqlalchemy[asyncio]`, `asyncpg`, `redis.asyncio`

## Commands

```bash
uv sync                        # install
uv run uvicorn app.main:app --reload --port 8000  # dev
uv run pytest                  # test
uv run ruff check .            # lint
uv run ruff format .           # format
uv run mypy app/               # typecheck
uv run alembic upgrade head    # migrate
```

## Code style

- Formatter: `ruff format` (Black-compatible)
- Linter: `ruff check` (E, F, I, B, UP rules)
- Type checker: `mypy --strict` for `app/`, lenient for tests
- Naming: snake_case throughout; PascalCase only for classes
- Async by default: every route handler `async def`, every DB call awaits
- Comments: only when the *why* is non-obvious

## What to avoid

- Do not use sync DB drivers (`psycopg2`) — use `asyncpg` via `sqlalchemy[asyncio]`
- Do not block the event loop with `time.sleep`, `requests`, or sync file I/O — use `asyncio.sleep`, `httpx.AsyncClient`, `aiofiles`
- Do not put business logic in route handlers — keep handlers thin, delegate to `app/services/`
- Do not use `BaseModel` for ORM models — use SQLAlchemy `DeclarativeBase`, Pydantic only for I/O schemas
- Do not commit `.env` — use `pydantic-settings` to read from env

## Important files

- `app/main.py` — FastAPI app construction, middleware, router registration
- `app/config.py` — Pydantic-settings config object (reads `.env`)
- `app/db.py` — async session factory, engine setup
- `app/models/` — SQLAlchemy ORM models
- `app/schemas/` — Pydantic request/response schemas
- `app/services/` — business logic
- `app/api/` — route handlers (one file per resource)
- `alembic/` — migrations
- `pyproject.toml` — `uv` deps, ruff/mypy config

---

<!-- Adapted from llmapi-pro/claude-md-templates -->
