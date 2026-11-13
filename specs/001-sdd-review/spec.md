# Spec 001 - sdd-review - Doubt-driven review

## Contexto y objetivo

El skill sdd-review proporciona una revisión profunda de especificaciones y decisiones de diseño técnicas mediante el patrón doubt-driven-development. Detecta ambigüedades, suposiciones no validadas, y decisiones que podrían tener alternativas más simples o seguras. Actúa como un "adversarial reviewer" que cross-examina cada no-trivial decision.

## Usuarios / actores

- Arquitectos de software que necesitan validar decisiones de diseño
- Líderes técnicos que quieren asegurar que las decisiones son sólidas
- Agentes AI que necesitan revisar sus propias decisiones
- Equipos que quieren reducir el riesgo de decisiones técnicas incorrectas

## Historias de usuario

- H1: Como arquitecto de software, quiero una revisión profunda de decisiones técnicas, para validar que no hay alternativas mejores o riesgos no considerados.
- H2: Como agente AI, quiero cross-examinar mis decisiones con un enfoque adversarial, para asegurar que no estoy cometiendo suposiciones inválidas.
- H3: Como líder técnico, quiero documentar las críticas y validaciones importantes, para que el equipo entienda el porqué de las decisiones tomadas.

## Requisitos funcionales (criterios de aceptación en EARS)

- RF-1: CUANDO se invoca sdd-review con una spec o plan, EL SISTEMA analiza suposiciones explícitas y detecta ambigüedades no cubiertas por sdd-clarify (salida: lista de dudas críticas).
- RF-2: SI hay decisiones técnicas no justificadas, EL SISTEMA genera prompts específicos para cross-examining (salida: preguntas de duda dirigida).
- RF-3: MIENTRAS el análisis identifica suposiciones inválidas, EL SISTEMA genera alternativas factibles y documenta pros/cons de cada una (salida: tabla de comparación).
- RF-4: EL SISTEMA produce un reporte estructurado con: suposiciones detectadas, alternativas evaluadas, y decisiones recomendadas (formato: markdown con secciones claras).

## Requisitos no funcionales (RNF)

- RNF-1: El skill debe ser ejecutable en menos de 30 segundos para specs pequeñas (< 500 líneas)
- RNF-2: El output debe ser legible por humanos y machine-parseable (markdown con estructura consistente)
- RNF-3: El skill debe funcionar con specs en markdown y plan.md sin depender de herramientas externas

## Casos límite

- Spec con más de 1000 líneas (debería fragmentar o requerir más tiempo)
- Spec sin sección de suposiciones explícitas
- Plan con múltiples decisiones técnicas conflicting
- Docenas de RF (debería procesar en chunks)
- Spec en idioma no español/inglés
- Archivos corruptos o inaccesibles

## Fuera de alcance

- No es un sustituto de sdd-clarify (no detecta errores de implementación)
- No reemplaza code review manual
- No analiza código fuente, solo specs y planes
- No genera código ni implementa cambios

## Criterios de finalización

- RF-1 a RF-4 implementados y testeados
- El skill detecta al menos 80% de las suposiciones comunes en specs de prueba
- Output es accionable por el usuario
- Documentación completa en SKILL.md

## Dudas abiertas

- [NECESITA ACLARACIÓN] ¿Cómo diferenciar entre suposiciones válidas y inválidas?
- [NECESITA ACLARACIÓN] ¿Cuál es el umbral de "no-trivial" para aplicar doubt-driven?