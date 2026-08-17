# AGENTS.md

Reglas vinculantes para agentes que trabajan en este repo.

## Qué es este repo

`ports-and-adapters-go` es una implementación de arquitectura hexagonal (puertos y adaptadores) en Go.

## Estructura del proyecto

```
cmd/server/          → Punto de entrada (main.go)
config/              → Configuración de la aplicación
internal/
  domain/            → Entidades y reglas de negocio (sin dependencias externas)
  application/       → Casos de uso (puertos de entrada/salida)
  adapters/
    in/              → Adaptadores de entrada (HTTP, gRPC, CLI)
    out/             → Adaptadores de salida (DB, APIs externas)
  infrastructure/    → Configuración de infraestructura
migrations/          → Migraciones de base de datos
```

## Reglas

1. **Dominio puro**: `internal/domain/` no puede importar nada fuera de `internal/domain/`.
2. **Puertos sobre adaptadores**: Definir interfaces en `application/`, implementar en `adapters/`.
3. **Dependencia hacia adentro**: Los adaptadores dependen del dominio, nunca al revés.
4. **Tests unitarios**: Cada archivo de dominio y aplicación debe tener su `_test.go`.
5. **Sin dependencias externas innecesarias**: Usar stdlib cuando sea posible.
6. **Convenciones Go**: Seguir `gofmt`, `go vet`, `staticcheck`.

## Comandos útiles

```sh
# Ejecutar
go run ./cmd/server

# Testear
go test ./...

# Lint
gofmt -l .
go vet ./...
```

## Commits

- Formato: Conventional Commits (`feat:`, `fix:`, `refactor:`, `docs:`, `test:`)
- Un cambio lógico por commit
- Mensajes en inglés, claros y concisos

## Ramas

- `main`: producción, siempre funcional
- `feat/*`: nuevas features
- `fix/*`: correcciones de bugs
- `refactor/*`: reestructuración sin cambio de comportamiento

## Referencias

- `docs/` — documentación del proyecto y twelve-factor app
- `README.md` — instrucciones de uso
