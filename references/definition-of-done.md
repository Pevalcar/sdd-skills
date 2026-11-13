# Definition of Done — Universal

Barra de calidad universal que TODO cambio debe cumplir antes de considerarse terminado. Diferente de los acceptance criteria (que son por tarea), el DoD es fijo y aplicable a todo.

---

## El Checklist Definitivo

Aplicar a TODO cambio antes de declararlo done.

### Correctness (Correctitud)
- [ ] Todos los acceptance criteria de la tarea están cumplidos
- [ ] El código se ejecuta y se comporta según lo esperado (verificado en runtime, no solo compilando)
- [ ] Nuevos comportamientos tienen tests que fallan sin el cambio y pasan con él
- [ ] Tests existentes siguen pasando (sin regresiones)
- [ ] Edge cases y paths de error están manejados, no solo happy path

### Quality (Calidad)
- [ ] El código revela intención mediante naming y estructura (no necesita comentarios explicativos)
- [ ] Sin lógica de negocio duplicada
- [ ] Sin código muerto, output de debug o bloques comentados abandonados
- [ ] Cambios scoped a la tarea; no hay refactors no solicitados
- [ ] Linting y formatting pasan sin warnings
- [ ] Type checking pasa (donde aplica): `tsc --noEmit`, `mypy`, `cargo check`, `go vet`

### Maintainability (Mantenibilidad)
- [ ] Funciones y métodos tienen un solo propósito claro
- [ ] Complejidad ciclomédica aceptable (<10 por función)
- [ ] Dependency graph no tiene cycles
- [ ] Código nuevo no requiere bloques try/catch vacíos
- [ ] No se introdujeron nuevas dependencias sin justificación documentada

### Security (Seguridad)
- [ ] Inputs no confiables validados y sanitizados
- [ ] Secrets/credentials no hardcodeados
- [ ] Auth zona crítica (si aplica)
- [ ] SQL injection, XSS, CSRF considerados (si aplica)
- [ ] No se expuso información sensible en logs

### Integration (Integración)
- [ ] El cambio funciona con el resto del sistema, no solo aislado
- [ ] Migraciones de base de datos, cambios de configuración y feature flags accounted for
- [ ] Backward compatibility considerado para interfaces/APIs públicas

### Documentation (Documentación)
- [ ] Interfaces públicas, APIs y comportamiento usuario documentado
- [ ] Decisiones arquitectónicas importantes registradas (ADR si aplica)
- [ ] Documentación describe estado actual en lenguaje atemporal, no historial de cambios

### Observability (Observabilidad)
- [ ] Logs estructurados con contexto relevante
- [ ] Métricas agregadas para performance crítico
- [ ] Traces disponibles para debug en staging
- [ ] Error rates y latency monitoring configurado

### Ship-readiness (Listo para Producción)
- [ ] Implicaciones de seguridad revisadas para inputs no confiables, auth, manejo de datos
- [ ] Observabilidad presente en nuevos critical paths (logs, métricas, traces)
- [ ] Path de rollback existe para cambios riesgosos
- [ ] El humano ha revisado y aprobado antes de merge/deploy

---

## DoD vs Acceptance Criteria

| Aspecto | Acceptance Criteria | Definition of Done |
|---------|---------------------|-------------------|
| Scope | Específico de una tarea o spec | Aplica a cada increment |
| Cambia | Diferente para cada item | Fijo y reutilizable |
| Responde | "¿Construimos ESTA cosa?" | "¿Está LISTA?" |
| Owner | Definido al planificar la tarea | Definido una vez para el proyecto |
| Ejemplo | "El usuario puede resetear contraseña" | "Tests pasan, sin regressions, docs actualizadas" |

Son complementarios. Una tarea está done cuando AMBOS se cumplen.

---

## How to Apply

- **Por tarea:** Confirmar Correctness, Quality, y Maintainability antes de marcar tarea completada
- **Por feature:** Confirmar Integration, Documentation, y Observability antes de considerar feature complete
- **Por release:** La checklist completa es el piso; añadir gates específicos de deploy

Tailorizar la lista UNA VEZ para el proyecto, luego reutilizarla sin renegociar. Un DoD que se renegocia cada sprint no es un Definition of Done.

---

## Red Flags

- "Está listo, solo no lo he ejecutado todavía": trabajo no verificado NO está listo
- "Tests pasan" usado como sinónimo de done mientras se saltan docs, regresiones o verificación runtime
- Una barra diferente aplicada dependiendo de presión de deadline
- Acceptance criteria tratados como la única medida, sin floor de calidad
- "Done" declarado antes de revisión humana en cambios que la requieren
- Código agregado sin pruebas equivalentes a la funcionalidad agregada
- Refactors no documentados o sin pruebas de comportamiento

---

## Per-Profile Extensions

### Web Frontend
- [ ] Type checking pasa (`tsc --noEmit`)
- [ ] ESLint no reporta errores
- [ ] Build de producción exitoso
- [ ] Tests críticos pasan en navegadores reales

### Systems (Rust/Go/Python)
- [ ] `cargo clippy` sin warnings (Rust)
- [ ] `go vet` sin errores (Go)
- [ ] `mypy` sin errores (Python)
- [ ] Zero compiler warnings

### Game Dev (Godot)
- [ ] Determinismo verificado (same frame count)
- [ ] Physics stability confirmada
- [ ] Memory usage within bounds
- [ ] Headless tests pasan

### Mobile
- [ ] Native build exitoso
- [ ] Memory leak scan limpio
- [ ] Lifecycle methods manejados
- [ ] Device tests pasan (simulator/emulator)

### Infrastructure
- [ ] Container scan sin vulnerabilidades críticas
- [ ] `terraform fmt` pasa
- [ ] `docker-compose config` valido
- [ ] Security posture verificada

---

## Quick Reference Checklist

```
[ ] Correctness: Tests + Behavior + Edge Cases
[ ] Quality: Clean Code + No Warnings
[ ] Maintainability: Simple + Clear + Tests
[ ] Security: Input Validation + No Secrets
[ ] Integration: Works + Compatible
[ ] Documentation: Docs + ADRs (if needed)
[ ] Observability: Logs + Metrics + Traces
[ ] Ship-ready: Rollback + Human Approval
```