# SDD Skills — Spec-Driven Development

[![Skills](https://img.shields.io/badge/skills-8%20skills-blue)](./docs/Skills.md)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

Sistema completo de **skills OpenCode** para desarrollo guiado por especificación, inspirado en patrones de desarrollo ágil y specification-driven development.

## 🎯 ¿Qué son las Skills SDD?

Skills SDD son módulos reutilizables que automatizan el proceso de creación de especificaciones, planes de desarrollo y validación de requisitos. Cada skill es autocontenida con su propia documentación y plantillas.

## 🚀 Hola AI Enhanced

Este sistema incorpora patrones de la metodología Hola AI, incluyendo:
- **Historias de usuario INVEST** para requisitos bien definidos
- **Critérios de aceptación en Gherkin** para pruebas automatizadas  
- **Plantillas estructuradas** para consistencia en todos los artefactos

## 📦 Skills Disponibles

| Skill | Uso | Output |
|-------|-----|--------|
| `sdd-constitution` | Crear constitución del proyecto | `docs/constitution.md` |
| `sdd-spec` | Generar especificación con RF-EARS | `specs/001-xxx/spec.md` |
| `sdd-clarify` | Revisión QA de especificaciones | Notas agregadas a spec.md |
| `sdd-plan` | Generar plan técnico con pseudocódigo | `specs/001-xxx/plan.md` |
| `sdd-tasks` | Generar tareas verificables con checkboxes | `specs/001-xxx/tasks.md` |
| `sdd-implement` | Implementar tarea (TDD) | Código + tests, marca Tn completada |
| `sdd-validate` | Validar RF por RF con veredicto | Tabla cobertura RF→Test |
| `sdd-flow` | Wizard completo interactivo | Genera todo el flujo automáticamente |

## 🔄 Flujo SDD

```
constitution → spec → clarify → plan → tasks → implement → validate
```

## 📥 Instalación

### Método 1: Desde GitHub (recomendado)

```bash
# Instalar desde el repositorio
npx skills add Pevalcar/sdd-skills
```

### Método 2: Localmente

```bash
# Copiar las skills al proyecto OpenCode
cp -r skills/sdd-* .opencode/skills/
```

### Verificar instalación

```bash
npx skills ls | grep sdd
```

## 💡 Ejemplos de Uso

### Uso rápido con el wizard completo

```bash
/sdd-flow "login Dofus con OAuth"
```

El wizard interactivo:
1. Pregunta por la constitución del proyecto
2. Genera spec.md
3. Aplica QA automático
4. Crea plan técnico
5. Genera tareas verificables
6. Implementa T1 con TDD
7. Valida RF por RF

### Uso individual por skill

```bash
# Generar constitución
/sdd-constitution

# Generar especificación
/sdd-spec

# Revisión QA
/sdd-clarify

# Plan técnico
/sdd-plan

# Tareas
/sdd-tasks

# Implementar tarea específica
/sdd-implement T1
/sdd-implement T2

# Validar
/sdd-validate
```

## 📁 Estructura del Repositorio

```
sdd-skills/
├── skills/                      # Skills principales (sdd-*)
│   ├── sdd-constitution/
│   ├── sdd-spec/
│   ├── sdd-clarify/
│   ├── sdd-plan/
│   ├── sdd-tasks/
│   ├── sdd-implement/
│   ├── sdd-validate/
│   └── sdd-flow/
├── examples/                    # Ejemplos de uso
├── docs/                        # Documentación detallada
├── .gitignore
├── README.md
├── CONTRIBUTING.md
└── skills-lock.json
```

## 📖 Documentación

- [Guía de Contribución](./CONTRIBUTING.md)
- [Arquitectura del Sistema](./docs/architecture.md)
- [Formato de Historias de Usuario](./docs/INVEST-patterns.md)
- [Ejemplos de Uso](./examples/)

## 🔧 Plantillas Incluidas

- `spec-template.md` - Formato de especificación con RF-EARS
- `plan-template.md` - Formato de plan con pseudocódigo
- `tasks-template.md` - Formato de tareas con checkboxes
- `clarify-template.md` - Formato de revisión QA

## 🏗️ Reglas SDD

1. **Especificación antes que código** - Ningún RF sin spec
2. **TDD obligatorio** - Test primero, código mínimo
3. **Una tarea a la vez** - Pausa después de cada implementación
4. **Verificables** - RF son verificables, no adjectivos
5. **FUERA de alcance** - Siempre definir lo que NO se implementa

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Consulta [CONTRIBUTING.md](./CONTRIBUTING.md) para más detalles.

## 📚 Referencias

- [Hola AI](https://github.com/mouredev/hola-ai) - Conceptos de agente AI
- [hello-sdd](https://github.com/mouredev/hello-sdd) - Referencia original de SDD
- [OpenCode Skills](https://github.com/opencode-ai/opencode) - Plataforma de skills

## 📄 Licencia

MIT License - Ver [LICENSE](./LICENSE) para más información.