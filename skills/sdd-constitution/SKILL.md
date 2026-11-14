---
name: sdd-constitution
description: Genera docs/constitution.md con principios cortos, citables y verificables que anclan los gates de sdd-validate y sdd-variants.
version: 1.0.0
disable-model-invocation: true
---

# Generador de Constitución SDD

Define los principios innegociables del proyecto. La constitución es el **contrato fundacional** que alimenta los gates automáticos de `sdd-clarify`, `sdd-validate` y `sdd-variants`.

Los principios son innegociables **durante un ciclo de proyecto**. Se revisan al cierre de cada ciclo mediante el proceso de versionado (§Vida de la constitución).

## 🛡️ ASSUMPTIONS I'M MAKING:

1. El usuario tiene requisitos sobre stack, calidad, tests y límites del proyecto.
2. Cada principio será **verificable** (tendrá un campo `Verificación:`) o estará marcado explícitamente como `[NO VERIFICABLE — solo guía]`.
3. La constitución alimenta los gates de `sdd-validate` y `sdd-variants`; sin ella, esos gates quedan sin criterio objetivo.
4. La aprobación es humana, no del agente.
5. **Nunca escribir código sin autorización explícita del usuario.** Ninguna skill escribe código hasta que el usuario confirme explícitamente.
6. **Bloqueo de flujo hasta confirmar constitución.** Si `docs/constitution.md` no existe o no está aprobada, ninguna skill posterior (sdd-spec, sdd-plan, sdd-implement, etc.) puede ejecutarse.

→ Correct me now or I'll proceed.

## When to Use

- Inicio de proyecto nuevo, antes de escribir cualquier spec.
- Cuando el equipo necesita alinear estándares de calidad, stack o tests.
- Cuando `docs/constitution.md` no existe y el flujo SDD va a comenzar.
- Cuando se cierra un ciclo y toca revisar principios (nueva versión).

## When NOT to Use

- `docs/constitution.md` ya existe y solo se necesita un ajuste menor → usa el flujo de versionado (§Vida de la constitución), no regeneres desde cero.
- Timeboxed spikes o pruebas de concepto donde el flujo SDD completo no aplica.
- **Proyecto pequeño o solo developer → NO es razón para saltarla.** La constitución ancla los gates de `sdd-validate` y `sdd-variants`. Puede ser de 2-3 principios, no de 10.

## Relación con otras skills

| Skill | Cómo consume la constitución |
|---|---|
| `sdd-clarify` | Cita principios por ID (P-001…) al detectar conflictos en la spec. |
| `sdd-validate` | Verifica compliance ítem por ítem contra cada principio. |
| `sdd-variants` | Elimina automáticamente variantes que violen un principio innegociable. |
| `verification-gates.md` | Define la DoD universal; la constitución **la complementa, no la duplica**. |

---

## Proceso

### 1. Recibe requisitos

Pide al usuario información sobre:
- **Stack**: lenguaje, framework, dependencias permitidas.
- **Calidad**: cobertura mínima, estándares de revisión, linters.
- **Tests**: quién los escribe, qué tipos (unit / integration / e2e).
- **Límites**: tamaño máximo de módulo, dependencias máximas, restricciones de arquitectura.
- **Idioma y convenciones**: idioma del código, de los commits, de la documentación.

Si el usuario no aporta algún punto, propón un valor por defecto razonable y **márcalo como supuesto** en el borrador.

### 2. Genera borrador con IDs estables

Genera un borrador de `docs/constitution.md` **en memoria** (no lo escribas todavía) con:

- **Máximo 10 principios.**
- IDs estables `P-001`, `P-002`, …, `P-0NN`.
- **Los IDs no se reutilizan nunca.** Si eliminas P-003, el siguiente principio es P-004. Esto protege las citas de `sdd-clarify` en specs antiguas.

### 3. Añade `Verificación:` a cada principio

Cada principio **debe** incluir un campo `Verificación:` con una de estas tres formas:

| Forma | Cuándo usarla | Ejemplo |
|---|---|---|
| **A — Comando ejecutable** | Hay un comando que reporta el estado | `npm ls --depth=0 --json \| jq '.dependencies \| length'` ≤ 3 |
| **B — Regla de conteo verificable** | Hay un archivo parseable con la métrica | `coverage/lcov.info` reporta `lines.covered / lines.total ≥ 0.80` |
| **C — No verificable automáticamente** | Requiere juicio humano | `[NO VERIFICABLE — revisión humana en PR]` |

**Regla dura:** si un principio no tiene `Verificación:`, la skill **no permite guardar** la constitución. Es un fail-closed en el momento de creación, igual que `sdd-validate` lo es en el momento de validación.

### 4. Gate de aprobación humana

Presenta el borrador al usuario con un resumen y pregunta explícitamente:

```markdown
## Gate de aprobación

Borrador de constitución listo:
- Principios: 6 (P-001 a P-006)
- Verificables automáticamente: 4
- [NO VERIFICABLE — solo guía]: 2 (P-004, P-006)

¿Apruebas el contenido?
  [ ] Sí → escribir docs/constitution.md y registrar en .sdd-state.json
  [ ] No → indicar cambios necesarios (la skill no escribe nada hasta nueva aprobación)

## 🔒 Reglas de bloqueo (obligatorias)

1. **No escribir código sin autorización explícita.** Ninguna skill escribe código, modifica archivos de implementación ni crea pruebas hasta que el usuario confirme explícitamente con "Sí" o "Aprobado".
2. **Flujo bloqueado sin constitución.** Si `docs/constitution.md` no existe o no está aprobada, `sdd-spec`, `sdd-plan`, `sdd-tasks`, `sdd-implement` y `sdd-validate` no pueden ejecutarse.
3. **Confirmación requerida antes de guardar.** La skill no escribe `docs/constitution.md` hasta que el usuario seleccione explícitamente "Sí" en el gate de aprobación.

**Regla dura:** si el usuario no selecciona "Sí", la skill **no escribe ningún archivo** y el flujo permanece bloqueado en esta fase.

## What happens after approval

Una vez el usuario aprueba:
1. Se escribe `docs/constitution.md`.
2. Se registra en `.sdd-state.json` como `approved_phases: ["constitution"]`.
3. Se desbloquea `sdd-spec` para la siguiente fase.
4. **Ningún código se escribe todavía** — solo se puede proceder a `sdd-spec` para definir requisitos.