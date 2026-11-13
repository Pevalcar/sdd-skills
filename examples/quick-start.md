# Quick Start Guide

Guía rápida para empezar a usar las Skills SDD en 5 minutos.

## Paso 1: Instalar las Skills

```bash
cd /ruta/a/tu/proyecto
npx skills add .opencode/skills/sdd-*
```

> **Nota:** Si usas el skills-lock.json:
> ```bash
> npx skills experimental_install
> ```

## Paso 2: Definir la Constitución

```bash
/sdd-constitution
```

Responde las preguntas sobre:
- Stack tecnológico
- Calidad requerida
- Pruebas obligatorias
- Límites del proyecto

**Output:** `docs/constitution.md`

## Paso 3: Generar la Primera Specification

```bash
/sdd-spec
```

Describe la funcionalidad. El asistente hará preguntas precisas.

**Output:** `specs/001-nombre-funcionalidad/spec.md`

## Paso 4: QA Automático

```bash
/sdd-clarify
```

Revisa y detecta ambigüedades automáticamente.

## Paso 5: Plan Técnico

```bash
/sdd-plan
```

Genera el plan de implementación con pseudocódigo.

## Paso 6: Tareas Verificables

```bash
/sdd-tasks
```

Descompone en tareas pequeñas y testables.

## Paso 7: Implementar (TDD)

```bash
/sdd-implement T1
/sdd-implement T2
# ... hasta completar
```

## Paso 8: Validar

```bash
/sdd-validate
```

Verifica que todos los RF están cubiertos.

## Todo en Un Solo Comando

Para saltarte los pasos manuales:

```bash
/sdd-flow "funcionalidad: login Dofus"
```

El wizard interactivo hará todo el pipeline automáticamente.

## Estructura de Archivos Generados

```
 proyecto/
 ├── docs/
 │   └── constitution.md      # Principios del proyecto
 └── specs/
     └── 001-login/
         ├── spec.md          # Especificación
         ├── plan.md          # Plan técnico
         └── tasks.md         # Tareas implementables
```

## ¿Qué Sigue?

- [Full Flow Example](./full-flow-example.md) - Ejemplo completo paso a paso
- [../CONTRIBUTINGING.md](../CONTRIBUTINGING.md) - Cómo contribuir
- [../docs/architecture.md](../docs/architecture.md) - Arquitectura del sistema