---
name: sdd-validate
description: Recorrido RF por RF verificando tests y completitud.
disable-model-invocation: true
---

# Validador SDD — Trazabilidad RF→Test

Comprueba que cada requisito funcional está cubierto y pasa sus tests.

## 🛡️ ASUMPTIONS I'M MAKING:

1. La spec existe en `specs/NNN-xxx/spec.md`
2. Los tests existen en directorio `tests/` o `test/`
3. Todos los códigos han sido ejecutados al menos una vez
→ Correct me now or I'll proceed.

## When to Use

- Implementación parece completa
- Antes de considerar feature shipped
- Necesito trazabilidad RF→Test documentada

## When NOT to Use

- Implementación aún incompleta
- Tests no написаны todavía
- Spec no existe (/sdd-spec first)

## Process

1. **Lee la spec.** `specs/001-xxx/spec.md`
2. **Lee los tests.** directorio `tests/` o `test/`
3. **Genera reporte de validación:**

## Formato output

```markdown
# Validación — 001-xxx

## Recorrido RF por RF

| RF | Test | Resultado | Comentario |
|---|---|---|---|
| RF-1 | test_xxxx | ✅ PASA | ... |
| RF-2 | test_yyyy | ❌ FALLA | ... |

## Cobertura
- RF cubiertos: X/Y
- Tests sin RF: [...]
- RF sin test: [...]

## Veredicto

**Elegir uno:** [ ] ✅ Spec cumplida | [ ] ⚠️ Incompleta | [ ] ❌ Rechazada

**Razón:** <explicación breve>
```

**Reglas:**
- Ejecuta los tests relevantes
- Si RF no tiene test: marcar como ❌
- Veredicto requiere 2/3 criterios de finalización

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Tests pasan, así que está done"* | "Tests pass" ≠ done si docs, regressions, runtime verification skipped | DoD completo required |
| *"Ya lo probé manual"* | Manual testing doesn't persist, no scales | Automated tests mandatory |
| *"Coverage es suficiente"* | Coverage metrics can be misleading (edge cases missed) | Runtime verification required |
| *"El código funciona visualmente"* | Visual ≠ correct. Edge cases, error paths may fail silently | All verification gates must pass |

## Verification

Antes de declarar feature completa:

- [ ] Cada RF tiene trazabilidad hacia test(s) específico(s)
- [ ] Tests relevantes ejecutados y pasando
- [ ] Tabla RF→Test generada y revisada
- [ ] Ningún RF queda sin cubierta (❌ marked si aplica)
- [ ] Tests existentes siguen pasando (sin regressions)
- [ ] Veredicto final tomado: ✅ Spec cumplida / ⚠️ Incompleta / ❌ Rechazada