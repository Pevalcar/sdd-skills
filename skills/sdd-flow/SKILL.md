---
name: sdd-flow
description: "Orquesta todo el flujo SDD: setup → spec → clarify → plan → tasks → implement → validate. Un wizard interactivo que respeta verification gates."
disable-model-invocation: true
---

# Wizard SDD — Desarrollo guiado por especificación

Orquesta todo el flujo Spec-Driven Development como un asistente interactivo.

## 🛡️ ASUMPTIONS I'M MAKING:

1. El repositorio tiene un directorio de trabajo válido
2. Usuario quiere iniciar nuevo flujo SDD o reanudar existente
3. `.sdd-state.json` puede existir con estado previo
4. Los 5 perfiles están instalados en `.agents/skills/profiles/`
5. El reference library de skills está disponible para routing
→ Correct me now or I'll proceed.

## When to Use

- Start nuevo proyecto desde cero (sin AGENT.md)
- Reanudar flujo interrumpido (`/sdd-flow resume`)
- Ejecutar pipeline completo sin pasos manuales
- Need to discover which skill to use first

## When NOT to Use

- Ya estás en medio de un flujo manual
- Solo necesitas un skill específico (usar directamente)
- Proyecto no tiene specs iniciales

## Usage

Invoca con una idea:
```
/sdd-flow "funcionalidad: login Dofus"
/sdd-flow "CLI para hábitos: add, done, list"
/sdd-flow --skip-constitution "login básico"
```

## Estado del flujo

Guarda estado en: `.sdd-state.json`

```json
{
  "version": "2.1.0",
  "current_phase": "spec",
  "approved_phases": ["setup", "constitution"],
  "profiles_active": ["web-frontend"],
  "specs_count": 1,
  "tasks_total": 0,
  "tasks_completed": 0,
  "last_checkpoint": "2026-01-15T10:30:00Z"
}
```

## El Flow Completo

### Phase 0: Setup
**Invoca:** `/sdd-setup` → `/sdd-constitution`
- Verificar si `AGENT.md` existe
- Verificar si `docs/constitution.md` existe
- Crear ambos si no existen
- **PAUSED:** Espera aprobación humana

### Phase 1: Especificación (SPEC)
**Invoca:** `/sdd-spec`
- Entrevista secuencial (máx 6 preguntas)
- Genera `specs/001-xxx/spec.md` con:
  - Objective
  - Tech Stack
  - Commands
  - Project Structure
  - Testing Strategy
  - Boundaries (Always/Ask/Never)
  - Success Criteria (RF en EARS)
- **PAUSED:** Espera aprobación humana antes de continuar

### Phase 2: Clarificación QA (loop)
**Invoca:** `/sdd-clarify`
- Lee spec + constitution
- Detecta: ambigüedades, contradicciones, casos faltantes
- QA automático
- Agrega sección `Revisión QA` al spec
- **PAUSED:** Preguntar: "¿Spec clarificada? Sí / No (volver a clarify)"
- **LOOP:** Si no, volver a sdd-clarify hasta que esté claro

### Phase 3: Planificación
**Invoca:** `/sdd-plan`
- Lee spec + constitution
- Genera `specs/001-xxx/plan.md`:
  - Módulos y dependencias (diagrama)
  - Modelo de datos con ejemplo JSON
  - Algoritmo principal (pseudocódigo)
  - Contrato CLI
  - Decisiones técnicas + alternativas descartadas
  - Cobertura RF por módulo
- **PAUSED:** Espera aprobación humana antes de continuar

### Phase 4: Tareas
**Invoca:** `/sdd-tasks`
- Genera `specs/001-xxx/tasks.md`
- Tareas ≤ 30 min cada una
- Orden por dependencia
- Checkbox con "Hecho cuando:" verificable
- **PAUSED:** Espera aprobación humana

### Phase 5: Implementación (TDD por tarea)
**Invoca:** `/sdd-implement`

Por iteración:
1. Lee Tn, plan, spec
2. Escribe test primero (falla → rojo)
3. Escribe código mínimo (pasa → verde)
4. Ejecuta test suite
5. Refactor si necesario
6. Commit cambios
7. Marca `[x] Tn` en tasks.md
8. **PAUSED:** "Tarea Tn completada. ¿Continuar con T(n+1)?"

### Phase 6: Validación final
**Invoca:** `/sdd-validate`
- Recorrido RF por RF
- Qué test cubre cada uno
- Estado: ✅ PASA / ❌ FALLA / ⚠️ SIN TEST
- Veredicto: "✅ Spec cumplida" o lista pendientes

### Phase 7: Variants (opcional)
**Invoca:** `/sdd-variants`
- Generar N variantes de implementación
- Evaluar vs AC/constitución/simplicidad
- Producir `variants-ranking.md` con shortlist ranqueada
- **OPCIONAL:** Solo si el usuario quiere explorar alternativas

## Control del wizard

| Comando | Acción |
|---------|--------|
| `/sdd-flow resume` | Reanuda desde último step |
| `/sdd-flow skip <step>` | Salta un paso |
| `/sdd-flow reset` | Reinicia el flujo |
| `/sdd-flow show` | Muestra estado actual |
| `/sdd-discover` | Ejecuta descubrimiento de perfil primero |

## Verification Gates

El wizard respeta los gates de verificación:

```
SETUP → SPEC → PLAN → TASKS → IMPLEMENT
   │        │        │        │         │
   ▼        ▼        ▼        ▼         ▼
 HUMAN    HUMAN    HUMAN    HUMAN     HUMAN
 REVIEW   REVIEW   REVIEW   REVIEW    REVIEW
```

Cada fase tiene un checklist de verificación que debe pasarse:
- **sdd-setup:** AGENT.md + constitution creados y aprobados
- **sdd-spec:** 6 áreas core completadas
- **sdd-plan:** Arquitectura validada
- **sdd-tasks:** Tasks son accionables
- **sdd-implement:** Tests pasan, code review hecho
- **sdd-validate:** DoD checklist pasado

## Output esperado

Al finalizar, tendrás:
- `AGENT.md` (raíz del proyecto)
- `CLAUDE.md` (raíz del proyecto, referencia a AGENT.md)
- `docs/constitution.md`
- `specs/001-xxx/spec.md`
- `specs/001-xxx/plan.md`
- `specs/001-xxx/tasks.md`
- Tests pasando 100%
- Código mínimo que cumple spec
- `specs/001-xxx/VALIDATION.md`

## Reglas del wizard

- **Un paso a la vez.** Pausa después de cada output
- **Aprobación explícita.** No avanza sin el usuario
- **Tests primero.** TDD obligatorio
- **Verificables.** "Hecho cuando" debe poder automatizarse
- **One assumption at a time.** Surface assumptions before each major step
- **Stop after spec.** Once spec is written, STOP until human approval
- **Clarify loop.** Keep asking until spec is crystal clear

## See Also

- `/sdd-discover` - Detect profile and current state
- `spec-driven-development` - Full spec pattern from reference
- `incremental-implementation` - Incremental build cycle
- `test-driven-development` - Testing patterns
- `definition-of-done.md` - Universal quality bar