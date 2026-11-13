# Plantilla Maestra para Skills SDD

Toda skill debe seguir esta estructura. Copia este archivo como base para nuevas skills.

---

```markdown
---
name: sdd-nombre
description: "Descripción clara y concisa de lo que hace el skill."
disable-model-invocation: true
---

# Título del Skill

Descripción breve de la responsabilidad única del skill.

## 🛡️ ASUMPTIONS I'M MAKING:

1. [suposición sobre el contexto del proyecto]
2. [suposición sobre el stack/tecnología]
3. [suposición sobre el estado previo del proyecto]
→ Correct me now or I'll proceed.

## When to Use

- [cuándo invocar este skill]
- [señales de que este skill aplica]

## When NOT to Use

- [casos donde NO se usa]
- [alternativas a considerar]

## Process

[Pasos específicos del skill. Cada paso debe ser accionable.]

### Paso 1: Preparación
[qué leer, qué cargar, qué validar]

### Paso 2: Ejecución
[acción principal del skill]

### Paso 3: Salida
[formato de output esperado]

## Profile Rules

[Reglas específicas del perfil detectado. Dejar vacío si no aplica.]

Ejemplo para perfil game-dev:
- Todos los cálculos de posición deben usar floats, nunca ints
- El state machine debe ser determinista (misma entrada = misma salida)
- Los paquetes de red usan Little-Endian

## Rationalizations

[Tabla de excusas comunes y su realidad. Adaptar al dominio del skill.]

| Excusa | Realidad | Regla |
|--------|----------|-------|
| "Es rápido, no necesito..." | ... | ... |

## Output Format

[Plantilla exacta del output que genera el skill]

```markdown
# [Título]

[Contenido...]
```

## Verification

- [ ] Checklist de verificación post-ejecución
- [ ] Cada ítem debe ser objetivamente verificable

## See Also

- [[skill_relacionado_1]]
- [[skill_relacionado_2]]
- [perfil_aplicable](../../profiles/<perfil>/SKILL.md)
```

---

## Notas de Uso

1. **Frontmatter obligatorio:** `name`, `description`, opcionalmente `disable-model-invocation`
2. **ASUMPTIONS siempre al inicio:** Antes de cualquier proceso
3. **Process paso a paso:** Numerado, accionable, sin ambigüedad
4. **Profile Rules condicionales:** Solo si el skill tiene reglas específicas por perfil
5. **Verification obligatoria:** Lista de checkboxes objetivos
6. **Ver enlace a perfiles:** Usar rutas relativas a `profiles/`
