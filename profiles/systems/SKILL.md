---
name: profile-systems
description: "Reglas específicas para sistemas/backend (Rust, Go, Python, C#, Java, etc.)"
---

# Perfil: Systems/Backend Development

Reglas específicas para proyectos backend, sistemas, CLI tools y servicios.

## Cuándo Cargar

| Indicadores | Acciona este perfil |
|-------------|---------------------|
| `Cargo.toml` presente | Rust projects |
| `go.mod` presente | Go projects |
| `pyproject.toml`, `requirements.txt` | Python projects |
| `pom.xml`, `build.gradle` | Java/Kotlin projects |
| `.csproj`, `*.sln` | C#/.NET projects |
| `composer.json` | PHP projects |

## Reglas Específicas por Lenguaje

### Rust
- Ownership/borrowing principles first
- `Result<T, E>` handling mandatory (no unwrap on production code)
- `clippy` warnings must be zero
- `rustfmt` formatting required
- Documentation comments (`///`) for public APIs

### Go
- `err != nil` checks mandatory
- Interface segregation (small, focused interfaces)
- Standard library first, avoid over-abstraction
- `gofmt` required
- `golint`/`staticcheck` warnings addressed

### Python
- Type hints for function signatures
- `mypy` type checking
- Pydantic models for data validation
- `black` formatting, `ruff` linting
- Virtual environments for dependencies

### C#/.NET
- Async/await properly used (no `.Result` blocking)
- Pattern matching where appropriate
- Dependency injection configured
- `dotnet format` applied
- Nullable reference types enabled

## Patterns Obligatorios

### Error Handling
```rust
// Bad
let value = result.unwrap();

// Good
match result {
    Ok(v) => v,
    Err(e) => return Err(Error::from(e)),
}
```

```go
// Bad
value := doSomething()

// Good
value, err := doSomething()
if err != nil {
    return nil, fmt.Errorf("operation failed: %w", err)
}
```

### Logging
- Structured logging (JSON format when possible)
- Log levels: DEBUG, INFO, WARN, ERROR
- Include correlation IDs for distributed tracing
- Never log sensitive data (passwords, tokens, PII)

### Configuration
- Environment variables for secrets
- Config files for non-sensitive settings
- Validation at startup (fail fast)
- Default values documented

## Dependencies
- Justify every external dependency
- Pin versions explicitly
- Regular security audits (`cargo audit`, `npm audit`, `pip-audit`)
- Prefer well-maintained, widely-used libraries

## Commands Comunes

| Language | Type Check | Lint | Test | Build |
|----------|-----------|------|------|-------|
| Rust | `cargo check` | `cargo clippy` | `cargo test` | `cargo build` |
| Go | `go vet` | `golangci-lint` | `go test` | `go build` |
| Python | `mypy` | `ruff`/`flake8` | `pytest` | `python -m build` |
| C# | `dotnet build` | `dotnet format` | `dotnet test` | `dotnet publish` |

## Anti-Patterns Específicos

| Anti-pattern | Problema | Alternativa |
|-------------|----------|-------------|
| Global mutable state | Hard to test, race conditions | Dependency injection, immutable data |
| Magic numbers/strings | Unclear intent, hard to maintain | Named constants/enums |
| God objects/functions | Complex, untestable | Single responsibility decomposition |
| Deep inheritance hierarchies | Fragile, tight coupling | Composition over inheritance |
| Premature optimization | Wrong targets, unreadable code | Measure first, optimize after |

## Verification Checklist

- [ ] Compiles without errors or warnings
- [ ] Linter passes with zero issues
- [ ] Unit tests pass
- [ ] Integration tests pass (if applicable)
- [ ] Error handling covers all failure paths
- [ ] Logs are structured and informative
- [ ] No sensitive data in logs/config
- [ ] Dependencies audited and justified
