# Plan 001 - sdd-review - Doubt-driven review

## Arquitectura de módulos

```
sdd-review/
├── SKILL.md              # Skill definition
├── README.md             # Documentation
├── src/
│   ├── parser.js         # Parse spec.md and plan.md
│   ├── assumptions.js    # Extract assumptions section
│   ├── doubter.js        # Generate doubt prompts
│   ├── alternatives.js   # Generate alternative options
│   └── report.js         # Generate markdown report
└── templates/
    └── review-template.md
```

## Modelo de datos

```json
{
  "spec_path": "specs/001-xxx/spec.md",
  "plan_path": "specs/001-xxx/plan.md",
  "assumptions": [
    {
      "text": "string",
      "line": 42,
      "severity": "high|medium|low",
      "category": "tech|scope|data|integration"
    }
  ],
  "doubt_questions": [
    {
      "assumption": "string",
      "question": "¿Qué pasa si...?",
      "category": "alternative|validation|edge-case"
    }
  ],
  "alternatives": [
    {
      "problem": "string",
      "solution_a": { "approach": "string", "pros": [], "cons": [] },
      "solution_b": { "approach": "string", "pros": [], "cons": [] }
    }
  ]
}
```

## Algoritmo principal (pseudocódigo)

```
LEER: spec_path, plan_path
EXTRAER: sección de suposiciones del spec
PARA CADA suposición:
  CLASIFICAR: severidad (high/medium/low)
  GENERAR: preguntas de duda adversariales
  BUSCAR: en documentación oficial (opcional)
  GENERAR: alternativas factibles
GENERAR: reporte estructurado con:
  - Suposiciones detectadas
  - Preguntas para cross-examining
  - Alternativas evaluadas
GUARDAR: output en specs/001-xxx/review.md
```

## Contrato de la CLI

| Comando | Entrada | Salida | Código error |
|---------|---------|--------|--------------|
| `/sdd-review` | ninguno (lee el spec actual) | `specs/001-xxx/review.md` | 1 (archivo no encontrado) |

## Decisiones técnicas

- **Usar regex para parseo de markdown**: simple y efectivo, alternativa descartada: parser AST complejo (sobreequipo)
- **Generar output como markdown**: legible y fácil de versionar, alternativa descartada: JSON (menos accesible)
- **Hardcodear categorías de suposiciones**: más rápido que NLP, alternativa descartada: clasificación automática (demasiado complejo para este contexto)

## Cobertura de RF por módulo

| RF | Módulo | Test asociado |
|----|--------|---------------|
| RF-1 | parser.js, assumptions.js | test_parser.js |
| RF-2 | doubter.js | test_doubter.js |
| RF-3 | alternatives.js | test_alternatives.js |
| RF-4 | report.js | test_report.js |

## Perfil aplicable

- **Todas**: skill es tecnología-agnóstica
- **Reglas específicas**: Ninguna (es un meta-skill)