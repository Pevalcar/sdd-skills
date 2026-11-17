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