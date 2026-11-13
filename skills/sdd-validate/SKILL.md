---
name: sdd-validate
description: "Recorrido RF por RF verificando tests y completitud. Aplica Definition of Done universal."
disable-model-invocation: true
---

# Validador SDD — Trazabilidad RF→Test

Comprueba que cada requisito funcional está cubierto y pasa sus tests.

## 🛡️ ASUMPTIONS I'M MAKING:

1. La spec existe en `specs/NNN-xxx/spec.md`
2. Los tests existen en directorio `tests/` o `test/`
3. Todos los códigos han sido ejecutados al menos una vez
4. El Definition of Done está disponible en `references/definition-of-done.md`
→ Correct me now or I'll proceed.

## When to Use

- Implementación parece completa
- Antes de considerar feature shipped
- Necesito trazabilidad RF→Test documentada
- Antes de merge to main

## When NOT to Use

- Implementación aún incompleta
- Tests no escritos todavía
- Spec no existe (/sdd-spec first)

## The Validation Cycle

```
SPEC → PLAN → TASKS → IMPLEMENT → VALIDATE
                │         │          │
                ▼         ▼          ▼
            RF mapping  TDD loop   DoD checks
```

## Process

1. **Lee la spec.** `specs/001-xxx/spec.md`
2. **Lee los tests.** directorio `tests/` o `test/`
3. **Ejecuta test suite.** Con el comando del perfil detectado
4. **Genera reporte de validación:**
   - Tabla RF→Test con estado de cada requisito
   - Cobertura parcial y gaps identificados
   - Comentarios sobre edge cases no cubiertos

## Formato output

```markdown
# Validación — 001-xxx

## Recorrido RF por RF

| RF | Test | Resultado | Comentario |
|---|---|---|---|
| RF-1 | test_create_user | ✅ PASA | ... |
| RF-2 | test_login_flow | ⚠️ SIN TEST | Falta coverage edge case |
| RF-3 | test_invalid_input | ❌ FALLA | Bug encontrado |

## Cobertura

- RF cubiertos: 2/5
- Tests sin RF mapping: [test_edge_case_1]
- RF sin test: [RF-2, RF-5]

## Edge Cases Check

- Boundary cases definidos en spec cubiertos? [ ]
- Error paths manejados y testeados? [x]
- Security validations testeadas? [ ]

## Definition of Done Checklist

- [ ] Todos los acceptance criteria cumplidos
- [ ] Tests pasan 100% (sin filtros)
- [ ] Build limpio sin warnings
- [ ] No regressions en tests existentes
- [ ] Edge cases y error paths manejados
- [ ] Código revela intención (no necesita comentarios)
- [ ] Sin código muerto o debug output
- [ ] Linting pasa sin warnings
- [ ] Documentación actualizada (si aplica)
- [ ] Security review completado (si aplica)

## Veredicto

**Elegir uno:** [ ] ✅ Spec cumplida | [ ] ⚠️ Incompleta | [ ] ❌ Rechazada

**Razón:** <explicación breve conrazones específicas>
```

## Validation Rules

- Ejecuta los tests relevantes con el comando del repositorio
- Si RF no tiene test: marcar como ❌
- Veredicto requiere 2/3 criterios de finalización
- Todo RF debe ser verificable automáticamente

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Tests pasan, así que está done"* | "Tests pass" ≠ done si docs, regressions, runtime verification skipped | DoD completo required |
| *"Ya lo probé manual"* | Manual testing doesn't persist, no scales | Automated tests mandatory |
| *"Coverage es suficiente"* | Coverage metrics can be misleading (edge cases missed) | Runtime verification required |
| *"El código funciona visualmente"* | Visual ≠ correct. Edge cases, error paths may fail silently | All verification gates must pass |
| *"Faltan 2 RF, pero son triviales"* | What's trivial to you may be complex to others | All RF must have tests |

## Verification

Antes de declarar feature completa:

- [ ] Every RF has traceability to specific test(s)
- [ ] Tests relevant executed and passing
- [ ] Full test suite passes (no regressions)
- [ ] Build succeeds con cero warnings
- [ ] Type checking passes (where applicable)
- [ ] Linting passes
- [ ] Edge cases definidos en spec cubiertos
- [ ] Código revela intención (no necesita comentarios)
- [ ] Sin código muerto o debug output
- [ ] Tabla RF→Test generada y revisada
- [ ] Ningún RF queda sin cubrir
- [ ] Veredicto final tomado: ✅ Spec cumplida / ⚠️ Incompleta / ❌ Rechazada

## See Also

- `definition-of-done.md` - Universal quality bar
- `test-driven-development` - Testing patterns
- `code-review-and-quality` - Review checklist