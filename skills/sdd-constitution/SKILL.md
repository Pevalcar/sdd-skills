---
name: sdd-constitution
description: Genera docs/constitution.md con principios cortos y verificables.
disable-model-invocation: true
---

# Generador de Constitución SDD

Define los principios innegociables del proyecto.

## 🛡️ ASUMPTIONS I'M MAKING:

1. Usuario tiene requisitos sobre stack, calidad, tests, límites
2. Constitution será documento vivo, no texto legal
3. Principios deben ser verificados, no solo aspiracionales
→ Correct me now or I'll proceed.

## When to Use

- Inicio de proyecto nuevo
- Antes de cualquier spec
- Cuando equipo necesita alineación en standards

## When NOT to Use

- Proyecto pequeño/solo developer (skip si no hay équipe)
- Constitution ya existe y solo necesita ajuste menor
- Timeboxed spikes donde specifications no aplican

## Pasos

1. **Recibe requisitos** sobre: stack, qualidad, tests, límites
2. **Genera `docs/constitution.md`** con máximo 15 líneas

## Plantilla

```markdown
# Constitución — <Nombre Proyecto>

1. **Stack mínimo.** <lenguaje> + <máx N dependencias>. <restricción>.
2. **Spec antes que código.** <cómo se valida>.
3. **Separación lógica.** <qué capas existen y su responsabilidad>.
4. **Tests obligatorios.** <quién escribe, cobertura mínima>.
5. **Persistencia controlada.** <qué se guarda, cómo, cuándo>.
6. **Idioma.** <qué idioma, convenciones>.
```

**Reglas:**
- Cada principio < 40 palabras
- Verificables: "máximo", "obligatorio", "debe", "no"
- Espera aprobación antes de escribir

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"No necesitamos constitution para este proyecto pequeño"* | Even small projects benefit from aligned standards | Skip only if solo developer, no team coordination needed |
| *"La constitution cambia todo el tiempo"* | Good constitution provides stability amid change | Review quarterly, update only when values change |
| *"Eso es paperwork administrativo"* | Constitution defines what "done" means for the team | Invest time upfront to prevent conflicts later |
| *"Ya sabemos cómo trabajar"* | Explicit > implicit. Written rules prevent drift | Document current practices, even if informal |

## Verification

- [ ] Constitución escrita en `docs/constitution.md`
- [ ] Máximo 15 principios (conciso, no dogma)
- [ ] Cada principio verificable (< 40 palabras, language claro)
- [ ] User aprobó explícitamente el contenido
- [ ] Principios consistentes entre sí (sin contradicciones)