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

## Lifecycle Sequence (SDD Flow)

For a complete SDD workflow, the typical skill sequence is:

```
1.  sdd-setup/sdd-constitution  → Create AGENT.md and constitution
2.  sdd-spec                    → Define what we're building (RF-EARS)
3.  sdd-clarify                 → Review and refine spec (loop until clear)
4.  sdd-plan                    → Design technical implementation
5.  (optional) sdd-review      → Review assumptions and alternatives
6.  sdd-tasks                   → Break into verifiable tasks
7.  sdd-implement               → Build slice by slice (TDD)
8.  sdd-validate                → Verify RF→Test coverage, DoD
9.  (optional) sdd-variants      → Multi-variant exploration and ranking
```

Not every task needs every skill. A bug fix might only need:
`debugging-and-error-recovery` → `test-driven-development` → `code-review-and-quality`

### Your SDD Flow

```
Setup → Spec → Clarify → Plan → Review → Tasks → Implement → Validate → Variants
   ↓       ↓        ↓       ↓        ↓       ↓          ↓          ↓        ↓
sdd-     sdd-spec  sdd-    sdd-plan sdd-    sdd-tasks  sdd-       sdd-     sdd-variants
setup    clarify   clarify        review         implement  validate (optional)

## Skill Router Table

| Fase | When to Use | Skill to Invoke |
|------|-------------|-----------------|
| **Setup** | No AGENT.md o constitution | `/sdd-setup` |
| **Define** | Have a rough concept | `idea-refine` |
| **Define** | Need specs | `sdd-spec` |
| **Define** | Need to clarify spec | `sdd-clarify` |
| **Plan** | Have a spec, need plan | `sdd-plan` |
| **Review** | Need to review assumptions | `sdd-review` |
| **Build** | Need tasks from plan | `sdd-tasks` |
| **Build** | Need to implement | `incremental-implementation` |
| **Verify** | Implement complete | `sdd-validate` |
| **Review** | Explore alternatives | `sdd-variants` |

## Pasos

1. **Verifica setup.** Señaladores de proyecto y estado actual:
   - `AGENT.md` existe? ❌ No → `/sdd-setup`
   - `docs/constitution.md` existe? ❌ No → `/sdd-constitution`
   - `specs/NNN-xxx/spec.md` existe? ❌ No → `/sdd-spec`
   - Spec clarificada? ❌ No → `/sdd-clarify`
   - `plan.md` existe? ❌ No → `/sdd-plan`
   - Decisions reviewed? ❌ No → `/sdd-review` (opcional)
   - `tasks.md` existe? ❌ No → `/sdd-tasks`
   - Tasks implementadas? ❌ No → `/sdd-implement`
   - Implementación validada? ❌ No → `/sdd-validate`
   - Quieres explore variants? → `/sdd-variants`

2. **Lee la spec.** `specs/001-xxx/spec.md` completa.
3. **Lee la constitución.** `docs/constitution.md` para principios.
4. **Muestra estado actual del proyecto:**
   - `specs/` → specs encontrados
   - `tests/` → tests existentes
   - `.sdd-state.json` → estado del flujo
   - `package.json` → stack detectado
5. **Sugiere skill inicial correcto** basado en estado.

## Quick Reference

| Phase | Skill | One-Line Summary |
|-------|-------|-----------------|
| **Setup** | sdd-setup | Create AGENT.md and constitution |
| **Define** | sdd-spec | Generate spec with RF-EARS |
| **Define** | sdd-clarify | Review and refine spec |
| **Plan** | sdd-plan | Design technical implementation |
| **Review** | sdd-review | Review assumptions and alternatives |
| **Build** | sdd-tasks | Break into verifiable tasks |
| **Build** | sdd-implement | Implement with TDD |
| **Verify** | sdd-validate | Verify RF→Test coverage |
| **Review** | sdd-variants | Multi-variant exploration |
| **Context** | source-driven-development | Verify against official docs |
| **Context** | incremental-implementation | Build slice by slice |
| **Context** | doubt-driven-development | Cross-examine decisions |
| **Context** | test-driven-development | Prove each slice works |
| **Review** | code-review-and-quality | Review before merge |
| **Remove** | code-simplification | Reduce unnecessary complexity |
| **Ship** | git-workflow-and-versioning | Clean commit history |
| **Ship** | ci-cd-and-automation | Automated quality gates |
| **Ship** | documentation-and-adrs | Document decisions |
| **Ship** | observability-and-instrumentation | Add logs/metrics |
| **Ship** | shipping-and-launch | Deploy safely |

## Output Inicial

Muestra al usuario el estado actual del proyecto:

```
🔍 Estado del proyecto:
   AGENT.md: ✅ existe
   docs/constitution.md: ✅ existe
   specs/: ✅ 1 spec encontrada
   tests/: ❌ sin tests aún
   .sdd-state.json: ❌ no existe

📋 Skills disponibles:
   - /sdd-spec → Crear especificación
   - /sdd-clarify → Revisar espec
   - /sdd-plan → Crear plan técnico
   - /sdd-review → Revisar suposiciones (opcional)
   - /sdd-tasks → Generar tareas
   - /sdd-implement → Implementar (TDD)
   - /sdd-validate → Validar implementación

💡 Skill recomendado: /sdd-spec
   Razón: Tienes constitution pero sin spec actualmente.
```

## Pasos

1. **Verifica setup.** Señaladores de proyecto y estado actual:
   - `AGENT.md` existe? ❌ No → `/sdd-setup`
   - `docs/constitution.md` existe? ❌ No → `/sdd-constitution`
   - `specs/NNN-xxx/spec.md` existe? ❌ No → `/sdd-spec`
   - Spec clarificada? ❌ No → `/sdd-clarify`
   - `plan.md` existe? ❌ No → `/sdd-plan`
   - Decisions reviewed? ❌ No → `/sdd-review` (opcional)
   - `tasks.md` existe? ❌ No → `/sdd-tasks`
   - Tasks implementadas? ❌ No → `/sdd-implement`
   - Implementación validada? ❌ No → `/sdd-validate`
   - Quieres explore variants? → `/sdd-variants`

2. **Lee la spec.** `specs/001-xxx/spec.md` completa.
3. **Lee la constitución.** `docs/constitution.md` para principios.
4. **Muestra estado actual del proyecto:**
   - `specs/` → specs encontrados
   - `tests/` → tests existentes
   - `.sdd-state.json` → estado del flujo
   - `package.json` → stack detectado
5. **Sugiere skill inicial correcto** basado en estado.

## Quick Reference

| Phase | Skill | One-Line Summary |
|-------|-------|-----------------|
| **Setup** | sdd-setup | Create AGENT.md and constitution |
| **Define** | sdd-spec | Generate spec with RF-EARS |
| **Define** | sdd-clarify | Review and refine spec |
| **Plan** | sdd-plan | Design technical implementation |
| **Review** | sdd-review | Review assumptions and alternatives |
| **Build** | sdd-tasks | Break into verifiable tasks |
| **Build** | sdd-implement | Implement with TDD |
| **Verify** | sdd-validate | Verify RF→Test coverage |
| **Review** | sdd-variants | Multi-variant exploration |
| **Context** | source-driven-development | Verify against official docs |
| **Context** | incremental-implementation | Build slice by slice |
| **Context** | doubt-driven-development | Cross-examine decisions |
| **Context** | test-driven-development | Prove each slice works |
| **Review** | code-review-and-quality | Review before merge |
| **Remove** | code-simplification | Reduce unnecessary complexity |
| **Ship** | git-workflow-and-versioning | Clean commit history |
| **Ship** | ci-cd-and-automation | Automated quality gates |
| **Ship** | documentation-and-adrs | Document decisions |
| **Ship** | observability-and-instrumentation | Add logs/metrics |
| **Ship** | shipping-and-launch | Deploy safely |