---
name: sdd-implement
description: Implementa una sola tarea de tasks.md con tests primero. Pausa al terminar.
disable-model-invocation: true
---

# Implementador SDD — Una tarea a la vez

Implementa tareas pequeñas siguiendo TDD y el plan.

## 🛡️ ASUMPTIONS I'M MAKING:

1. La tarea Tn existe en `specs/NNN-xxx/tasks.md` y no tiene otros trabajos pendientes
2. El test framework está configurado (pytest/Jest/GUT según perfil detectado)
3. Las dependencias necesarias ya existen en el proyecto
→ Correct me now or I'll proceed.

## When to Use

- Task específica marcada para implementar
- TDD flow requerido (red-green-refactor)
- Una tarea a la vez, verificar al finalizar

## When NOT to Use

- Task ya completada ([x] marcado)
- Múltiples tareas pendientes (hacer una a la vez)
- Sin task list disponible (/sdd-tasks first)

## Process

1. **Lee la tarea.** `specs/001-xxx/tasks.md`, Tn elegida por el usuario
2. **Lee el plan.** `specs/001-xxx/plan.md`
3. **Lee la spec.** `specs/001-xxx/spec.md`
4. **Escribe test primero.** Crea el test que cubra los RF indicados
5. **Ejecuta test.** Debe fallar (rojo)
6. **Escribe código mínimo.** Solo para pasar el test
7. **Ejecuta test.** Debe pasar (verde)

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

## Reglas

- Solo una tarea a la vez
- Tests primero, código mínimo
- Pausa al terminar: "Hecho Tn. ¿Continuar con T(n+1)?"
- Verifica RF cubiertos: `RF cubierto: RF-X, RF-Y`

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Es pequeño, no necesito tests"* | Cambios pequeños sin tests causan regresiones silenciosas | Tests obligatorios para lógica crítica |
| *"Tragamos la excepción para no romper flow"* | Errores ocultos peores que fallos explícitos | Capturar, registrar, fallar controladamente |
| *"Dejo código comentado, lo limpio después"* | Código muerto degrada mantenibilidad | Eliminar inmediatamente |
| *"Ignoro warnings del linter"* | Warnings acumulados esconden bugs latentes | Zero-warnings policy obligatorio |
| *"Parche temporal es más rápido"* | Parches se acumulan y rompen arquitectura | Código limpio desde el inicio |

## Verification

Antes de declarar tarea completada:

- [ ] Test wrote first (RED phase), then code (GREEN phase)
- [ ] Test passes after implementation (GREEN)
- [ ] RF specified in task covered by tests
- [ ] tasks.md updated con `[x] Tn` marked complete
- [ ] No debug logs o code temporales left behind
- [ ] Linter/compiler passes con cero warnings