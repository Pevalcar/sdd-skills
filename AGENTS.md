# SDD Skills — Agent Configuration

Este directorio define el comportamiento de los agentes AI para trabajar con el sistema SDD (Spec-Driven Development).

## Perfil del Proyecto

El sistema detecta automáticamente el perfil tecnológico cargando reglas específicas desde `profiles/`:

| Perfil | Archivos detectados | Qué activa |
|--------|---------------------|------------|
| **web-frontend** | `package.json`, `tsconfig.json` | TypeScript strict, React/Vue patterns |
| **systems** | `Cargo.toml`, `go.mod`, `pyproject.toml` | Error handling, memory safety, concurrency |
| **game-dev** | `project.godot`, `.godot/` | Determinismo, state machines, netcode |
| **mobile** | `pubspec.yaml`, `Podfile`, `build.gradle` | Lifecycle management, platform differences |
| **infrastructure** | `Dockerfile`, `.github/workflows/` | IaC, security, immutability |

## Discovery Flow

Antes de cualquier trabajo, ejecutar:

```bash
/sdd-discover
```

Esto:
1. Escanea el repositorio
2. Identifica perfiles activos
3. Muestra estado actual (constitution ✓, spec ✗, etc.)
4. Sugiere skill siguiente

## Flujo SDD Mejorado

```
discover → constitution → spec ✓ → clarify → plan ✓ → tasks ✓ → implement → validate ✓
              │               │                    │           │
              ▼               ▼                    ▼           ▼
         [perfil rules]  [verification gates]  [verification] [DoD check]
```

Los `✓` marcan approval gates where human verification is required.

## Skills Disponibles

### Core SDD
| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar proyecto y rutear | Matriz de skills aplicables |
| `/sdd-constitution` | Crear constitución del proyecto | `docs/constitution.md` |
| `/sdd-spec` | Generar especificación RF-EARS | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | Revisión QA automática | Notas en spec.md |
| `/sdd-plan` | Diseño técnico con pseudocódigo | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Descomposición en tareas | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement` | Implementación TDD por tarea | Código + tests, Tn marcada |
| `/sdd-validate` | Validación cobertura RF→Test | Tabla trazabilidad |
| `/sdd-flow` | Wizard completo automatizado | Pipeline completo |

### Perfiles por Dominio
Cada skill carga automáticamente reglas del perfil detectado:
- `profiles/web-frontend/SKILL.md`
- `profiles/systems/SKILL.md`
- `profiles/game-dev/SKILL.md`
- `profiles/mobile/SKILL.md`
- `profiles/infrastructure/SKILL.md`

## Reglas Globales Obligatorias

1. **Always discover first.** Antes de escribir código, confirmar dominio y skill a usar.
2. **ASUMPTIONS explícitas.** Toda tarea debe listar suposiciones al inicio.
3. **Nunca parchear.** Si algo está mal, refactorizar limpio nunca workaround.
4. **Verification gates antes de continuar.** Cada skill termina con checklist.
5. **Definition of Done universal.** Todo cambio cumple DoD antes de merge.

## State Management

Estado se guarda en `.sdd-state.json`:

```json
{
  "current_phase": "spec",
  "approved_phases": ["constitution"],
  "profiles_active": ["game-dev"],
  "specs_count": 1,
  "tasks_total": 8,
  "tasks_completed": 2,
  "last_checkpoint": "2026-01-15T10:30:00Z"
}
```

Comandos de control:
- `/sdd-discover resume` — Continuar desde último paso
- `/sdd-discover status` — Mostrar estado actual
- `/sdd-flow reset` — Reiniciar flujo

## Material de Referencia

Consultar antes de tomar decisiones:

| Archivo | Contenido |
|---------|-----------|
| `references/skill-template.md` | Estructura base para nuevos skills |
| `references/anti-rationalizations.md` | Excusas comunes y realidad |
| `references/verification-gates.md` | Checklists transversales |
| `references/definition-of-done.md` | Barra de calidad universal |

## Pattern de Contribución

Para agregar un nuevo skill:

1. Copiar `references/skill-template.md`
2. Añadir frontmatter obligatorio (`name`, `description`)
3. Incluir sección `ASUMPTIONS I'M MAKING:`
4. Definir `RATIONALIZATIONS` table específica
5. Agregar `VERIFICATION` checklist
6. Actualizar `skills-lock.json`

Para agregar un nuevo perfil:

1. Crear `profiles/<nombre>/SKILL.md`
2. Definir reglas específicas del dominio
3. Listar commands específicos
4. Agregar anti-patterns propios
5. Documentar integration points con core SDD

---

*Este archivo se lee automáticamente al iniciar sesión. Las reglas aquí definidas son obligatorias.*
