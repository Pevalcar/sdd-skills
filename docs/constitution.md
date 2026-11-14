# Constitución — sdd-skills

1. **Stack mínimo.** TypeScript/JavaScript moderno, npm como gestor de paquetes, sin dependencias innecesarias. Código ejecutable con `npm test`.

2. **Spec antes que código.** TODO requisito documentado en spec.md antes de implementar. Cada skill debe pasar por el flujo SDD completo.

3. **Separación lógica.** `skills/<skill-name>/` (código de skill), `specs/` (requisitos), `docs/` (documentación), `references/` (plantillas).

4. **Tests obligatorios.** Cada skill nueva incluye SKILL.md, README.md y verificación funcional. Verificar con `npx skills ls`.

5. **Persistencia controlada.** Estado del flujo guardado en `.sdd-state.json`. No sobrescribir archivos modificados sin backup previo.

6. **Idioma.** Responde siempre en el idioma del usuario (si escribe en español, responde en español). Documentación bilingüe ES/EN, mensajes de error claros, nombres de variables sin abreviaturas.
