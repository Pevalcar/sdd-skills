---
name: sdd-implement
description: "Implementa una sola tarea de tasks.md con tests primero. Pausa al terminar. Usa el ciclo incremental: Implement → Test → Verify → Commit."
disable-model-invocation: true
---

# Implementador SDD — Una tarea a la vez

Implementa tareas pequeñas siguiendo TDD y el plan. Usa el ciclo incremental: Implement → Test → Verify → Commit.

## 🛡️ ASSUMPTIONS I'M MAKING:

1. La tarea Tn existe en `specs/NNN-xxx/tasks.md` y no tiene otros trabajos pendientes
2. El test framework está configurado (pytest/Jest/GUT según perfil detectado)
3. Las dependencias necesarias ya existen en el proyecto
4. La spec, plan y tasks están aprobados por el humano
5. **PARAR después de cada tarea:** no continuar con T(n+1) sin aprobación explícita
→ Correct me now or I'll proceed.

## When to Use

- Task específica marcada para implementar
- TDD flow requerido (red-green-refactor)
- Una tarea a la vez, verificar al finalizar
- Implementation touches more than one file

## When NOT to Use

- Task ya completada ([x] marcado)
- Tarea no aprobada (verificar en tasks.md y `.sdd-state.json`)
- Múltiples tareas pendientes (hacer una a la vez)
- Sin task list disponible (/sdd-tasks first)
- Single-line fix where scope is already minimal

## The Increment Cycle

```
┌──────────────────────────────────────┐
│                                      │
│   Implement ──→ Test ──→ Verify ──┐  │
│       ▲                           │  │
│       └───── Commit ◄─────────────┘  │
│              │                       │
│              ▼                       │
│          Next slice                  │
│                                      │
└──────────────────────────────────────┘
```

Para cada slice:

1. **Implement** the smallest complete piece of functionality
2. **Test** — run the test suite (or write a test if none exists)
3. **Verify** — confirm the slice works as expected (tests pass, build succeeds, manual check)
4. **Commit** -- save your progress with a descriptive message
5. **Move to the next slice** — carry forward, don't restart

## Rule 0: Simplicity First

Before writing any code, ask: "What is the simplest thing that could work?"

After writing code, review it against these checks:
- Can this be done in fewer lines?
- Are these abstractions earning their complexity?
- Would a staff engineer look at this and say "why didn't you just..."?
- Am I building for hypothetical future requirements, or the current task?

**SIMPLICITY CHECK:**
```
✗ Generic EventBus with middleware pipeline for one notification
✓ Simple function call

✗ Abstract factory pattern for two similar components  
✓ Two straightforward components with shared utilities

✗ Config-driven form builder for three forms
✓ Three form components
```

## Rule 0.5: Scope Discipline

Touch only what the task requires.

**Do NOT:**
- "Clean up" code adjacent to your change
- Refactor imports in files you're not modifying
- Remove comments you don't fully understand
- Add features not in the spec because they "seem useful"
- Modernize syntax in files you're only reading

If you notice something worth improving outside your task scope, note it — don't fix it:

```
NOTICED BUT NOT TOUCHING:
- src/utils/format.ts has an unused import (unrelated to this task)
- The auth middleware could use better error messages (separate task)
→ Want me to create tasks for these?
```

## Process

1. **Verifica gate.** La tarea Tn debe estar aprobada (checkbox sin marcar en tasks.md). Si no está en la lista, ejecutar `/sdd-tasks` primero.
2. **Lee la tarea.** `specs/001-xxx/tasks.md`, Tn elegida por el usuario
3. **Lee el plan.** `specs/001-xxx/plan.md`
4. **Lee la spec.** `specs/001-xxx/spec.md`
5. **Write test first.** Crea el test que cubra los RF indicados. Debe fallar (RED).
6. **Write minimal code.** Solo para pasar el test (GREEN).
7. **Run test.** Verifica que pasa.
8. **Refactor if needed.** Clean up without changing behavior.
9. **Commit.** Guardar progreso con mensaje descriptivo.
10. **Verify RF covered.** Menciona qué RF cubiste: `RF cubierto: RF-X, RF-Y`
11. **MARCAR [x] Tn en tasks.md y PARAR.** No empezar T(n+1) sin aprobación explícita del usuario.

## Ejecución de tests

### Godot (GUT)
```bash
Godot_console.exe --headless --path godot-client -s addons/gut/gut_cmdln.gd -gdir=res://test -gexit
```

### Python/pytest
```bash
pytest -q tests/
```

### JavaScript/Jest
```bash
npm test -- --testNamePattern="Tn"
```

## Output

- Código en `src/` o `habits/` según el proyecto
- Tests en `test/` o `tests/`
- tasks.md actualizado con `[x]` Tn
- Cambios commitados con mensaje descriptivo

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Es pequeño, no necesito tests"* | Cambios pequeños sin tests causan regresiones silenciosas | Tests obligatorios para lógica crítica |
| *"Tragamos la excepción para no romper flow"* | Errores ocultos peores que fallos explícitos | Capturar, registrar, fallar controladamente |
| *"Dejo código comentado, lo limpio después"* | Código muerto degrada mantenibilidad | Eliminar inmediatamente |
| *"Ignoro warnings del linter"* | Warnings acumulados esconden bugs latentes | Zero-warnings policy obligatorio |
| *"Es más rápido hacerlo todo junto"* | Bugs compound. Un bug en Slice 1 hace equivocado Slices 2-5 | Testear cada slice |
| *"No necesito feature flag"* | Si el feature no está completo, no debe ser visible | Agregar flag ahora |

## Red Flags

- More than 100 lines of code written without running tests
- Multiple unrelated changes in a single increment
- "Let me just quickly add this too" scope expansion
- Skipping the test/verify step to move faster
- Build or tests broken between increments
- Large uncommitted changes accumulating

## Verification

Antes de declarar tarea completada:

- [ ] The change does one thing and does it completely
- [ ] Every new behavior has a corresponding test
- [ ] The full test suite passes (repository's test command)
- [ ] Build succeeds (repository's build command)
- [ ] Type checking passes, where applicable (`npx tsc --noEmit`, `mypy`, ...)
- [ ] Linting passes (repository's lint command)
- [ ] No tests were skipped or disabled
- [ ] No debug logs o código temporal dejado atrás
- [ ] Linter/compiler passes con cero warnings
- [ ] Changes committed with descriptive message
- [ ] RF cubiertos documentados

## See Also

Per-skill verification is the local check. Before declaring a task done, apply the project-wide Definition of Done as the final gate, the standing bar every increment clears regardless of the task. See `references/definition-of-done.md`.