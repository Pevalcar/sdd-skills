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

### Integration (Integración)
- [ ] El cambio funciona con el resto del sistema, no solo aislado
- [ ] Migraciones de base de datos, cambios de configuración y feature flags accounted for
- [ ] Backward compatibility considerado para interfaces/APIs públicas

### Documentation (Documentación)
- [ ] Interfaces públicas, APIs y comportamiento usuario documentado
- [ ] Decisiones arquitectónicas importantes registradas (ADR si aplica)
- [ ] Documentación describe estado actual en lenguaje atemporal, no historial de cambios

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

- **Por tarea:** Confirmar Correctness y Quality antes de marcar tarea completada
- **Por feature:** Confirmar Integration y Documentation antes de considerar feature complete
- **Por release:** La checklist completa es el piso; añadir gates específicos de deploy

Tailorizar la lista UNA VEZ para el proyecto, luego reutilizarla sin renegociar. Un DoD que se renegotea cada sprint no es un Definition of Done.

---

## Red Flags

- "Está listo, solo no lo he ejecutado todavía": trabajo no verificado NO está listo
- "Tests pasan" usado como sinónimo de done mientras se saltan docs, regresiones o verificación runtime
- Una barra diferente aplicada dependiendo de presión de deadline
- Acceptance criteria tratados como la única medida, sin floor de calidad
- "Done" declarado antes de revisión humana en cambios que la requieren
