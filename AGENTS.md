# AGENTS.md — sdd-skills

## Proyecto
Sistema de skills OpenCode para desarrollo guiado por especificación (SDD). Skills autocontenidas con reglas de dominio, verificación y flujo unificado. Tecnología-agnóstico, adaptable a cualquier stack.

## Comandos
- Ejecutar: `npx skills ls` (listar skills disponibles) | `/sdd-discover` (iniciar flujo SDD)
- Tests: `npx skills ls | grep sdd` (verificar skills SDD instalados)
- Lint/formato: por definir

## Estilo y convenciones
Documentación bilingüe ES/EN. Nombres de skills en kebab-case (sdd-spec, sdd-clarify, etc.). Mensajes de error claros en español.

## Reglas
- Lee docs/constitution.md y la spec activa en specs/ antes de tocar código.
- No añadas dependencias ni cambies el formato del JSON sin actualizar antes la spec.
- No modifiques archivos dentro de specs/ salvo petición explícita.

## Al terminar cualquier tarea
- Ejecuta `npx skills ls` para verificar que las skills están instaladas. Confirma que no hay warnings ni errores.

## 🦙 Ponytail (Opcional - Skill externa)

Ponytail es una skill independiente de DietrichGebert/ponytail que ayuda a escribir el mínimo código necesario. No es obligatoria para usar el flujo SDD.

### Instalación opcional

```bash
mkdir -p .opencode/skills/ponytail
cp <ruta-a-ponytail>/.opencode/skills/ponytail/SKILL.md .opencode/skills/ponytail/SKILL.md
```

### Activación

```bash
/ponytail          # Nivel por defecto (full)
/ponytail lite     # Nivel mínimo
/ponytail ultra    # Nivel máximo
/ponytail off      # Desactivar
```

### Comandos disponibles

| Comando | Qué hace |
|---------|----------|
| `/ponytail-review` | Revisar diff como senior dev |
| `/ponytail-audit` | Auditoría completa del repo |
| `/ponytail-debt` | Listar `shortcut:` comentarios deferidos |
| `/ponytail-gain` | Mostrar ahorros medidos |
| `/ponytail-help` | Referencia rápida |

### Reglas clave

- **La mejor código es el código que nunca escribiste**
- Regla de la escalera: ¿Necesita existir? ¿Ya está en el codebase? ¿Stdlib? ¿Feature nativa? ¿Dependencia? ¿Una línea? ¿Mínimo que funciona?
- Validación en trust boundaries, error handling, seguridad, accesibilidad — nunca se cortan