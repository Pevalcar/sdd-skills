# Tareas — 001-sdd-review

- [ ] T1: Crear estructura de directorios para sdd-review
  - RF: RF-1, RF-4
  - Hecho cuando: carpeta skills/sdd-review/ con subcarpetas src/ y templates/
  - Archivos: skills/sdd-review/, src/, templates/

- [ ] T2: Implementar parser de spec.md
  - RF: RF-1
  - Hecho cuando: funciones parse_assumptions() que extraen sección de suposiciones
  - Archivos: skills/sdd-review/src/parser.js

- [ ] T3: Implementar generador de preguntas de duda
  - RF: RF-2
  - Hecho cuando: funciones generate_doubts() que producen preguntas adversariales
  - Archivos: skills/sdd-review/src/doubter.js

- [ ] T4: Implementar generador de alternativas
  - RF: RF-3
  - Hecho cuando: funciones generate_alternatives() que producen alternatives JSON
  - Archivos: skills/sdd-review/src/alternatives.js

- [ ] T5: Implementar generador de reporte markdown
  - RF: RF-4
  - Hecho cuando: funciones generate_report() que producen report.md
  - Archivos: skills/sdd-review/src/report.js

- [ ] T6: Crear SKILL.md completo
  - RF: RF-1 a RF-4
  - Hecho cuando: SKILL.md con ASUMPTIONS, Rationalizations, Verification checklist
  - Archivos: skills/sdd-review/SKILL.md

- [ ] T7: Crear README.md documentación
  - RF: RF-4
  - Hecho cuando: README.md con uso, output, referencias
  - Archivos: skills/sdd-review/README.md

- [ ] T8: Tests unitarios para cada módulo
  - RF: todos
  - Hecho cuando: tests pasando, cobertura > 80%
  - Archivos: skills/sdd-review/tests/test_*.js

- [ ] T9: Integrar con sdd-flow
  - RF: RF-4
  - Hecho cuando: sdd-flow actualizado con sdd-review como fase opcional
  - Archivos: skills/sdd-flow/SKILL.md