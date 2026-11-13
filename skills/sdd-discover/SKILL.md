---
name: sdd-discover
description: "Meta-skill que analiza el proyecto y rutea al skill apropiado según el dominio detectado y estado del flujo SDD."
disable-model-invocation: true
---

# Descubridor SDD — Enrutamiento cognitivo

Analiza el repositorio para detectar perfil tecnológico, estado del flujo y rutea al skill correcto.

## 🛡️ ASUMPTIONS I'M MAKING:

1. El proyecto tiene un directorio de trabajo actual (`pwd`)
2. Hay archivos de configuración que indican el stack (package.json, Cargo.toml, etc.)
3. El usuario necesita determinar qué skill usar primero
4. El estado del flujo SDD se guarda en `.sdd-state.json`
→ Correct me now or I'll proceed.

## Lifecycle Sequence

For a complete SDD workflow, the typical skill sequence is:

```
1.  interview-me                → Extract what the user actually wants
2.  idea-refine                 → Refine vague ideas  
3.  spec-driven-development     → Define what we're building
4.  planning-and-task-breakdown → Break into verifiable chunks
5.  context-engineering         → Load the right context
6.  source-driven-development   → Verify against official docs
7.  incremental-implementation  → Build slice by slice
8.  observability-and-instrumentation → Instrument as you build
9.  doubt-driven-development    → Cross-examine non-trivial decisions in-flight
10. test-driven-development     → Prove each slice works
11. code-review-and-quality     → Review before merge
12. code-simplification         → Reduce unnecessary complexity
13. git-workflow-and-versioning → Clean commit history
14. documentation-and-adrs      → Document decisions
15. shipping-and-launch         → Deploy safely
```

Not every task needs every skill. A bug fix might only need:
`debugging-and-error-recovery` → `test-driven-development` → `code-review-and-quality`

## Skill Router Table

| Fase | When to Use | Skill to Invoke |
|------|-------------|-----------------|
| **Define** | Don't know what you want | `interview-me` |
| **Define** | Have a rough concept | `idea-refine` |
| **Define** | New project/feature/change | `spec-driven-development` |
| **Define** | No quality bar written | `constraint-driven-development` |
| **Plan** | Have a spec, need tasks | `planning-and-task-breakdown` |
| **Build** | Need better context | `context-engineering` |
| **Build** | Need doc-verified code | `source-driven-development` |
| **Build** | Implementing code | `incremental-implementation` |
| **Build** | UI work | `frontend-ui-engineering` |
| **Build** | API work | `api-and-interface-design` |
| **Build** | Stakes high / unfamiliar | `doubt-driven-development` |
| **Build** | Need tests | `test-driven-development` |
| **Build** | Browser-based | `browser-testing-with-devtools` |
| **Verify** | Something broke | `debugging-and-error-recovery` |
| **Review** | Reviewing code | `code-review-and-quality` |
| **Review** | Too complex | `code-simplification` |
| **Review** | Security concerns | `security-and-hardening` |
| **Review** | Performance concerns | `performance-optimization` |
| **Ship** | Committing/version | `git-workflow-and-versioning` |
| **Ship** | CI/CD pipeline | `ci-cd-and-automation` |
| **Ship** | Deprecating/migrating | `deprecation-and-migration` |
| **Ship** | Writing docs | `documentation-and-adrs` |
| **Ship** | Adding logs/metrics | `observability-and-instrumentation` |
| **Ship** | Deploying/launching | `shipping-and-launch` |

## Pasos

1. **Escanea el repositorio.** Busca archivos de configuración para identificar el perfil:
   - `package.json`, `tsconfig.json` → Web/Fullstack
   - `Cargo.toml`, `go.mod`, `pyproject.toml` → Systems
   - `project.godot`, `.godot/` → Game Dev
   - `pubspec.yaml`, `Podfile`, `build.gradle` → Mobile
   - `Dockerfile`, `docker-compose.yml` → Infrastructure

2. **Determina perfiles activos.** Un proyecto puede tener múltiples perfiles (ej. Godot + Python backend).

3. **Carga reglas del perfil.** Lee los archivos en `profiles/<nombre>/SKILL.md` correspondientes.

4. **Rutea al skill inicial.** Sugiere el primer skill basado en el estado del proyecto:
   - No existe `constitution.md` → `/sdd-constitution`
   - Existe constitution pero no spec → `/sdd-spec`
   - Ya hay spec pero falta plan → `/sdd-plan`
   - Ya hay plan pero faltan tareas → `/sdd-tasks`
   - Ya hay tasks pero faltan implementar → `/sdd-implement`
   - Terminada implementación → `/sdd-validate`

5. **Resume flujo existente.** Si existe `.sdd-state.json`, recuperar última fase y continuar desde ahí.

## Matriz de Perfiles

| Perfil | Archivos detectados | Skills adicionales | Validación específica |
|--------|---------------------|-------------------|----------------------|
| **web-frontend** | package.json, tsconfig.json | TypeScript patterns, SSR rules | type-check, jest tests |
| **systems** | Cargo.toml, go.mod, pyproject.toml | Concurrency rules, memory safety | cargo check, go vet, mypy |
| **game-dev** | project.godot, .godot/ | Determinismo, physics, render loop | headless tests, frame timing |
| **mobile** | pubspec.yaml, Podfile, build.gradle | Lifecycle management | native build, unit tests |
| **infrastructure** | Dockerfile, docker-compose.yml | Deploy security, IaC patterns | container scan, fmt validation |

## Quick Reference

| Phase | Skill | One-Line Summary |
|-------|-------|-----------------|
| Define | interview-me | Surface what the user actually wants before any plan, spec, or code exists |
| Define | idea-refine | Refine ideas through structured divergent and convergent thinking |
| Define | spec-driven-development | Requirements and acceptance criteria before code |
| Plan | planning-and-task-breakdown | Decompose into small, verifiable tasks |
| Build | incremental-implementation | Thin vertical slices, test each before expanding |
| Build | source-driven-development | Verify against official docs before implementing |
| Build | doubt-driven-development | Adversarial fresh-context review of every non-trivial decision |
| Build | context-engineering | Right context at the right time |
| Build | frontend-ui-engineering | Production-quality UI with accessibility |
| Build | api-and-interface-design | Stable interfaces with clear contracts |
| Verify | test-driven-development | Failing test first, then make it pass |
| Verify | browser-testing-with-devtools | Chrome DevTools MCP for runtime verification |
| Verify | debugging-and-error-recovery | Reproduce → localize → fix → guard |
| Review | code-review-and-quality | Five-axis review with quality gates |
| Review | code-simplification | Preserve behavior while reducing unnecessary complexity |
| Review | security-and-hardening | OWASP prevention, input validation, least privilege |
| Review | performance-optimization | Measure first, optimize only what matters |
| Ship | git-workflow-and-versioning | Atomic commits, clean history |
| Ship | ci-cd-and-automation | Automated quality gates on every change |
| Ship | deprecation-and-migration | Remove old systems and migrate users safely |
| Ship | documentation-and-adrs | Document the why, not just the what |
| Ship | observability-and-instrumentation | Structured logs, RED metrics, traces, symptom-based alerts |
| Ship | shipping-and-launch | Pre-launch checklist, monitoring, rollback plan |

## Output Inicial

Muestra al usuario:

```
🔍 Perfil detectado: [web-frontend]
📁 Stack: Node.js 20, React 18, TypeScript

📋 Estado actual del proyecto:
  ✓ constitution.md existe
  ✗ spec.md no existe
  ✗ plan.md no existe
  ✗ tasks.md no existe
  ✗ Tests no ejecutados

💡 Skill recomendado: /sdd-spec
   Razón: Tienes constitución pero necesitas especificar primero.

¿Continuar? [s/n]
```

## Control del Flujo

Comandos disponibles:

| Comando | Acción |
|---------|--------|
| `/sdd-discover` | Ejecutar análisis completo |
| `/sdd-discover resume` | Continuar desde último paso |
| `/sdd-discover status` | Mostrar estado actual |
| `/sdd-discover force <skill>` | Forzar skill específico |

## Reglas

- **Un solo perfil dominante** si hay conflicto, listar ambos y preguntar
- **Nunca asumir stack** sin evidencia en archivos de configuración
- **Preservar estado** en `.sdd-state.json` entre sesiones
- **Documentar decisiones** de routing en el output

## Verification

Antes de dar por terminado el descubrimiento:

- [ ] Se detectaron correctamente los archivos de configuración
- [ ] El perfil coincide con el stack real del proyecto
- [ ] La recomendación de skill siguiente es clara
- [ ] El usuario entendió el flujo sugerido