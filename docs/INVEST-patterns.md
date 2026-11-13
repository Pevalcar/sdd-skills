# INVEST Patterns & Gherkin Format

Este documento describe los patrones de historias de usuario y criterios de aceptación que las skills SDD utilizan, inspirados en metodologías de desarrollo ágil y specification-driven development.

## INVEST Pattern

Todas las historias de usuario generadas siguen el patrón **INVEST**:

### I - Independent (Independiente)
- Cada historia puede ser valorada por separado
- No depende de otras historias

### N - Negotiable (Negociable)
- No es un contrato rígido
- Abierto a conversación y refinamiento

### V - Valuable (Valiosa)
- Aporta valor al usuario o al negocio
- Justifica su existencia

### E - Estimable (Estimable)
- Se puede estimar su esfuerzo de implementación
- Tiene suficiente contexto

### S - Small (Pequeña)
- Puede implementarse en un sprint
- Tiempo estimado: 1-3 días

### T - Testable (Testeable)
- Tiene criterios de aceptación claros
- Se puede verificar automáticamente

## Formato de Historias de Usuario

```
Como <rol>,
quiero <acción>,
para <beneficio>.
```

**Ejemplo:**
```
Como usuario registrado,
quiero recuperar mi contraseña,
para acceder a mi cuenta sin contactar soporte.
```

## Gherkin Syntax

Los criterios de aceptación se expresan en **Gherkin** para que sean ejecutables por tests automatizados:

### Given-When-Then Structure

```gherkin
Dado <condición inicial>
Cuando <acción del usuario>
Entonces <resultado esperado>
```

### Ejemplos

```gherkin
Dado un usuario registrado con email válido
Cuando ingresa su email en "Olvidé mi contraseña"
Entonces recibe un email con enlace de recuperación
```

```gherkin
Dado un usuario sin sesión activa
Cuando intenta acceder a "/mi-cuenta"
Entonces es redirigido al login
```

```gherkin
Dado un producto con stock > 0
Cuando agrega 1 unidades al carrito
Entonces el carrito muestra "✓ Agregado"
```

## Relación con hello-sdd

El repositorio [mouredev/hello-sdd](https://github.com/mouredev/hello-sdd) es una referencia fundamental. Diferencias clave:

| Aspecto | hello-sdd | SDD Skills |
|---------|-----------|------------|
| **Formato** | Markdown manual | Templates automatizados |
| **Pipeline** | Manual | Wizard interactivo |
| **TDD** | Opcional | Obligatorio |
| **QA** | Manual | Automatizado |
| **Integración** | Standalone | OpenCode Skills |

## Mejores Prácticas

### 1. Un RF por línea
```markdown
RF-1: CUANDO el usuario inicia sesión, EL SISTEMA valida credenciales
RF-2: SI las credenciales son incorrectas, EL SISTEMA muestra error
```

### 2. Historias con comas
```markdown
H1: Como <rol>, quiero <acción>, para <beneficio>.
```

### 3. Verificables, no descriptivos
✅ **Correcto:**
- "El sistema muestra mensaje de error"
- "El usuario puede ver su historial"

❌ **Incorrecto:**
- "El sistema es rápido"
- "La UI es intuitiva"

### 4. Testables con Gherkin
Cada RF debe traducirse a al menos un escenario Gherkin:

| RF | Escenario Gherkin |
|----|-------------------|
| RF-1 | `Dado usuario, Cuando login, Entonces token` |
| RF-2 | `Dado sin-login, Cuando /protegido, Entonces redirect` |

## Referencias

- [Spec-Driven Development](https://github.com/mouredev/hello-sdd)
- [INVEST Checklist](https://www.extensibleassociates.com/blog/2017/05/09/invest-checklist-for-user-stories/)
- [Gherkin Reference](https://cucumber.io/docs/gherkin/)