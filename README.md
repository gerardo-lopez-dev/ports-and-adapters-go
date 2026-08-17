# Ports and Adapters - Go

Hexagonal architecture (ports and adapters) implementation in Go.

## Requirements

- Go 1.26+

## Project Structure

```
cmd/server/          → Entry point (main.go)
config/              → Application configuration
internal/
  domain/            → Entities and business rules (no external dependencies)
  application/       → Use cases (input/output ports)
  adapters/
    in/              → Input adapters (HTTP, gRPC, CLI)
    out/             → Output adapters (DB, external APIs)
  infrastructure/    → Infrastructure configuration
migrations/          → Database migrations
```

## Architecture Rules

1. **Pure domain**: `internal/domain/` cannot import anything outside itself
2. **Ports over adapters**: Define interfaces in `application/`, implement in `adapters/`
3. **Inward dependency**: Adapters depend on domain, never the reverse
4. **Unit tests**: Every domain and application file must have its `_test.go`

## Run

```sh
go run ./cmd/server
```

## Test

```sh
go test ./...
```

## Lint

```sh
gofmt -l .
go vet ./...
```

## Commits

Format: Conventional Commits (`feat:`, `fix:`, `refactor:`, `docs:`, `test:`)

## License

[MIT](LICENSE)
