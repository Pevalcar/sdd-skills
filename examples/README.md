# Ejemplos de Uso de SDD Skills

Bienvenido a los ejemplos de las Skills SDD. Estos ejemplos demuestran cómo usar las diferentes skills en situaciones reales.

## Índice de Ejemplos

### [quick-start.md](./quick-start.md)
**Tiempo estimado:** 5 minutos

Guía rápida para empezar a usar las Skills SDD. Cubre:
- Instalación de skills
- Configuración inicial
- Primeros comandos
- Estructura de archivos generados

### [full-flow-example.md](./full-flow-example.md)
**Tiempo estimado:** 30-60 minutos

Ejemplo completo del flujo SDD usando el skill `/sdd-flow`. Muestra:
- Implementación completa de autenticación
- Cada paso del wizard interactivo
- Archivos generados en cada etapa
- Verificación final de cobertura

## Ejemplo de Uso Avanzado

### Skill: sdd-stories (Próximamente)

Basado en los patrones de [Hola AI](https://github.com/mouredev/hola-ai), las siguientes skills generarán historias de usuario ricas:

```bash
/sdd-stories "login Dofus"
```

Generará:
- Historias INVEST completas
- Escenarios Gherkin para cada RF
- Criterios de aceptación detallados

## Patrones de Historias de Usuario

### INVEST Pattern

Todas las historias siguen el patrón **INVEST**:

```
Como <rol>,
quiero <acción>,
para <beneficio>.
```

### Gherkin Syntax

Los criterios de aceptación se expresan en Gherkin:

```gherkin
Dado <condición inicial>
Cuando <acción del usuario>
Entonces <resultado esperado>
```

## Referencias

- [Arquitectura del Sistema](../docs/architecture.md)
- [Patrones INVEST](../docs/INVEST-patterns.md)
- [Hola AI](https://github.com/mouredev/hola-ai)
- [hello-sdd](https://github.com/mouredev/hello-sdd) - Referencia original