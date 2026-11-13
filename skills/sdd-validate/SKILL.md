---
name: sdd-validate
description: "Recorrido RF por RF verificando tests, evidencia de código y cumplimiento constitucional. Fail-closed: rechaza si falta algo."
disable-model-invocation: true
---

# Validador SDD — Trazabilidad RF→Test

Comprueba que cada requisito funcional está cubierto, tiene evidencia de código y cumple la constitución. Fail-closed: si falta algo, se rechaza.

## 🛡️ ASUMPTIONS I'M MAKING:

1. La spec existe en `specs/NNN-xxx/spec.md`
2. Los tests existen en directorio `tests/` o `test/`
3. Todos los códigos han sido ejecutados al menos una vez
4. El Definition of Done está disponible en `references/definition-of-done.md`
5. La constitución está disponible en `docs/constitution.md`
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
SPEC → PLAN → TASKS → IMPLEMENT → VALIDATE → VARIANTS
                │         │          │          │
                ▼         ▼          ▼          ▼
            RF mapping  TDD loop   DoD+Const  Variant eval
```

## Process

1. **Lee la spec.** `specs/001-xxx/spec.md`
2. **Lee la constitución.** `docs/constitution.md`
3. **Lee los tests.** directorio `tests/` o `test/`
4. **Busca evidencia de código.** archivos fuente que implementan cada RF
5. **Ejecuta test suite.** Con el comando del perfil detectado
6. **Genera reporte de validación:**
   - Tabla RF→Test→Code con estado de cada requisito
   - Cobertura parcial y gaps identificados
   - Comentarios sobre edge cases no cubiertos
   - **Constitution Compliance** checklista ítem por ítem

## Formato output

```markdown
# Validación — 001-xxx

## Recorrido RF por RF

| RF | Test | Código | Resultado | Comentario |
|---|---|---|---|---|
| RF-1 | test_create_user | src/user.js: createUser() | ✅ PASA | ... |
| RF-2 | test_login_flow | ⚠️ SIN CÓDIGO | ❌ FALLA | Test mockea en vez de usar código real |
| RF-3 | test_invalid_input | src/validators.js | ✅ PASA | ... |

## Constitution Compliance

| Principio | RF Afectado | Cumple | Comentario |
|-----------|-------------|--------|------------|
| Zero-warnings | RF-2 | ❌ | Warning en validación |
| TDD mandatory | All | ✅ | Tests escritos primero |

## Cobertura

- RF cubiertos: 2/5
- Tests sin RF mapping: [test_edge_case_1]
- RF sin test: [RF-2, RF-5]
- RF sin código: [RF-2]

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

**Razón:** <explicación breve con razones específicas>
```

## Validation Rules

- Ejecuta los tests relevantes con el comando del repositorio
- Si RF no tiene test: marcar como ❌
- Si RF no tiene código implementado: marcar como ❌ (no basta con test)
- Si algún principio de constitución se viola: marcar como ❌
- Veredicto **fail-closed**: si falta un RF o test o código → RECHAZADA
- Sólo si TODO RF tiene test + código + pasa test → ✅ Spec cumplida

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Tests pasan, así que está done"* | "Tests pass" ≠ done si no hay código ni cumplimiento constitucional | DoD completo + Constitution required |
| *"Ya lo probé manual"* | Manual testing doesn't persist, no scales | Automated tests mandatory |
| *"Coverage es suficiente"* | Coverage metrics can be misleading (edge cases missed) | Runtime verification required |
| *"El código funciona visualmente"* | Visual ≠ correct. Edge cases, error paths may fail silently | All verification gates must pass |
| *"Faltan 2 RF, pero son triviales"* | What's trivial to you may be complex to others | All RF must have tests + code |

## Verification

Antes de declarar feature completa:

- [ ] Every RF has traceability to specific test(s)
- [ ] Every RF has evidence of implementation (code file/line)
- [ ] Tests relevant executed and passing
- [ ] Full test suite passes (no regressions)
- [ ] Build succeeds con cero warnings
- [ ] Type checking passes (where applicable)
- [ ] Linting passes
- [ ] Edge cases definidos en spec cubiertos
- [ ] Código revela intención (no necesita comentarios)
- [ ] Sin código muerto o debug output
- [ ] Constitution Compliance checklista pasado ítem por ítem
- [ ] Tabla RF→Test→Code generada y revisada
- [ ] Ningún RF queda sin cubrir
- [ ] Veredicto final tomado: ✅ Spec cumplida / ⚠️ Incompleta / ❌ Rechazada

## See Also

- `definition-of-done.md` - Universal quality bar
- `test-driven-development` - Testing patterns
- `code-review-and-quality` - Review checklist