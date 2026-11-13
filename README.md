# SDD Skills — Spec-Driven Development

[![Skills](https://img.shields.io/badge/skills-9%20skills-blue)](./docs/SKILLS.md)
[![Profiles](https://img.shields.io/badge/profiles-5-orange)](./profiles/)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

Sistema completo de **skills OpenCode** para desarrollo guiado por especificación. Tecnología-agnóstico, adaptable a cualquier stack.

## 🎯 ¿Qué es SDD?

Especification-Driven Development: procesos estructurados que fuerzan claridad antes de escribir código. Cada skill es autocontenida con su propia documentación, reglas de dominio y verificación.

## 🔄 Nuevo Flujo (V2)

```
discover → constitution → spec ✓ → clarify → plan ✓ → tasks ✓ → implement → validate ✓
   │              │          │                    │           │            │
   ▼              ▼          ▼                    ▼           ▼            ▼
 [perfil      [principios  [verification    [verificable  [TDD         [cobertura
  detectado]   inneg.]     gates]           checks]      enforced]   RF→Test]
```

Los `✓` indican approval gates where se requiere confirmación humana.

## 📦 Skills Disponibles

### Core SDD
| Skill | Uso | Output |
|-------|-----|--------|
| `/sdd-discover` | Analizar proyecto, detectar perfil | Matriz de skills |
| `/sdd-constitution` | Principios innegociables | `docs/constitution.md` |
| `/sdd-spec` | Especificación RF-EARS | `specs/NNN-xxx/spec.md` |
| `/sdd-clarify` | QA automático | Notas en spec.md |
| `/sdd-plan` | Diseño técnico | `specs/NNN-xxx/plan.md` |
| `/sdd-tasks` | Tareas verificables | `specs/NNN-xxx/tasks.md` |
| `/sdd-implement` | Implementación TDD | Código + tests |
| `/sdd-validate` | Validación RF→Test | Tabla trazabilidad |
| `/sdd-flow` | Wizard completo | Pipeline automático |

### Perfiles por Dominio
| Perfil | Stack | Reglas clave |
|--------|-------|--------------|
| `web-frontend` | React, Vue, Next.js | TypeScript strict, a11y, bundle size |
| `systems` | Rust, Go, Python, C# | Error handling, memory safety, zero-warnings |
| `game-dev` | Godot, Unity | Determinismo, state machines, netcode sync |
| `mobile` | Flutter, RN, Swift | Lifecycle, memory leaks, platform parity |
| `infrastructure` | Docker, K8s, Terraform | IaC, security-first, immutability |

## 🚀 Quick Start

```bash
# Descubrir perfil del proyecto
/sdd-discover

# Wizard completo
/sdd-flow "funcionalidad: login Dofus con OAuth"
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
├── skills/                    # 9 skills principales
│   ├── sdd-discover/       # NUEVO: Meta-skill router
│   ├── sdd-constitution/
│   ├── sdd-spec/
│   ├── sdd-clarify/
│   ├── sdd-plan/
│   ├── sdd-tasks/
│   ├── sdd-implement/
│   ├── sdd-validate/
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
3. **Anti-racionalizaciones** — Prevenir atajos peligrosos
4. **Verification gates** — Checkpoints obligatorios entre fases
5. **Definition of Done** — Barra de calidad universal

## 🛡️ Anti-Patterns Protegidos

| Excusa | Realidad | Prevención |
|--------|----------|------------|
| *"Es pequeño, no necesito tests"* | Regresiones silenciosas | Tests obligatorios para lógica crítica |
| *"Ignoro warnings, lo arreglo después"* | Bugs latentes | Zero-warnings policy |
| *"Parche temporal está bien"* | Deuda técnica acumulada | Código limpio desde el inicio |
| *"Ya lo probé manual"* | No escala, no persiste | Automatización requerida |

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
