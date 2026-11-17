# Skills SDD — Spec-Driven Development

Sistema completo de skills para desarrollo guiado por especificación. Universal, tecnología-agnóstico.

## Arquitectura V2

```
┌─────────────────────────────────────────────────────────────┐
│                      Core SDD                               │
│   discover → constitution → backlog → spec → clarify       │
│            → plan → review → tasks → implement → validate   │
│            → variants                                          │
└─────────────────────────────────────────────────────────────┘
                           ↕
┌─────────────────────────────────────────────────────────────┐
│                    Perfiles Adaptativos                      │
│  web-frontend | systems | game-dev | mobile | infrastructure │
└─────────────────────────────────────────────────────────────┘
                           ↕
┌─────────────────────────────────────────────────────────────┐
│                  Material de Referencia                      │
│  skill-template | anti-rationalizations | verification-gates │
└─────────────────────────────────────────────────────────────┘
```

---

## Skills Core (11)

| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar proyecto, detectar perfil | Matriz de skills aplicables |
| `/sdd-constitution` | Crear constitución del proyecto | `docs/constitution.md` |
| `/sdd-backlog` | Backlog de historias de usuario | `specs/NNN-xxx/backlog.md` |
| `/sdd-spec` | Generar especificación RF-EARS | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | Revisión QA automática | Notas en spec.md |
| `/sdd-review` | Review de suposiciones y decisiones | `specs/NNN-xxx/review.md` |
| `/sdd-plan` | Diseño técnico con pseudocódigo | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Descomposición en tareas | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement` | Implementación TDD por tarea | Código + tests |
| `/sdd-validate` | Validación RF→Test con Constitution | Tabla trazabilidad + veredicto |
| `/sdd-variants` | Multi-variant exploration | `variants-ranking.md` |
| `/sdd-flow` | Wizard completo automatizado | Pipeline completo |

---

## Perfiles Disponibles (5)

### web-frontend
**Stack:** React, Vue, Angular, Next.js, Svelte  
**Reglas clave:** TypeScript strict, bundle size monitoring, accessibility first  
**Commands típicos:** `tsc --noEmit`, `eslint src/`, `npm test`

### systems
**Stack:** Rust, Go, Python, C#, Java  
**Reglas clave:** Error handling obligatorio, memory safety, zero-warnings policy  
**Commands típicos:** `cargo check`, `go vet`, `mypy`, `dotnet build`

### game-dev
**Stack:** Godot, Unity, Unreal  
**Reglas clave:** Determinismo estricto, state machines, network sync, object pooling  
**Commands típicos:** `godot --headless`, Unity batch mode tests

### mobile
**Stack:** Flutter, React Native, Swift, Kotlin  
**Reglas clave:** Lifecycle management, memory leaks prevention, platform parity  
**Commands típicos:** `flutter analyze`, Xcode/test execution

### infrastructure
**Stack:** Docker, Kubernetes, Terraform, CI/CD  
**Reglas clave:** IaC only, security-first, immutability, rollback plans  
**Commands típicos:** `docker build`, `terraform plan`, pipeline validation

---

## Referencias Transversales

| Archivo | Propósito |
|---------|-----------|
| `references/skill-template.md` | Plantilla maestra para crear nuevos skills |
| `references/anti-rationalizations.md` | Tablas de excusas comunes vs realidad |
| `references/verification-gates.md` | Checklists de verificación por fase |
| `references/definition-of-done.md` | Barra de calidad universal |

---

## Flujo Mejorado

```bash
# Paso 1: Descubrir perfil y estado
/sdd-discover

# Paso 2: Iniciar flujo completo (o individual)
/sdd-flow "descripción de la funcionalidad"

# O paso a paso:
/sdd-constitution     # Crear principios innegociables
/sdd-backlog          # Destilar idea en historias de usuario verticales
/sdd-spec             # Especificar QUÉ construir
/sdd-clarify          # Validar calidad de spec
/sdd-plan             # Diseñar CÓMO construir
/sdd-review           # Revisar suposiciones y alternativas
/sdd-tasks            # Descomponer en tareas
/sdd-implement T1     # Implementar tarea 1
/sdd-validate         # Verificar cobertura completa
/sdd-variants          # Explorar alternativas y ganar la mejor
```

---

## Reglas Globales

1. **Always discover first.** Ejecutar `/sdd-discover` antes de cualquier trabajo.
2. **ASSUMPTIONS explícitas.** Cada skill lista suposiciones al inicio.
3. **Nunca parchear.** Code limpio desde el inicio, nunca workarounds temporales.
4. **Verification gates.** Checkpoints obligatorios entre fases con aprobación humana.
5. **Definition of Done universal.** Todo cambio debe cumplir DoD antes de merge.

---

## Estado del Proyecto

El sistema guarda estado persistente en `.sdd-state.json`:

```json
{
  "version": "2.1.0",
  "current_phase": "discovered",
  "approved_phases": [],
  "profiles_active": [],
  "specs_count": 0,
  "tasks_total": 0,
  "tasks_completed": 0,
  "last_checkpoint": null,
  "flow": {
    "phases": ["setup", "constitution", "backlog", "spec", "clarify", "plan", "review", "tasks", "implement", "validate", "variants"],
    "current_phase_index": 0,
    "approved_gates": []
  }
}
```

Comandos de control:
- `/sdd-discover resume` — Continuar desde último step
- `/sdd-discover status` — Mostrar estado actual
- `/sdd-flow reset` — Reiniciar flujo completo

---

## Cambios recientes (v2.1.0)

- **Skills eliminadas:** `sdd-pair`, `sdd-story` (funcionalidad integrada en otros skills)
- **sdd-review:** Ahora es fase obligatoria entre plan y tasks
- **sdd-variants:** Ahora es fase obligatoria con gate de aprobación
- **sdd-validate:** Fail-closed, requiere evidencia de código + Constitution compliance
- **sdd-flow:** Integrado sdd-variants como Phase 10 con gate obligatorio
- **Contexto compartido:** Cada skill incluye bloque de contexto de consumo/producción
- **Estandarización frontmatter:** todas las skills tienen version 2.1.0 y bloque de contexto

---

## Skills Eliminadas (V2.1)

Las siguientes skills han sido **eliminadas**:
- **`sdd-pair`** — Su funcionalidad está cubierta por `sdd-implement` con verificación humana por tarea
- **`sdd-story`** — Su funcionalidad está integrada en `sdd-backlog` y `sdd-spec`

---

*Versión 2.1.0 — Sistema agnóstico a tecnología con perfiles adaptativos*