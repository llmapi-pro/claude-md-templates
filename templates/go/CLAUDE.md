# CLAUDE.md

## Project context

A Go service using mostly the standard library plus a small set of carefully chosen dependencies. Single binary deploy, runs on Linux.

## Stack & conventions

- Language: Go 1.22+
- Module: enabled (`go.mod` at root)
- HTTP: `net/http` standard library + `github.com/go-chi/chi/v5` for routing
- DB: `database/sql` + `github.com/jackc/pgx/v5` for PostgreSQL
- Logging: `log/slog` (stdlib structured logging)
- Testing: `testing` package + `github.com/stretchr/testify/require` for assertions

## Commands

```bash
go mod download
go run ./cmd/server          # dev
go build -o bin/server ./cmd/server
go test ./...                # all tests
go test -race ./...          # race detector
go vet ./...                 # vet
gofmt -w .                   # format
```

## Code style

- Formatter: `gofmt` (mandatory; CI fails if not formatted)
- Errors: return as values, never panic in library code; wrap with `fmt.Errorf("doing X: %w", err)`
- Naming: idiomatic Go — short names for short scopes, descriptive for exported
- Comments: every exported identifier needs a doc comment starting with the name
- Concurrency: prefer channels for ownership transfer; use `sync.Mutex` only for protecting shared state

## What to avoid

- Do not use `interface{}` / `any` unless truly necessary — prefer concrete types or generics
- Do not catch panics with `recover()` in normal flow — only in long-running goroutines as last-resort safety
- Do not use init() for non-trivial work — explicit setup in `main` is clearer
- Do not import test helpers into production packages — keep `*_test.go` boundary clean
- Do not use ORMs — `database/sql` + `pgx` is sufficient and more transparent

## Important files

- `cmd/server/main.go` — entry point, wiring
- `internal/handlers/` — HTTP handlers
- `internal/services/` — business logic
- `internal/store/` — DB layer
- `internal/config/` — env-driven config
- `migrations/` — goose-managed SQL migrations
- `go.mod` / `go.sum` — modules

---

<!-- Adapted from llmapi-pro/claude-md-templates -->
