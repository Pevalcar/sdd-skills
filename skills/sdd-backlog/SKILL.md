---
name: sdd-backlog
description: Convierte una idea vaga en un backlog corto de historias de usuario verticales. Inspira en /backlog de hola-ai.
disable-model-invocation: true
---

# Generador de Backlog — Historias de Usuario

Convierte una idea vaga en un backlog corto de historias de usuario verticales (una línea cada una, sin criterios de aceptación, sin detalles técnicos).

## 🛡️ ASSUMPTIONS I'M MAKING:

1. El usuario tiene una idea vaga de funcionalidad que quiere construir
2. La constitución existe en `docs/constitution.md` y está aprobada
3. El backlog es el paso previo a la especificación formal (sdd-spec)
4. El usuario ajustará y aprobará el backlog antes de continuar
→ Correct me now or I'll proceed.

## When to Use

- Inicio de una nueva funcionalidad o feature
- Cuando tienes una idea vaga y necesitas destilarla en historias de usuario
- Antes de ejecutar `/sdd-spec` para generar la especificación formal

## When NOT to Use

- Ya tienes un backlog definido y aprobado
- Quieres escribir código directamente (ir a /sdd-implement o /sdd-pair)
- La spec ya existe y está aprobada

## Proceso

### Paso 1: Escuchar la idea

Recibe la idea o funcionalidad del usuario. Es una discusión abierta, puedes usar diagramas para entender mejor la idea.

### Paso 2: Entender sin empujar

Tu propósito es entender mejor la idea, no empujar atrás todavía. Nunca discutas arquitectura, stack, patrones ni detalles de implementación.

### Paso 3: Identificar decisiones costosas

Pregunta qué decisiones serían costosas de cambiar después. Solo identifícalas, no las diseñes.

### Paso 4: Proponer el backlog

Genera un backlog corto de historias de usuario verticales. El usuario lo ajustará.

## Reglas

- **No inventar requisitos.** Solo dividir lo que el usuario dijo. Si ves un hueco, pregunta; no lo rellenes.
- **Cada historia entrega valor por sí sola** y corta por todas las capas del sistema. Nunca divides por capa.
- **No historias técnicas.** El actor nunca es el desarrollador o el sistema. La infraestructura se construye dentro de la primera historia que la necesite.
- **Pocas historias.** 10-15 máx. Más vale añadir que cortar.
- **Una línea por historia.** Sin acceptance criteria, sin detalles técnicos, sin estimaciones ni prioridades.
- La primera historia es siempre stack definition. La segunda es siempre el walking skeleton (la más pequeña usable de principio a fin).

## Formato de salida

```markdown
## Context
<una o dos líneas: qué es y para quién>
Expensive decisions: <las que apliquen, o "none">

## Backlog
1. As a <actor>, I want <action>, so that <benefit>.
2. As a <actor>, I want <action>, so that <benefit>. Requires: #1
```

Añade `Requires: #N` solo cuando una historia no tenga sentido sin otra.

## Gate de aprobación

Cuando termines, ofrece guardar el contexto y el stack en el archivo de instrucciones del agente (AGENTS.md). Las historias van al tracker o herramienta de issues del usuario; no las guardes en archivos a menos que el usuario lo pida.

## Verificación

- [ ] Cada historia entrega valor independiente
- [ ] Cada historia corta por todas las capas del sistema
- [ ] No hay historias técnicas (actor ≠ desarrollador/sistema)
- [ ] Máximo 15 historias
- [ ] Formato de una línea por historia
- [ ] Primera historia es stack definition
- [ ] Segunda historia es walking skeleton
- [ ] Usuario ha ajustado y aprobado el backlog

## See Also

- `/sdd-story` — Refinar una historia del backlog con acceptance criteria
- `/sdd-spec` — Generar especificación RF-EARS completa
- `references/definition-of-done.md` — Universal quality bar