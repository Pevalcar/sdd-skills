---
name: sdd-pair
description: Pair programming con TDD paso a paso para una historia de usuario refinada. Inspira en /pair de hola-ai.
disable-model-invocation: true
---

# Pair Programming SDD

Tú eres el driver: escribes el código. Yo soy el navigator: reviso, decido y te digo sí o no. Trabajamos una historia por sesión.

## 🛡️ ASSUMPTIONS I'M MAKING:

1. Existe una historia refinada aprobada en `specs/NNN-xxx/story-0N.md`
2. Existe un plan aprobado en `specs/NNN-xxx/plan.md`
3. El usuario aprobará cada paso antes de continuar
4. No se harán commits automáticos
→ Correct me now or I'll proceed.

## When to Use

- Tienes una historia de usuario refinada y aprobada
- Quieres implementar con TDD paso a paso (test → rojo → código mínimo → verde)
- Quieres parar después de cada test para revisar

## When NOT to Use

- No hay historia refinada aprobada (ejecutar /sdd-story primero)
- No hay plan aprobado (ejecutar /sdd-plan primero)
- Quieres implementar sin TDD o sin parar entre pasos (ir a /sdd-implement)

## Proceso

### Paso 1: Review

Lee la historia que te doy (idealmente el bloque generado por `/sdd-story`: criterios, plan, "Out of scope").
Revisa el plan contra el código actual. Si algo ya no encaja, dímelo antes de empezar.
Si no hay plan, propón uno de 5 bullets máximo y espera mi aprobación.

### Paso 2: Lista de tests

Desde los acceptance criteria, propón **la lista de tests: solo nombres, no los escribas aún.**
Dice **en qué nivel** se testa cada uno. Preferir el nivel más alto práctico.
Marca los criterios que no se pueden probar automáticamente como **manual verification**.
Espera mi aprobación. Esta lista es el spec: la apruebo yo, no tú.

### Paso 3: Ciclo

Un paso = un test de la lista:

1. Escribe el test.
2. Ejecútalo y **muestra que falla** (rojo).
3. Escribe el **código mínimo** que haga pasar el test. Nada que el test no requiera.
4. Ejecuta los tests y muestra que pasan (verde).

Por defecto haces **1 paso** y paras. Si digo "haz N", haces N ciclos completos (test → código → verde, uno tras otro), nunca "N tests y luego el código". En un lote, muestra los tests primero y luego el código: los tests son lo que más necesito revisar.

Cuando pares, envía un micro mensaje:

```
✅ Passes "<test name>". <qué hice en una línea> (<archivo:línea>)
Decided: <juicio de valor, si aplica>
¿Cambiar algo o continuar con "<siguiente test>"?
```

### Para inmediatamente (incluso a medio lote) si:

- Necesitas tomar una decisión de diseño que no está en el plan.
- Piensas en añadir algo que no pedí, aunque parezca razonable.
- Hacer pasar un test requeriría cambiar, saltar o borrar un test.
- Has tenido dos intentos sin llegar a verde.
- El paso supera ~50 líneas o toca más de 3 archivos: propone dividirlo.

### Reglas de tests

- El valor esperado viene del acceptance criterion, **nunca calculado con la misma lógica que el código**.
- Testea el comportamiento a través de la interfaz pública, no detalles internos.

### Paso 4: Check

Cuando la lista esté verde:

- Verifiquemos juntos los criterios marcados como **manual verification**.
- Sugiere que obtenga una revisión de un contexto nuevo; no revises tu propio código.
- Si algo se repite o parece desordenado, **sugiere** el refactor; yo decido. Refactor solo con tests verdes, y nunca mezclado con nueva funcionalidad.
- Si tomamos una decisión que aplica a todo el proyecto, propón una línea para el archivo de instrucciones del agente.

### Paso 5: Commit

**Nunca commits.** Cuando haya un buen punto (tests verdes, una unidad lógica), avísame y sugiere el mensaje, separando funcionalidad y refactor en diferentes commits. Yo hago el commit.

## Verificación

- [ ] Lista de tests con nombres (sin escribir aún)
- [ ] Nivel de testing definido para cada uno
- [ ] Criterios manuales marcados
- [ ] Usuario aprobó la lista de tests
- [ ] Ciclo TDD: test → rojo → código mínimo → verde
- [ ] Un paso a la vez, parar después de cada uno
- [ ] Micro mensaje al parar
- [ ] No commits automáticos

## See Also

- `/sdd-story` — Refinar historia con acceptance criteria
- `/sdd-implement` — Implementar tarea con TDD (alternativa a pair)
- `references/definition-of-done.md` — Universal quality bar