---
name: sdd-story
description: Toma una historia de usuario del backlog, añade acceptance criteria y propone un mini plan. Inspira en /story de hola-ai.
disable-model-invocation: true
---

# Refinador de Historias de Usuario

Refina una sola historia de usuario, justo antes de construirla. Tú propones y el usuario decide.

## 🛡️ ASSUMPTIONS I'M MAKING:

1. Existe un backlog aprobado en `specs/NNN-xxx/backlog.md`
2. El usuario ha seleccionado una historia específica para refinar
3. La constitución existe en `docs/constitution.md` y está aprobada
4. El usuario aprobará explícitamente la historia refinada antes de continuar
→ Correct me now or I'll proceed.

## When to Use

- Tienes un backlog aprobado y quieres refinar una historia específica
- Necesitas acceptance criteria antes de pasar a la especificación formal
- Quieres definir un mini plan antes de implementar

## When NOT to Use

- No hay backlog aprobado (ejecutar /sdd-backlog primero)
- Quieres escribir código directamente (ir a /sdd-pair o /sdd-implement)
- La historia ya está refinada y aprobada

## Proceso

### Paso 1: Leer la historia

Lee la historia que el usuario te da y revisa el archivo de instrucciones del agente (AGENTS.md) y la constitución para entender el contexto.

### Paso 2: Acceptance criteria

Propón criterios de aceptación en formato Given/When/Then. Solo describen *qué* ve o recibe el usuario, nunca *cómo* se implementa.

### Paso 3: Evaluar división

Si necesita más de 3 criterios, evalúa dividirla. Entrega las nuevas historias en formato de backlog (`As a…, I want…, so that…`) para que el usuario las añada al tracker, y continúa con la primera.

### Paso 4: Mini plan

Propón un mini plan de 5 bullets máximo, sin código ni nombres de archivo. Cómo corta a través de las capas.

### Paso 5: Esperar aprobación

Espera a que el usuario apruebe. Ajustad hasta que diga sí.

## Reglas

- **No inventar requisitos.** Si falta información, pregúntame.
- **Lo más simple que cumple los criterios.** Sin abstracciones, capas, configuración ni patrones "para el futuro".
- **Sugerir, no decidir.** Si un patrón podría ayudar, menciónalo bajo "Suggestions" con su por qué. Solo sugiere si hay una señal concreta en el código actual, no de antemano.

## Formato de salida

Un bloque listo para pegar en el issue.

```markdown
## Story
As a <actor>, I want <action>, so that <benefit>.

## Acceptance criteria
- [ ] Given <context>, when <action>, then <result>.
- [ ] ...

## Plan
- ...

## Out of scope
- <qué se deja fuera de esta historia, para que no se cule>

## Suggestions (tu decisión)
- <opcional>
```

## Gate de aprobación

Espera a que el usuario apruebe. Ajustad hasta que diga sí.

## Verificación

- [ ] Acceptance criteria en formato Given/When/Then
- [ ] Máximo 3 criterios (o historia dividida)
- [ ] Mini plan de ≤5 bullets, sin código ni nombres de archivo
- [ ] Out of scope definido
- [ ] Usuario ha aprobado explícitamente

## See Also

- `/sdd-backlog` — Generar backlog de historias de usuario
- `/sdd-spec` — Generar especificación RF-EARS completa
- `references/definition-of-done.md` — Universal quality bar