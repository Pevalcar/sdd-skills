---
name: sdd-plan
description: Genera plan.md con módulos, modelo de datos, pseudocódigo, contrato CLI y decisiones técnicas.
disable-model-invocation: true
---

# Planificador SDD — Diseño técnico

Convierte una spec en un plan de implementación sin escribir código.

## 🛡️ ASUMPTIONS I'M MAKING:

1. La spec aprobada existe en `specs/NNN-xxx/spec.md`
2. La constitución existe en `docs/constitution.md`
3. `clarification.status = PASS` en `.sdd-state.json` (sdd-clarify aprobado)
4. No hay plan existente sin completar (verificar antes de sobrescribir)
→ Correct me now or I'll proceed.

## When to Use

- Spec está aprobada y validada
- Necesito diseñar implementación técnica
- Debo documentar decisiones antes de codificar

## When NOT to Use

- Sin spec aprobada todavía
- `clarification.status` no es PASS en `.sdd-state.json` (ejecutar /sdd-clarify primero)
- Quiere implementar directamente (ir a /sdd-implement)
- Plan ya existe y está completo

## Process

1. **Verifica gate.** `.sdd-state.json` debe tener `clarification.status = PASS`. Si no, ejecutar `/sdd-clarify` primero.
2. **Lee la spec.** `specs/001-xxx/spec.md` completa.
3. **Lee la constitución.** `docs/constitution.md` para principios.
4. **Genera `plan.md`** con estas secciones obligatorias:

## Plantilla de output

```markdown
# Plan NNN - <Nombre>

## Arquitectura de módulos
[Diagrama o lista con dependencias]

## Modelo de datos
```json
{ejemplo JSON con campo clave y descripción}
```

## Algoritmo principal (pseudocódigo)
[pseudocódigo claro, sin sintaxis del lenguaje]

## Contrato de la CLI
| Comando | Entrada | Salida | Código error |
|---|---|---|---|
| habits add | <args> | <output> | <código> |

## Decisiones técnicas
- **Decisión 1**: <justificación>
  - Alternativa descartada: <por qué>

## Cobertura de RF
| RF | Módulo | Test asociado |
|---|---|---|
| RF-1 | MóduloA | test_xxxx |
```

**Reglas:**
- Nada de código
- Cada RF debe tener COBERTURA explícita
- Justifica decisiones técnicas
- Respetar constitución

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Ya sé cómo hacerlo, no necesito plan"* | Planning is the task. Implementation sin plan is just typing | Documento escrito required |
| *"Los planes cambian, mejor agrego sobre la marcha"* | Los planes change cuando hay cambios NO previstos | Plan saves decisions made explicitly |
| *"Solo necesito pseudocódigo básico"* | Pseudocódigo sin estructura lleva a spaghetti | Architecture + data model + CLI contract required |
| *"Lo haré en mi cabeza"* | Context windows有限. Written plans survive sessions | Write it down |

## Verification

- [ ] Plan document save en `specs/NNN-xxx/plan.md`
- [ ] No pre-existing incomplete plan overwritten without user confirmation
- [ ] Every decision justified with alternative considered
- [ ] RF coverage table complete (every RF has module + test)
- [ ] Human reviewed and approved the plan