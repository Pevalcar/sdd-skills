# Arquitectura del Sistema de Skills SDD (V2)

## Visión General

El sistema SDD (Spec-Driven Development) V2 está diseñado como un **sistema universal y agnóstico a tecnología**, complementado con **perfiles adaptativos** que se cargan según el stack detectado.

```
┌─────────────────────────────────────────────────────┐
│                    Core SDD                         │
│  discover → constitution → spec → clarify           │
│       → plan → tasks → implement → validate          │
└─────────────────────────────────────────────────────┘
                          ↕
┌─────────────────────────────────────────────────────┐
│                 Perfiles Adaptativos                 │
│  web-frontend | systems | game-dev | mobile | infra │
└─────────────────────────────────────────────────────┘
                          ↕
┌─────────────────────────────────────────────────────┐
│              Material de Referencia                  │
│  templates | checklists | anti-rationalizations     │
└─────────────────────────────────────────────────────┘
```

## Componentes Core

### 1. sdd-discover (NUEVO - Meta-skill)
**Propósito:** Analizar repositorio, detectar perfil, rutear al skill correcto.

```
Input:  directorio de trabajo
Output: matriz de skills aplicables + perfil detectado
```

**Detección automática:**
| Archivos encontrados | Perfil activado |
|---------------------|-----------------|
| `package.json`, `tsconfig.json` | web-frontend |
| `Cargo.toml`, `go.mod` | systems |
| `project.godot`, `.godot/` | game-dev |
| `pubspec.yaml`, `Podfile` | mobile |
| `Dockerfile`, `.github/workflows/` | infrastructure |

### 2. sdd-constitution
**Propósito:** Establecer principios innegociables del proyecto.

```
Input:  requisitos del usuario sobre stack, calidad, tests
Output: docs/constitution.md (máximo 15 líneas)
```

**Reglas:**
- Cada principio < 40 palabras
- Verificables: "máximo", "obligatorio", "debe", "no"
- Espera aprobación antes de escribir

### 3. sdd-spec
**Propósito:** Convertir ideas vagas en especificaciones acordadas.

```
Input:  idea o requisito
Output: specs/NNN-xxx/spec.md con RF en notación EARS
```

**Mejoras V2:**
- ASUMPTIONS explícitas al inicio
- Tabla de anti-racionalizaciones
- Verification gates obligatorias

### 4. sdd-clarify
**Propósito:** Revisión QA automática de especificaciones.

```
Input:  spec.md existente
Output: notas QA agregadas al final del archivo
```

**Checklist QA (V2):**
- RF verificables (no adjectivos)
- Historias en formato "Como <rol>, quiero <acción>, para <beneficio>"
- Casos límite definidos
- Fuera de alcance explícito
- Consistencia con constitución

### 5. sdd-plan
**Propósito:** Diseño técnico con pseudocódigo ejecutable.

```
Input:  spec.md
Output: specs/NNN-xxx/plan.md
```

**Secciones (V2):**
1. Arquitectura de módulos
2. Modelo de datos con ejemplo JSON
3. Algoritmo principal (pseudocódigo)
4. Contrato de la CLI
5. Decisiones técnicas con alternativas descartadas
6. Cobertura de RF por módulo
7. Reglas específicas del perfil detectado

### 6. sdd-tasks
**Propósito:** Descomposición en tareas verificables.

```
Input:  plan.md
Output: specs/NNN-xxx/tasks.md
```

**Formato (V2):**
- Tareas pequeñas y verificables (≤ 30 min)
- Ordenadas por dependencia
- Checkboxes para tracking
- "Hecho cuando:" explícito
- RF cubiertos mapeados

### 7. sdd-implement
**Propósito:** Implementación TDD por tarea.

```
Input:  Tn (número de tarea)
Output: Código + tests, marca Tn completada
```

**Flujo TDD (V2):**
1. Lee la tarea específica
2. Escribe test primero (RED)
3. Ejecuta test → debe fallar
4. Implementa código mínimo (GREEN)
5. Ejecuta test → debe pasar
6. Refactoriza si necesario
7. Marca como completada
8. Verification checklist obligatorio

### 8. sdd-validate (ACTUALIZADO V2.1)
**Propósito:** Verificación final de cobertura con Constitution compliance.

```
Input:  spec.md + tests + constitution
Output: tabla de trazabilidad RF→Test→Code + veredicto binario
```

**Veredicto (V2):**
- ✅ Spec cumplida (todo RF tiene test + código + pasa)
- ❌ RF pendientes (faltan tests o código)
- **Fail-closed:** cualquier problema = Rechazada

**Mejoras V2.1:**
- Requiere evidencia de CODE además de tests
- Valida Constitution compliance ítem por ítem
- Veredicto binario sin ambigüedades

### 9. sdd-flow (ACTUALIZADO V2.1)
**Propósito:** Orquestador interactivo del flujo completo.

```
Input:  idea o funcionalidad
Output: todo el pipeline automáticamente
```

**Mejoras V2.1:**
- Inicia con `/sdd-discover` automático
- Carga reglas del perfil detectado
- Aplica verification gates en cada fase
- Guarda checkpoint en .sdd-state.json
- Requiere aprobación humana en fases críticas
- **Incluye sdd-variants como Phase 8 obligatorio con gate de aprobación**

### 10. sdd-variants (NUEVO V2.1)
**Propósito:** Exploración y ranking de variantes de implementación.

```
Input:  spec.md + plan.md
Output: variants-ranking.md con shortlist ranqueada
```

**Scoring:**
- RF Coverage (30%): % de RF con implementation
- Constitution (25%): ¿Cumple los principios innegociables?
- Simplicity (20%): LOC + Complejidad ciclomática
- Tests (15%): Cobertura + calidad de tests
- Maintainability (10%): Naming + claridad

**Mejoras V2.1:**
- Scoring objetivo con pesos explícitos
- Umbral mínimo de elegibilidad definido
- Eliminación automática si viola constitución

## Perfiles Adaptativos

### web-frontend/SKILL.md
- TypeScript strict mode
- Bundle size monitoring
- Accessibility WCAG 2.1 AA
- Testing patterns: Jest + Testing Library

### systems/SKILL.md
- Error handling obligatorio (Result/Option)
- Memory safety first
- Zero-warnings policy
- Language-specific: Rust/Go/Python/C#

### game-dev/SKILL.md
- Determinismo estricto en cálculos
- State machines documentados
- Network packet validation
- Object pooling para frequent instantiation

### mobile/SKILL.md
- Lifecycle management explicit
- Memory leak prevention
- Platform parity considerations
- Battery impact awareness

### infrastructure/SKILL.md
- IaC-only philosophy
- Security-first mindset
- Immutability principles
- Rollback procedures required

## References Transversales

### skill-template.md
Plantilla maestra que todas las skills deben seguir:
- Frontmatter obligatorio
- ASUMPTIONS section
- Process paso a paso
- Rationalizations table
- Verification checklist

### anti-rationalizations.md
Tabla universal de excusas comunes vs realidad técnica.

### verification-gates.md
Checklists por fase y por perfil tecnológico.

### definition-of-done.md
Barra de calidad universal aplicable a TODO cambio.

## Patrones de Diseño

### Inmutabilidad
- Cada skill genera su output sin modificar inputs anteriores
- Estado guardado en `.sdd-state.json`
- Planes existentes protegidos contra sobrescritura accidental

### Single Responsibility
- Cada skill tiene una única razón de cambio
- Plantillas separadas de lógica
- Perfiles encapsulan reglas de dominio

### Extensibilidad
- Agregar nuevo skill: copiar plantilla, seguir estructura
- Agregar nuevo perfil: crear SKILL.md con reglas específicas
- Material referencial centralizado en `references/`

### Testability
- Cada skill puede ser testeada individualmente
- Plantillas con placeholders verificables
- Verification gates objetivas

## Integración con Hola AI Patterns

Este sistema incorpora:

1. **INVEST Patterns** para historias de usuario
2. **Gherkin Syntax** para criterios de aceptación
3. **Given-When-Then Structure** para tests
4. **Living Documentation** through markdown templates
5. **Anti-rationalization tables** desde agent-skills referencia
6. **Definition of Done** transversal

## Flujos de Uso

### Nuevo Proyecto
```bash
/sdd-discover          # Detectar perfil
/sdd-flow "feature X"  # Wizard completo
```

### Proyecto Existente
```bash
/sdd-discover resume   # Continuar desde estado previo
```

### Skill Específico
```bash
/sdd-spec              # Solo generar spec
/sdd-implement T3      # Solo implementar tarea 3
```
