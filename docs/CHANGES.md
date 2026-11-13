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
- [x] Unificar en README.md usando notación SDD
- [x] Actualizar AGENTS.md para reflejar el flujo corregido
- [x] Eliminar sección duplicada "Pasos" en sdd-disover/SKILL.md

### 2. Integrar sdd-variants como fase obligatoria

**Problema:** sdd-variants está implementada pero no se invoca en sdd-flow

**Solución:**
- [x] Añadir Phase 8: Variants en sdd-flow/SKILL.md
- [x] Añadir gate de aprobación humana: "¿Se aprueba la variante recomendada? Sí/No"
- [x] Actualizar .sdd-state.json para reflejar fase de variantes

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
- [x] Añadir sección "Constitution Compliance" checklista ítem por ítem
- [x] Hacer que veredicto sea ❌ Rechazada si algún RF viola constitución

### 5. Hacer fail-closed sdd-validate

**Problema:** Solo verifica test coverage, no evidencia de código

**Solución:**
- [x] Exigir evidencia de código + test por RF
- [x] Veredicto binario: ✅ Cumple / ❌ No cumple
- [x] Si falta un RF o test → FAIL (no warning)

### 6. Clarificar sdd-review vs sdd-variants

**Problema:** Ambas exploran alternativas, pero sin límite claro

**Solución:**
- [x] Documentar: `sdd-review` = alternativas de diseño, `sdd-variants` = alternativas de implementación

---

## P2 - Mejora

### 7. Corregir typos

- [x] ASUMPTIONS → ASSUMPTIONS
- [x] Adiconals → Additional  
- [x] coBERTURA → COBERTURA
- [x] Consistencia idioma ES/EN

### 8. Definir rúbrica de scoring en sdd-variants

- [x] Pesos explícitos para cada métrica (RF 30%, Constitution 25%, Simplicity 20%, Tests 15%, Maintainability 10%)
- [x] Umbral mínimo de elegibilidad definido
- [x] Eliminación automática si viola constitución

### 9. Scripts de validación

- [ ] Verificar spec.md tiene todas secciones obligatorias
- [ ] Verificar tasks.md mapea cada RF

---

## Estado actual de cambios realizados

| Skill | Estado | Comentario |
|-------|--------|------------|
| sdd-spec/SKILL.md | ✅ Actualizado | Eliminadas secciones stack/commands/structure |
| sdd-spec/spec-template.md | ✅ Actualizado | Formato RF-EARS limpio |
| README.md | ✅ Actualizado | Flujo unificado con sdd-variants, 10 skills listados |
| AGENTS.md | ✅ Actualizado | Flujo unificado con approval gates ↓ |
| sdd-discover/SKILL.md | ✅ Actualizado | Eliminadas secciones duplicadas, flujo unificado |
| sdd-flow/SKILL.md | ✅ Actualizado | Integrado sdd-variants como Phase 8 con gate obligratorio |
| sdd-validate/SKILL.md | ✅ Actualizado | Validación constitucional, fail-closed, evidencia de código requerida |
| sdd-variants/SKILL.md | ✅ Actualizado | Scoring objetivo con pesos explícitos y umbrales |
| verifications-gates.md | ✅ Actualizado | Corregidos typos (Adiconals→Additional, ASUMPTIONS) |
| sdd-plan/SKILL.md | ✅ Actualizado | Corregido typo (coBERTURA→COBERTURA) |
| .sdd-state.json | ✅ Actualizado | Añadido flow.phases con variants incluido |

---

## Próximos pasos

1. **Crear sdd-orchestrator** - Skill que orquesta el flujo guiado por estado
2. **Crear scripts de validación** - Verificar spec.md y tasks.md
3. **Validar con user** antes de continuar