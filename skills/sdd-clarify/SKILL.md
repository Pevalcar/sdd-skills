---
name: sdd-clarify
description: Revisa una spec como QA profesional para detectar ambigüedades, contradicciones y huecos antes de planificar.
disable-model-invocation: true
---

# Clarificador SDD — Revisión QA de especificaciones

Identifica problemas en una spec antes de pasar a planificación. Elimina dudas, conflictos y casos faltantes.

## 🛡️ ASUMPTIONS I'M MAKING:

1. La spec existe en `specs/NNN-xxx/spec.md`
2. La constitución opcionalmente existe en `docs/constitution.md`
3. El análisis busca problemas, no propone soluciones inmediatamente
→ Correct me now or I'll proceed.

## When to Use

- Spec escrita pero necesita validación QA
- Antes de pasar a planificación
- Para detecting edge cases y ambiguities

## When NOT to Use

- Spec no existe todavía (/sdd-spec primero)
- Ya se hizo revisión QA anteriormente
- Solo necesitas modificar spec, no revisar calidad

## Process

1. **Lee la spec.** `specs/001-xxx/spec.md` completa.
2. **Lee la constitución.** `docs/constitution.md` para validar principios.
3. **Actúa como QA.** Detecta sin resolver:

## Qué detectar (lista numerada)

| Categoría | Qué buscar |
|---|------------|
| **Ambigüedades** | Términos sin definir, comportamientos implícitos |
| **Contradicciones** | RF que se contradicen entre sí |
| **Casos límite faltantes** | Errores, límites, datos corruptos, null, vacío |
| **Conflictos con constitución** | Violaciones de principios innegociables |

## Output

Agrega sección al final de `spec.md`:

```markdown
## Revisión QA

### Ambigüedades restantes
1. [...]
2. [...]

### Contradicciones entre requisitos
1. [...]
2. [...]

### Casos límite no cubiertos
1. [...]
2. [...]

### Conflictos con constitución
1. [...]
2. [...]

### Resumen
- RF con ambigüedad: [lista]
- RF con contradicción: [lista]
- Casos límite faltantes: [lista]
```

**Reglas:**
- Solo detecta, no resuelve
- Usa formato de lista numerada
- Si todo está claro: "✅ No se detectan problemas críticos"

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Ya entendí lo que pasa, mejor sigo"* | Ambiguous specs lead to wrong implementations. Catching issues early saves hours | Spend time clarifying before implementing |
| *"Los requirements son obvios"* | Even clear requests have implicit assumptions. QA surfaces these | Always check for ambiguities |
| *"Esto toma mucho tiempo"* | 15 minutes of clarification prevents hours of rework | Early investment pays off |
| *"El cliente lo entiende, no necesito escribirlo"* | Client understanding ≠ written clarity. Documentation protects everyone | Capture in writing |

## Verification

- [ ] Lista numerada de ambigüedades (si existen)
- [ ] Contradicciones identificadas y listadas
- [ ] Casos límite no cubiertos detectados
- [ ] Conflictos con constitución verificados
- [ ] Output agregado al final de spec.md (no replacear contenido existente)