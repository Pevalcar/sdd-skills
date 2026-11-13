---
name: sdd-tasks
description: Genera tasks.md con tareas pequeñas, verificables y ordenadas por dependencia.
disable-model-invocation: true
---

# Generador de tareas SDD

Descompone el plan en tareas implementables paso a paso.

## 🛡️ ASUMPTIONS I'M MAKING:

1. El plan técnico existe en `specs/NNN-xxx/plan.md`
2. Las tareas serán ≤ 30 minutos cada una
3. El orden debe seguir dependencias naturales (no importancia percibida)
→ Correct me now or I'll proceed.

## When to Use

- Plan aprobado existe
- Necesito descomponer trabajo en unidades implementables
- Quiero visualizar dependencias y checkpointing

## When NOT to Use

- Sin plan todavía (/sdd-plan first)
- Cambios muy pequeños (una función, un fix)
- Plan ya existe con tasks.md sin completar

## Process

1. **Lee la spec.** `specs/001-xxx/spec.md`
2. **Lee el plan.** `specs/001-xxx/plan.md`
3. **Genera `tasks.md`** con formato:

## Formato output

```markdown
# Tareas — 001-xxx

- [ ] T1: <descripción (≤30 min)>
  - RF: RF-1, RF-3
  - Hecho cuando: <verificable, test pasa>

- [ ] T2: <descripción>
  - RF: RF-2, RF-4
  - Hecho cuando: <verificable>
```

**Reglas:**
- Cada tarea ≤ 30 minutos
- Orden por dependencia (T1 → T2 → T3)
- Cada RF cubierto al menos una vez
- "Hecho cuando" debe ser verificable automáticamente (test, output específico)

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Las tareas son obvias"* | Escribir tasks surface hidden dependencies and forgotten edge cases | Write them down anyway |
| *"Planning es overhead"* | Planning IS the task. Without it, implementation is guessing | 10 min planning saves hours |
| *"Ya tengo(tasks en mi cabeza"* | Context windows有限. External tracker needed | tasks/todo.md or external system required |
| *"Overwriting existing plan es ok"* | Unchecked tasks may be mid-build in another session | Stop and ask first |

## Verification

- [ ] Todas las tasks have acceptance criteria
- [ ] Cada tarea verificable automáticamente ("Hecho cuando" claro)
- [ ] Task dependencies identified and ordered correctly
- [ ] Tasks recorded in tasks/todo.md o tracker externo designado
- [ ] No pre-existing incomplete plan overwritten without explicit confirmation
- [ ] Human reviewed and approved the task list