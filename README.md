# SDD Skills — Spec-Driven Development

[![Skills](https://img.shields.io/badge/skills-11%20skills-blue)](./docs/SKILLS.md)
[![Profiles](https://img.shields.io/badge/profiles-5-orange)](./profiles/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

Sistema completo de **skills OpenCode** para desarrollo guiado por especificación. Tecnología-agnóstico, adaptable a cualquier stack.

## 🎯 ¿Qué es SDD?

Especification-Driven Development: procesos estructurados que fuerzan claridad antes de escribir código. Cada skill es autocontenida con su propia documentación, reglas de dominio y verificación.

## 🔄 Nuevo Flujo (V2)

```
discover → constitution → backlog → spec → clarify → plan → review → tasks → implement → validate → variants
    ↓           ↓          ↓        ↓        ↓         ↓          ↓            ↓
[setup    [principios [backlog [RF-EARS [QA      [arquitectura [suposiciones [TDD       [pair      [TDD       [RF→Test
 detected]   inneg.]   historias[refinar] mapping] loop]    decisiones]     review]     [tareas]   [implement] enforced]   coverage]
           ↓          ↓         ↓       ↓     ↓      ↓        ↓        ↓        ↓          ↓          ↓            ↓
        [human   [human   [human  [human   [human   [human   [human   [human   [human    [human      [human      [human
         approval] approval] approval] approval] approval] approval] approval] approval] approval] approval] approval]

Los `↓` indican **approval gates** donde se requiere confirmación humana antes de continuar.

## 📦 Skills Disponibles

### Core SDD
| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar proyecto, detectar perfil | Matriz de skills |
| `/sdd-constitution` | Principios innegociables | `docs/constitution.md` |
| `/sdd-backlog` | Backlog de historias de usuario | `specs/NNN-xxx/backlog.md` |
| `/sdd-spec` | Especificación RF-EARS | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | QA automático | Notas en spec.md |
| `/sdd-review` | Review de suposiciones y decisiones | `specs/NNN-xxx/review.md` |
| `/sdd-plan` | Diseño técnico | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Tareas verificables | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement` | Implementación TDD | Código + tests |
| `/sdd-validate` | Validación RF→Test | Tabla trazabilidad |
| `/sdd-variants` | Multi-variant exploration | `variants-ranking.md` |
| `/sdd-flow` | Wizard completo | Pipeline automático |

### Perfiles por Dominio
| Perfil | Stack | Reglas clave |
|--------|-------|--------------|
| `web-frontend` | React, Vue, Next.js | TypeScript strict, a11y, bundle size |
| `systems` | Rust, Go, Python, C# | Error handling, memory safety, zero-warnings |
| `game-dev` | Godot, Unity | Determinismo, state machines, netcode sync |
| `mobile` | Flutter, RN, Swift | Lifecycle, memory leaks, platform parity |
| `infrastructure` | Docker, K8s, Terraform | IaC, security-first, immutability |

## 🎭 Historias de Usuario y Vertical Slicing

Integramos el enfoque de **hola-ai** para destilar ideas antes de especificar:

| Fase | Skill | Qué hace |
|------|-------|----------|
| Backlog | `/sdd-backlog` | Idea vaga → historias de usuario verticales (1 línea cada una) |

**Principios:**
- **Vertical slicing:** historias cruzan todas las capas
- **No inventar:** la información faltante se pregunta, no se rellena
- **Lo más simple que funciona:** ninguna abstracción "para el futuro"
- **Checkpoints explícitos:** cada fase espera tu aprobación

## 🚀 Quick Start

```bash
# Descubrir perfil del proyecto
/sdd-discover

# Crear constitución (principios innegociables)
/sdd-constitution

# Destilar idea en historias de usuario
/sdd-backlog "idea de funcionalidad"

# Especificar en RF-EARS
/sdd-spec

# Validar calidad de spec
/sdd-clarify

# Diseñar plan técnico
/sdd-plan

# Revisar suposiciones (opcional)
/sdd-review

# Descomponer en tareas
/sdd-tasks

# Implementar tarea con TDD
/sdd-implement T1

# Validar cobertura completa
/sdd-validate

# Explorar variantes de implementación
/sdd-variants
```

## 📥 Instalación

### Desde GitHub (recomendado)
```bash
npx skills add Pevalcar/sdd-skills
```

### Localmente
```bash
cp -r skills/ .opencode/skills/
cp -r profiles/ .opencode/profiles/
cp -r references/ .opencode/references/
```

### Verificar
```bash
npx skills ls | grep sdd
```

## 🏗️ Arquitectura

```
sdd-skills/
├── skills/                    # 13 skills principales
│   ├── sdd-discover/       # Meta-skill router
│   ├── sdd-constitution/
│   ├── sdd-backlog/
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

## 🔑 Principios Clave

1. **Descubrimiento primero** — `/sdd-discover` antes de todo
2. **Reglas por perfil** — Cada tecnología tiene sus constraints
3. **Historias de usuario y vertical slicing** — `(sdd-backlog)` crea historias pequeñas que cruzan todas las capas
4. **Anti-racionalizaciones** — Prevenir atajos peligrosos
5. **Verification gates** — Checkpoints obligatorios entre fases
6. **Definition of Done** — Barra de calidad universal

## 🛡️ Anti-Patterns Protegidos

| Excusa | Realidad | Prevención |
|--------|----------|------------|
| *"Es pequeño, no necesito tests"* | Regresiones silenciosas | Tests obligatorios para lógica crítica |
| *"Ignoro warnings, lo arreglo después"* | Bugs latentes | Zero-warnings policy |
| *"Parche temporal está bien"* | Deuda técnica acumulada | Código limpio desde el inicio |
| *"Ya lo probé manual"* | No escala, no persiste | Automatización requerida |

## 🎓 Skills Eliminadas

Las siguientes skills han sido **eliminadas**:
- **`sdd-pair`** — Su funcionalidad está cubierta por `sdd-implement` con verificación humana por tarea
- **`sdd-story`** — Su funcionalidad está integrada en `sdd-backlog` y `sdd-spec`
- **`ponytail`** — Skill externa opcional, no forma parte del sistema SDD

## 🤝 Contribuir

Ver [CONTRIBUTING.md](./CONTRIBUTING.md) para guías completas.

Quick start:
```bash
# Crear nueva skill
cp -r skills/sdd-template/ skills/sdd-nuevo/
# Editar SKILL.md siguiendo references/skill-template.md
# Actualizar skills-lock.json
```

## 📚 Referencias

- [Arquitectura del Sistema](./docs/architecture.md)
- [INVEST Patterns](./docs/INVEST-patterns.md)
- [Definición de Done](./references/definition-of-done.md)
- [Checklist Verificación](./references/verification-gates.md)

## 📄 Licencia

MIT License - Ver [LICENSE](./LICENSE)