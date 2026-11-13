# Arquitectura del Sistema de Skills SDD

## Visión General

El sistema SDD (Spec-Driven Development) está diseñado como un **pipeline de skills** donde cada componente tiene una responsabilidad única y bien definida.

## Componentes

### 1. sdd-constitution
**Propósito:** Establecer los principios innegociables del proyecto.

```
Input:  requisitos del usuario sobre stack, qualidad, tests
Output: docs/constitution.md (máximo 15 líneas)
```

**Reglas:**
- Cada principio < 40 palabras
- Verificables: "máximo", "obligatorio", "debe", "no"
- Espera aprobación antes de escribir

### 2. sdd-spec
**Propósito:** Convertir ideas vagas en especificaciones acordadas.

```
Input:  idea o requisito
Output: specs/001-xxx/spec.md con RF en notación EARS
```

**Formato EARS:**
- RF-1: CUANDO <evento>, EL SISTEMA <respuesta>
- RF-2: SI <condición no deseada>, ENTONCES EL SISTEMA <respuesta>
- RF-3: MIENTRAS <estado>, EL SISTEMA <respuesta>
- RF-4: EL SISTEMA <comportamiento permanente>

### 3. sdd-clarify
**Propósito:** Revisión QA automática de especificaciones.

```
Input:  spec.md existente
Output: notas QA agregadas al final del archivo
```

**Checklist QA:**
- RF verificables (no adjectivos)
- Historias en formato "Como <rol>, quiero <acción>, para <beneficio>"
- Casos límite definidos
- Fuera de alcance explícito

### 4. sdd-plan
**Propósito:** Diseño técnico con pseudocódigo ejecutable.

```
Input:  spec.md
Output: specs/001-xxx/plan.md
```

**Secciones:**
1. Arquitectura de módulos
2. Modelo de datos con ejemplo JSON
3. Algoritmo principal (pseudocódigo)
4. Contrato de la CLI
5. Decisiones técnicas
6. Cobertura de RF

### 5. sdd-tasks
**Propósito:** Descomposición en tareas verificables.

```
Input:  plan.md
Output: specs/001-xxx/tasks.md
```

**Formato:**
- Tareas pequeñas y verificables
- Ordenadas por dependencia
- Checkboxes para tracking

### 6. sdd-implement
**Propósito:** Implementación TDD por tarea.

```
Input:  Tn (número de tarea)
Output: Código + tests, marca Tn completada
```

**Flujo TDD:**
1. Lee la tarea específica
2. Escribe el test primero
3. Implementa el código mínimo
4. Ejecuta tests
5. Marca como completada

### 7. sdd-validate
**Propósito:** Verificación final de cobertura.

```
Input:  spec.md + tests
Output: tabla de trazabilidad RF→Test
```

**Veredicto:**
- ✅ Spec cumplida
- ❌ RF pendientes
- ⚠️ SIN TEST

### 8. sdd-flow
**Propósito:** Orquestador interactivo del flujo completo.

```
Input:  idea o funcionalidad
Output: todo el pipeline automáticamente
```

## Patrones de Diseño

### Inmutabilidad
- Cada skill genera su output sin modificar inputs anteriores
- Estado guardado en `.sdd-state.json`

### Single Responsibility
- Cada skill tiene una única razón de cambio
- Plantillas separadas de lógica

### Testability
- Cada skill puede ser testeada individualmente
- Plantillas con placeholders verificables

## Extensibilidad

### Agregar una nueva skill

1. Crear carpeta `sdd-nombre/`
2. Añadir SKILL.md, README.md, template
3. Registrar en `skills-lock.json`

### Personalizar plantillas

Las plantillas son templates markdown con placeholders:
- `<Nombre>` - Será reemplazado por el sistema
- `<rol>` - Para historias de usuario
- `<evento>` - Para requisitos funcionales

## Integración con Hola AI Patterns

Este sistema incorpora:

1. **INVEST Patterns** para historias de usuario
2. **Gherkin Syntax** para criterios de aceptación
3. **Given-When-Then Structure** para tests
4. **Living Documentation** through markdown templates