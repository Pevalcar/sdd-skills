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
1. Verifica si necesitas setup (AGENT.md, constitution)
2. Escanea el repositorio
3. Identifica perfiles activos
4. Muestra estado actual (constitution ✓, spec ✗, etc.)
5. Sugiere skill inicial correcto

## El Flow SDD

```
Setup → Spec → Clarify → Plan → Tasks → Implement → Validate → Variants
   ↓      ↓        ↓       ↓       ↓          ↓          ↓        ↓
sdd-     sdd-spec  sdd-    sdd-plan sdd-tasks sdd-      sdd-     sdd-variants
setup  clarify   clarify        (loop)             implement  validate (optional)
```

Los `✓` marcan approval gates donde human verification es requerida.

## Skills Disponibles

### Core SDD
| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar proyecto y rutear | Matriz de skills aplicables |
| `/sdd-setup` | Crear AGENT.md y constitution | AGENT.md + docs/constitution.md |
| `/sdd-constitution` | Crear constitutional | `docs/constitution.md` |
| `/sdd-spec` | Generar especificación RF-EARS | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | Revisión QA automática | Notas en spec.md |
| `/sdd-plan` | Diseño técnico con pseudocódigo | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Descomposición en tareas | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement` | Implementación TDD por tarea | Código + tests, Tn marcada |
| `/sdd-validate` | Validación cobertura RF→Test | Tabla trazabilidad |
| `/sdd-variants` | Multi-variant exploration | `variants-ranking.md` |

### Perfiles por Dominio
Cada skill carga automáticamente reglas del perfil detectado:
- `profiles/web-frontend/SKILL.md`
- `profiles/systems/SKILL.md`
- `profiles/game-dev/SKILL.md`
- `profiles/mobile/SKILL.md`
- `profiles/infrastructure/SKILL.md`

## Reglas Globales Obligatorias

1. **Startup check.** Antes de cualquier trabajo, verificar si necesitas setup → `/sdd-setup`
2. **Always discover first.** Antes de escribir código, confirmar dominio y skill a usar.
3. **ASUMPTIONS explícitas.** Toda tarea debe listar suposiciones al inicio.
4. **Clarify loop.** Keep asking until spec is crystal clear.
5. **Nunca parchear.** Si algo está mal, refactorizar limpio nunca workaround.
6. **Verification gates antes de continuar.** Cada skill termina con checklist.
7. **Definition of Done universal.** Todo cambio cumple DoD antes de merge.

## State Management

Estado se guarda en `.sdd-state.json`:

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