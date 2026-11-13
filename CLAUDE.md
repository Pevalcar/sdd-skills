# CLAUDE.md — Configuración para Claude Code

Este archivo define el comportamiento de los agentes AI para trabajar con el sistema SDD V2.

## 🎯 Sistema SDD V2 — Resumen Ejecutivo

**Versión:** 2.0.0 — Tecnología-agnóstico con perfiles adaptativos

### Core Principles

1. **Siempre descubrir primero** — `/sdd-discover` antes de cualquier trabajo
2. **Suposiciones explícitas** — Cada skill lista ASUMPTIONS al inicio
3. **Nunca parchear** — Código limpio desde el inicio, sin workarounds
4. **Verification gates** — Checkpoints obligatorios entre fases
5. **Definition of Done universal** — Todo cambio cumple DoD antes de merge

### Skills Core (9)

| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar, detectar perfil | Matriz de skills aplicables |
| `/sdd-constitution` | Crear constitución | `docs/constitution.md` |
| `/sdd-spec` | Generar especificación | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | QA automático | Notas en spec.md |
| `/sdd-plan` | Diseño técnico | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Tareas verificables | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement` | TDD por tarea | Código + tests |
| `/sdd-validate` | RF→Test coverage | Tabla trazabilidad |
| `/sdd-flow` | Wizard completo | Pipeline automático |

### Perfiles Adaptativos (5)

- **web-frontend**: React, Vue, TypeScript, Vite
- **systems**: Rust, Go, Python, C#
- **game-dev**: Godot, Unity, determinismo
- **mobile**: Flutter, Swift, Kotlin
- **infrastructure**: Docker, K8s, Terraform

### Referencias Transversales

- `references/skill-template.md` — Plantilla maestra
- `references/anti-rationalizations.md` — Excusas vs realidad
- `references/verification-gates.md` — Checklists
- `references/definition-of-done.md` — Barra de calidad

### Estado Persistente

`.sdd-state.json` — Lleva tracking del flujo actual

### Flujo Recomendado

```bash
/sdd-discover          # Paso 1: Detectar perfil
/sdd-flow "funcionalidad"  # Wizard completo
# O paso a paso
/sdd-constitution → /sdd-spec → /sdd-plan → /sdd-tasks → /sdd-implement → /sdd-validate
```

### Reglas V2 Obligatorias

1. **Frontmatter requerido** en todos los SKILL.md: name, description, disable-model-invocation
2. **Sección ASUMPTIONS** con preguntas verificables
3. **When to Use/When NOT to Use** claramente separados
4. **Rationalizations table** adaptada al dominio
5. **Verification checklist** al final de cada skill
6. **Version bump a 2.0.0** en skills-lock.json

### Quick Commands

```bash
# Ver estado actual
npx opencode /sdd-discover status

# Iniciar flujo
npx opencode /sdd-discover

# Wizard completo
npx opencode /sdd-flow "mi funcionalidad"
```

### Documentación

- [Arquitectura V2](./docs/architecture.md)
- [Skills Catalog](./docs/SKILLS.md)
- [Quick Start](./examples/quick-start.md)

---

*Este archivo se lee automáticamente al iniciar sesión. Las reglas aquí definidas son obligatorias.*