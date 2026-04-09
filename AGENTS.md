# Notely (learn-cicd-starter)

## Build & Run

```bash
go build -o notely && ./notely
```

Requires `.env` with `PORT="8080"`. Runs without a database (CRUD endpoints disabled if `DATABASE_URL` is unset).

## Database & Codegen

- sqlc generates `internal/database/*.sql.go` from `sql/schema` and `sql/queries`
- Run `sqlc generate` after modifying SQL files
- Migrations via goose: `scripts/migrateup.sh` (runs `goose turso $DATABASE_URL up`)

## Production Build

```bash
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o notely
```

Linux amd64 target is required for the Docker image (debian:stable-slim).

## Dependencies

- Go 1.22+ (CI tests on 1.26.0)
- chi router, libsql-client-go, godotenv
