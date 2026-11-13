# Gates de Verificación — Universal

Checklist transversal que debe cumplirse ANTES de marcar cualquier tarea como completada.

---

## Pre-flight (Antes de Empezar)

- [ ] He identificado el perfil del proyecto (web/systems/game-dev/mobile/infrastructure)
- [ ] He leído los archivos de configuración relevantes
- [ ] He listado mis suposiciones explícitas (ASSUMPTIONS section)
- [ ] Entiendo qué cambios impacta esta tarea y sus dependencias
- [ ] Confirmé que la spec/requerimiento existe y está aprobado

---

## Durante la Implementación

- [ ] Sigo el patrón existente en el repositorio (naming, estructura, conventions)
- [ ] No agrego dependencias sin justificación documentada
- [ ] No refactorizo código no relacionado con la tarea
- [ ] Mantengo el código dentro del scope acordado
- [ ] DocumentO decisiones importantes inline si no cabe en el commit message

---

## Post-flight (Al Terminar)

### Sintaxis y Tipado
- [ ] El código compila/type-check sin errores ni warnings
- [ ] Linter pasa sin errores (zero-warnings policy)
- [ ] Formateador aplicado consistentemente

### Pruebas
- [ ] Tests asociados pasan (unidad, integración según corresponda)
- [ ] Coverage no disminuyó
- [ ] Edge cases cubiertos
- [ ] Tests manuales ejecutados si aplica

### Limpieza
- [ ] Sin archivos temporales
- [ ] Sin logs de depuración (`console.log`, `print`, etc.)
- [ ] Sin código comentado sin justificación
- [ ] Sin imports/dependencias no usadas

### Funcionalidad
- [ ] Comportamiento esperado verificado en runtime
- [ ] Spec original sigue cubierta
- [ ] No hay regressions (tests previos siguen pasando)
- [ ] Casos límite considerados

### Documentación
- [ ] Code comments explican WHY, no WHAT
- [ ] README/CHANGELOG actualizados si aplica
- [ ] ADR creado para decisiones arquitectónicas relevantes

### Seguridad (si aplica)
- [ ] Inputs validados
- [ ] Secrets no hardcodeados
- [ ] Permissions mínimos requeridos

---

## Por Perfil

### Web/Frontend Adicionales
- [ ] TypeScript strict mode passes
- [ ] Accessibility audit (basic): aria labels, keyboard nav
- [ ] Browser devtools clean (no console errors)
- [ ] Bundle size no aumentó significativamente

### Systems Adicionales
- [ ] Memory sanitizer clean (valgrind/address-sanitizer)
- [ ] Race condition analysis (data race detector)
- [ ] Error propagation tested

### Game Dev Adicionals
- [ ] Determinism verified (same input → same output across runs)
- [ ] Frame timing acceptable (< target frame time)
- [ ] Network packet sizes validated
- [ ] State machine transitions complete (no stuck states)

### Mobile Additional
- [ ] Lifecycle tested (background/foreground)
- [ ] Orientation change handled
- [ ] Low memory warning handled
- [ ] Battery impact acceptable

### Infrastructure Additional
- [ ] Docker build successful
- [ ] Config schema validated
- [ ] Rollback plan documented
- [ ] Monitoring/alerting in place

---

## Sign-offs Requeridos

| Cambio | Requiere |
|--------|----------|
| Bug fix menor | Auto-verificación |
| Nueva funcionalidad | Revisión de par |
| Cambio架构tural | Approbación del equipo |
| Fix de seguridad | Revisión especializada |

---

## Flow de Ejecución

```
Inicio de tarea
    │
    ▼
Pre-flight checklist ──→ Fallo? → documentar bloqueantes
    │
    ▼
Implementación
    │
    ▼
Post-flight checklist ──→ Fallo? → reparar antes de continuar
    │
    ▼
Sign-off required? ──→ Yes: request review
    │
    ▼
Task complete ✓
```
