# Skills SDD — Spec-Driven Development

Sistema completo de skills para desarrollo guiado por especificación. Universal, tecnología-agnóstico.

## Arquitectura V2

```
┌─────────────────────────────────────────────────────────────┐
│                      Core SDD                               │
│   discover → constitution → spec → clarify → plan          │
│            → tasks → implement → validate                   │
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

## Skills Core (9)

| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar proyecto, detectar perfil | Matriz de skills aplicables |
| `/sdd-constitution` | Crear constitución del proyecto | `docs/constitution.md` |
| `/sdd-spec` | Generar especificación RF-EARS | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | Revisión QA automática | Notas en spec.md |
| `/sdd-plan` | Diseño técnico con pseudocódigo | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Descomposición en tareas | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement` | Implementación TDD por tarea | Código + tests |
| `/sdd-validate` | Validación cobertura RF→Test | Tabla trazabilidad |
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
/sdd-spec             # Especificar QUÉ construir
/sdd-clarify          # Validar calidad de spec
/sdd-plan             # Diseñar CÓMO construir
/sdd-tasks            # Descomponer en unidades
/sdd-implement T1     # Implementar tarea 1
/sdd-validate         # Verificar cobertura completa
```

---

## Reglas Globales

1. **Always discover first.** Ejecutar `/sdd-discover` antes de cualquier trabajo.
2. **ASUMPTIONS explícitas.** Cada skill lista suposiciones al inicio.
3. **Nunca parchear.** Code limpio desde el inicio, nunca workarounds temporales.
4. **Verification gates.** Checkpoints obligatorios entre fases.
5. **Definition of Done universal.** Todo cambio debe cumplir DoD antes de merge.

---

## Estado del Proyecto

El sistema guarda estado persistente en `.sdd-state.json`:

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
- `/sdd-discover resume` — Continuar desde último step
- `/sdd-discover status` — Mostrar estado actual
- `/sdd-flow reset` — Reiniciar flujo completo

---

*Versión 2.0.0 — Sistema agnóstico a tecnología con perfiles adaptativos*
