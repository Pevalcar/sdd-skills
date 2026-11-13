# Anti-Racionalizaciones — Universal

Tabla de excusas comunes que los agentes usan para saltarse pasos. Cada racionalización incluye la realidad técnica y la regla obligatoria.

Esta tabla se aplica a TODO cambio en TODO proyecto, independientemente del stack.

---

## Excusas Universales

| Excusa Común | Realidad | Regla Obligatoria |
|-------------|----------|-------------------|
| *"Es pequeño, no necesito tests"* | Cambios pequeños sin tests causan regresiones silenciosas | Todo componente o función crítica debe tener prueba unitaria o integración |
| *"Tragamos la excepción para no romper el flujo"* | Errores ocultos son peores que fallos explícitos | Capturar, registrar mensaje claro, fallar controladamente |
| *"Dejo código comentado, lo limpio después"* | Código muerto degrada mantenibilidad | Eliminar inmediatamente; base limpia en cada iteración |
| *"Ignoro warnings del linter/compilador"* | Warnings acumulados esconden bugs latentes | Zero-warnings policy en compilación y linter |
| *"El código funciona, ¿qué importa si es feo?"* | Legibilidad es requisito no negociable | Si otro dev no entiende en 30s, está mal |
| *"Ya lo probé manual, basta"* | Testing manual no persiste ni escala | Tests automatizados obligatorios para lógica crítica |
| *"Agregué una dependencia más, no pasa nada"* | Cada dependencia aumenta deuda técnica | Justificar toda nueva dependencia en el PR |
| *"Lo refactorizo después"* | El "después" nunca llega | Refactorizar solo si mejora el feature actual |
| *"Solo cambiaré esto y listo"* | Los cambios tienen efecto dominó | Evaluar impacto antes de modificar |

---

## Por Dominio

### Web/Frontend

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Usaré `any` en TypeScript porque es más rápido"* | Any destruye type-safety y causa bugs en runtime | Strict mode obligado; never any sin justificación explícita |
| *"Los useEffect son complicados, mejor callback directo"* | Callbacks desincronizan state y causan renders infinitos | Seguir pattern de dependencies array correctamente |
| *"No necesito accesibilidad ahora"* | A11y técnico legalmente requerido y buen UX | WCAG 2.1 AA mínimo desde día uno |

### Systems/Rust/Go

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Ignoro el error de unwrap()"* | Panic en producción cuesta minutos de downtime | Result/Option handling obligatorio |
| *"El borrow checker es muy estricto, lo evito con Arc<Mutex>"* | Locking innecesario mata performance y causa deadlocks | Diseño sin locks cuando sea posible |
| *"Las lifetimes son dolor, usaré &'static"* | Static references crean memory leaks | Diseñar ownership correcto desde inicio |

### Game Dev/Godot

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"El state machine puede tener drift偶尔"* | Desync posicional arruina multiplayer | Determinismo estricto en every tick |
| *"Godot maneja la física, yo no necesito calcular"* | Física no-determinista rompe replay/sync | Simular física en código si requiere sync |
| *"Un parche en el código del motor es más rápido"* | Parches se pierden en updates y rompen compatibilidad | Extensión via hooks o subclassing |

### Mobile

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"El ciclo de vida es automático, no lo manejo"* | Apps que crashlean en background/foreground rejection | Manejar explicitamente lifecycle events |
| *"No necesito manejar orientación/cambio de tamaño"* | Layout roturado en certain devices = mala UX | Tests en múltiples tamaños/orientaciones |
| *"El battery drain es problema del dispositivo"* | Apps que drenan batería son uninstalladas | Limitar work en background, usar JobScheduler |

### Infrastructure/DevOps

| Excusa | Realidad | Regla |
|--------|----------|-------|
| *"Hardcodeo las creds en el config para debug rápido"* | Credenciales en codebase = breach potencial | Usar secrets manager desde día uno |
| *"El YAML se ve bien, no necesita validación"* | Config malformada rompe deploy en producción | Schema validation en CI |
| *"Backup manual está bien para este proyecto"* | Recovery manual es lento y propenso a error | Automatizar backups desde día uno |

---

## Cómo Usar

1. **Al iniciar cualquier tarea**, el agente revisa esta tabla
2. **Si surge una excusa**, compara contra la tabla
3. **Si encuentra coincidencia**, explica por qué la excusa es incorrecta
4. **Aplicar la regla obligatoria** propuesta

Las rationalizaciones específicas del skill sobreescriben estas generales cuando aplican.
