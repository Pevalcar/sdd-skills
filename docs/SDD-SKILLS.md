# Skills SDD V2 — Spec-Driven Development

Sistema completo de skills para desarrollo guiado por especificación. **Tecnología-agnóstico con perfiles adaptativos.**

## 🚀 Novedades V2

- **sdd-discover**: Meta-skill que detecta perfil tecnológico automáticamente
- **sdd-review**: Review de suposiciones y decisiones con doubt-driven development
- **sdd-variants**: Exploración y ranking de variantes de implementación
- **Perfiles adaptativos**: Reglas específicas para web, systems, game-dev, mobile, infrastructure
- **ASUMPTIONS explícitas**: Cada skill lista suposiciones al inicio
- **Rationalizations tables**: Excusas comunes vs realidad técnica
- **Verification gates**: Checkpoints obligatorios por fase y perfil
- **Definition of Done**: Barra de calidad universal

## 📦 Skills Core (10)

| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar, detectar perfil | Matriz de skills aplicables |
| `/sdd-constitution` | Crear constitución | `docs/constitution.md` |
| `/sdd-spec` | Generar especificación | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | QA automático | Notas en spec.md |
| `/sdd-review` | Review de suposiciones y decisiones | `specs/NNN-xxx/review.md` |
| `/sdd-plan` | Diseño técnico | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Tareas verificables | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement Tn` | TDD por tarea | Código + tests, marca Tn completada |
| `/sdd-validate` | RF→Test coverage + Constitution | Tabla trazabilidad + veredicto |
| `/sdd-variants` | Multi-variant exploration | `variants-ranking.md` |
| `/sdd-flow "idea"` | Wizard completo | Pipeline automático con gates |

## 🎯 Perfiles Adaptativos (5)

| Perfil | Stack | Reglas clave |
|--------|-------|--------------|
| **web-frontend** | React, Vue, TypeScript | Strict mode, a11y, bundle size |
| **systems** | Rust, Go, Python, C# | Error handling, zero-warnings |
| **game-dev** | Godot, Unity | Determinismo, netcode, state machines |
| **mobile** | Flutter, Swift, Kotlin | Lifecycle, memory leaks, parity |
| **infrastructure** | Docker, K8s, Terraform | IaC-only, security-first |

## 🔄 Flujo SDD V2

```
discover → constitution → spec → clarify → plan → review → tasks → implement → validate → variants
    ↓           ↓          ↓          ↓         ↓         ↓         ↓          ↓            ↓
[setup]    [principios] [RF-EARS]  [QA]    [tech]   [decisiones] [TDD]     [coverage]   [ranking]
           ↓          ↓          ↓         ↓         ↓          ↓          ↓            ↓
        [human]    [human]    [human]   [human]   [human]    [human]    [human]    [human]
       approval]  approval]  approval]  approval]  approval]  approval]  approval]  approval]
```

Los `↓` indican **verification gates** donde se requiere aprobación humana.

## 📁 Estructura del Proyecto

```
.sdd-skills/
├── skills/                    # 10 skills principales
│   ├── sdd-discover/       # Meta-skill router
│   ├── sdd-constitution/
│   ├── sdd-spec/
│   ├── sdd-clarify/
│   ├── sdd-review/
│   ├── sdd-plan/
│   ├── sdd-tasks/
│   ├── sdd-implement/
│   ├── sdd-validate/
│   ├── sdd-variants/
│   └── sdd-flow/
├── profiles/                 # 5 perfiles adaptativos
│   ├── web-frontend/
│   ├── systems/
│   ├── game-dev/
│   ├── mobile/
│   └── infrastructure/
├── references/               # Material transversal
│   ├── skill-template.md
│   ├── anti-rationalizations.md
│   ├── verification-gates.md
│   └── definition-of-done.md
├── docs/                     # Documentación detallada
├── examples/                 # Casos de uso
└── .sdd-state.json          # Estado persistente
```

## 📋 Plantillas Incluidas

- `spec-template.md` - Formato de especificación con RF-EARS
- `plan-template.md` - Formato de plan con pseudocódigo
- `tasks-template.md` - Formato de tareas con checkboxes
- `clarify-template.md` - Formato de revisión QA
- `TASKS.md` (en specs/template/) - Template para tasks.md

## ⚠️ Reglas SDD V2 Obligatorias

1. **Especificación antes que código** - Ningún RF sin spec aprobada
2. **TDD obligatorio** - Test primero, código mínimo
3. **Una tarea a la vez** - Pausa después de cada implementación
4. **Verificables** - RF son verificables, no adjectivos
5. **FUERA de alcance** - Siempre definir lo que NO se implementa
6. **Antes de todo cambio**: `/sdd-discover` para detectar perfil
7. **Cada skill** debe tener ASUMPTIONS, Rationalizations, Verification

## 🚀 Ejemplo de uso

```bash
# Paso 1: Descubrir perfil
/sdd-discover

# Wizard completo (detecta automáticamente el perfil)
/sdd-flow "funcionalidad: login Dofus con OAuth"

# Output ejemplo:
→ Perfil detectado: game-dev
→ Constitution verificada
→ Spec generada (RF-1 a RF-4)
→ QA automático pasado
→ Plan técnico creado
→ Review de decisiones completado
→ 6 tareas verificables generadas
→ T1 implementada con TDD
→ Validación RF→Test (5/6 completado)
→ Variants generados y shortlist ranqueada
```

## 📚 Referencias Rápidas

- [Arquitectura V2](./architecture.md)
- [Skills Catalog](./SKILLS.md)
- [Quick Start](../examples/quick-start.md)
- [Full Flow Example](../examples/full-flow-example.md)
- [Skill Template](../references/skill-template.md)
- [Definition of Done](../references/definition-of-done.md)

## 🏷️ Tags por perfil

Cuando el sistema detecta el perfil, carga automáticamente:

- **web-frontend**: TypeScript strict, ESLint, Testing Library
- **systems**: Zero-warnings, Memory safety, Error handling
- **game-dev**: Determinismo estricto, State machines, Netcode
- **mobile**: Lifecycle explicit, Memory leak prevention
- **infrastructure**: IaC only, Security-first, Rollback plans

---

*Versión 2.1.0 — Sistema agnóstico a tecnología con perfiles adaptativos y variants integrados*