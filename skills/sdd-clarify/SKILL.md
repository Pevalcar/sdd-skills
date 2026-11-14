---
name: sdd-clarify
description: Revisa una spec como QA profesional para detectar ambigüedades, contradicciones y huecos antes de planificar.
disable-model-invocation: true
---

# Clarificador SDD — Revisión QA de especificaciones

Identifica problemas en una spec antes de pasar a planificación. Elimina dudas, conflictos y casos faltantes.

## 🛡️ ASSUMPTIONS I'M MAKING:

1. La spec existe en `specs/NNN-xxx/spec.md` (NNN = número de feature)
2. La constitución opcionalmente existe en `docs/constitution.md`
3. El análisis busca problemas, no propone soluciones inmediatamente
→ Correct me now or I'll proceed.

## When to Use

- Spec escrita pero necesita validación QA
- Antes de pasar a planificación
- Para detectar edge cases y ambigüedades

## When NOT to Use

- Spec no existe todavía (/sdd-spec primero)
- Ya se hizo revisión QA y la spec no ha cambiado desde entonces
- Solo necesitas modificar spec, no revisar calidad

## Process

1. **Lee la spec.** `specs/001-xxx/spec.md` completa.
2. **Lee la constitución.** `docs/constitution.md` para validar principios.
3. **Actúa como QA. Detecta sin resolver, clasificando por severidad:**
   🔴 Crítico / 🟡 Alto / 🟢 Medio

## Qué detectar

| Categoría | Qué buscar |
|---|---|
| Ambigüedades | Términos sin definir, comportamientos implícitos, cuantificadores vagos |
| Contradicciones | RF que se contradicen entre sí o internamente |
| Casos límite faltantes | Errores, límites, null, vacío, datos corruptos |
| Conflictos con constitución | Violaciones de principios innegociables |
| Requisitos no testeables | AC sin criterio objetivo de verificación |
| RF sin AC | Requisito funcional sin criterio de aceptación |
| Dependencias circulares | RF que se referencian mutuamente |
| Requisitos no funcionales ausentes | Seguridad, rendimiento, accesibilidad, observabilidad |
| Scope creep | RF no derivados del problema original |

## Output Format

Cada ítem con prefijo de severidad y RF afectado:

```
### 🔴 Crítico
- RF-1: Termino "login rápido" sin definición de qué significa

### 🟡 Alto
- RF-2: No especifica timeout para operaciones de red

### 🟢 Medio
- RF-3: Uso de "muy fácil" sin métrica clara
```

## Veredicto QA

- [ ] PASS — 0 conflictos constitucionales, 0 ambigüedades 🔴, ≤2 🟡
- [ ] FAIL — ≥1 conflicto constitucional o >3 ambigüedades 🔴
- → Si FAIL, `sdd-plan` NO debe ejecutarse hasta resolver.

**Reglas:**
- Solo detecta, no resuelve
- Usa formato de lista numerada con severidad
- Si todo está claro: "✅ No se detectan problemas críticos"
- Si PASS: "✅ No se detectan problemas críticos"

## Rationalizations

| "Las specs ambiguas llevan a implementaciones incorrectas..." | ... |
| "Si no hay tiempo para QA, los bug-costs son mayores" | ... |

## Verification

- [ ] Lista numerada de ambigüedades con severidad
- [ ] Contradicciones identificadas y listadas
- [ ] Casos límite no cubiertos detectados
- [ ] Conflictos con constitución verificados
- [ ] Output agregado al final de spec.md (no reemplaza contenido existente)
- [ ] Veredicto QA declarado (PASS/FAIL)
- [ ] `.sdd-state.json` actualizado con `clarification.status`
- [ ] Si FAIL, `sdd-plan` bloqueado

## See Also

- `/sdd-spec` — Generar especificación
- `/sdd-plan` — Diseñar implementación
- `definition-of-done.md` — Universal quality bar
- `anti-rationalizations.md` — Excusas comunes vs realidad