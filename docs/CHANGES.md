# Plan de Acción QA - sdd-skills

**Estado:** Diagnóstico completo. Cambios documentados para implementación.

## Resumen Ejecutivo

El repositorio tiene los ingredientes correctos (skills autocontenidas, approval gates, anti-rationalizaciones) pero el flujo SDD no está garantizado por el sistema - depende de la disciplina del agente.

---

## P0 - Críticos

### 1. Unificar definición del flujo

**Problema:** Tres fuentes de verdad contradicen:
- README.md: `discover → specification → code`
- AGENTS.md: `Setup → Spec → Clarify → Plan → Review → Tasks → Implement → Validate → Variants`
- sdd-discover/SKILL.md: `Setup → Spec → Clarify → Plan → Review → Tasks → Implement → Validate → Variants`

**Solución:** 
- [ ] Unificar en README.md usando notación SDD
- [ ] Actualizar AGENTS.md para reflejar el flujo corregido
- [ ] Eliminar sección duplicada "Pasos" en sdd-discover/SKILL.md

### 2. Integrar sdd-variants como fase obligatoria

**Problema:** sdd-variants está implementada pero no se invoca en sdd-flow

**Solución:**
- [ ] Añadir Phase 5: Variants en sdd-flow/SKILL.md
- [ ] Añadir gate de aprobación humana: "¿Se aprueba la variante recomendada? Sí/No"
- [ ] Actualizar .sdd-state.json para reflejar fase de variantes

### 3. Crear sdd-orchestrator

**Problema:** El flujo depende de la disciplina del agente

**Solución:**
- [ ] Crear skill `sdd-orchestrator` que:
  - Lea .sdd-state.json
  - Determine fase actual
  - Bloquee avance si gate anterior no está aprobado
  - Redirija a skill correcta si agente intenta improvisar

---

## P1 - Alto

### 4. Validación constitucional en sdd-validate

**Problema:** sdd-validate no valida contra docs/constitution.md

**Solución:**
- [ ] Añadir sección "Constitution Compliance" checklista ítem por ítem
- [ ] Hacer que veredicto sea ❌ Rechazada si algún RF viola constitución

### 5. Hacer fail-closed sdd-validate

**Problema:** Solo verifica test coverage, no evidencia de código

**Solución:**
- [ ] Exigir evidencia de código + test por RF
- [ ] Veredicto binario: ✅ Cumple / ❌ No cumple
- [ ] Si falta un RF o test → FAIL (no warning)

### 6. Clarificar sdd-review vs sdd-variants

**Problema:** Ambas exploran alternativas, pero sin límite claro

**Solución:**
- [ ] Documentar: `sdd-review` = alternativas de diseño, `sdd-variants` = alternativas de implementación
- [ ] O fusionarlas si hacen lo mismo

---

## P2 - Mejora

### 7. Corregir typos

- [ ] ASUMPTIONS → ASSUMPTIONS
- [ ] Adiconals → Additional  
- [ ] coBERTURA → COBERTURA
- [ ] Consistencia idioma ES/EN

### 8. Definir rúbrica de scoring en sdd-variants

- [ ] Pesos explícitos para cada métrica
- [ ] Umbral mínimo de elegibilidad
- [ ] Eliminación automática si viola constitución

### 9. Scripts de validación

- [ ] Verificar spec.md tiene todas secciones obligatorias
- [ ] Verificar tasks.md mapea cada RF

---

## Estado actual de cambios realizados

| Skill | Estado | Comentario |
|-------|--------|------------|
| sdd-spec/SKILL.md | ✅ Actualizado | Eliminadas secciones stack/commands/structure |
| sdd-spec/spec-template.md | ✅ Actualizado | Formato RF-EARS limpio |
| sdd-discover/SKILL.md | ❌ Pendiente | Duplicado de secciones "Pasos" |
| sdd-flow/SKILL.md | ❌ Pendiente | No invoca sdd-variants |
| sdd-validate/SKILL.md | ❌ Pendiente | No valida constitución |
| sdd-variants/SKILL.md | ❌ Pendiente | Scoring subjetivo |

---

## Próximos pasos

1. **Commit de cambios iniciales** (sdd-spec)
2. **Actualizar sdd-discover** (eliminar duplicado)
3. **Crear sdd-orchestrator**
4. **Integrar sdd-variants en sdd-flow**
5. **Validar con user** antes de continuar