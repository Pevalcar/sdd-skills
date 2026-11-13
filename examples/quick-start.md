# Quick Start — Ejemplo Rápido

Este ejemplo muestra el flujo completo desde cero hasta validación.

## Paso 1: Descubrir Perfil

```bash
/sdd-discover
```

**Output esperado:**
```
🔍 Perfil detectado: game-dev
📁 Stack: Godot 4.x, GDScript typed

📋 Estado actual del proyecto:
  ✗ constitution.md no existe
  ✗ spec.md no existe
  ✗ plan.md no existe
  ✗ tasks.md no existe
  ✗ Tests no ejecutados

💡 Skill recomendado: /sdd-constitution
   Razón: No hay constitution definida.

¿Continuar? [s/n]
```

## Paso 2: Crear Constitución

```bash
/sdd-constitution
```

**Input del usuario:**
> Stack: Godot 4.2+, GDScript typed, GUT para tests, servidor Python asyncio

**Output generado (`docs/constitution.md`):**
```markdown
# Constitución — Dofus Emulator

1. **Stack mínimo.** Godot 4.2+ + GDScript typed + Python asyncio. Máximo 3 dependencias externas por módulo.

2. **Spec antes que código.** Todo RF debe tener spec aprobada antes de implementar. Sin spec = no code.

3. **Separación lógica.** Cliente (Godot) ↔ Servidor (Python). Comunicación vía packets binarios Little-Endian.

4. **Tests obligatorios.** GUT para cliente, pytest para servidor. Cobertura mínima: 80% línea.

5. **Determinismo estricto.** State machine debe ser determinista: misma input → misma output.

6. **Idioma.** Español para specs y documentación técnica. Código en inglés.
```

## Paso 3: Generar Especificación

```bash
/sdd-spec
```

**Entrevista secuencial (máx 6 preguntas):**
1. ¿Qué funcionalidad específica quieres implementar?
2. ¿Quiénes son los usuarios/actores principales?
3. ¿Cuál es el comportamiento esperado en caso de error?
4. ¿Hay casos límite importantes a considerar?
5. ¿Qué queda explícitamente fuera de alcance?
6. ¿Cómo sabremos que está terminado?

**Output generado (`specs/001-login/spec.md`):**
```markdown
# Spec 001 - Login Dofus con OAuth

## Contexto y objetivo
Implementar sistema de login usando OAuth2 para autenticación con cuentas Dofus.

## Usuarios / actores
- Jugadores que desean iniciar sesión
- Sistema de autenticación externo (Andromeda)

## Historias de usuario
- H1: Como jugador, quiero iniciar sesión con mi cuenta Dofus, para acceder al juego.

## Requisitos funcionales (criterios de aceptación en EARS)
- RF-1: CUANDO el jugador selecciona "Iniciar sesión con Dofus", EL SISTEMA redirige al endpoint OAuth de Andromeda (salida: URL de autorización).
- RF-2: SI la autenticación OAuth falla (token inválido o expirado), ENTONCES EL SISTEMA muestra mensaje de error y opción de reintentar (salida 1).
- RF-3: MIENTRAS el token OAuth está activo, EL SISTEMA mantiene sesión válida sin requerir login adicional (salida: session cookie).
- RF-4: DONDE el jugador tiene credenciales válidas, EL SISTEMA genera ticket de acceso al servidor de juego (comportamiento permanente).

## Casos límite
- Token OAuth expirado durante sesión
- Redirección fallida a endpoint OAuth
- Múltiples sesiones simultáneas del mismo usuario

## Fuera de alcance
- Registro de nuevos usuarios (solo login)
- Recuperación de contraseña
- Autenticación 2FA

## Criterios de finalización
- RF-1 a RF-4 implementados y testeados
- Demo manual del flujo completo funciona
```

## Paso 4: Clarificación QA

```bash
/sdd-clarify
```

**Output agregado al final de spec.md:**
```markdown
## Revisión QA

### Ambigüedades restantes
1. Tiempo máximo de duración de sesión no especificado
2. Mensaje exacto de error no definido

### Contradicciones entre requisitos
(Ninguna detectada)

### Casos límite no cubiertos
1. Qué sucede si Andromeda está offline
2. Rate limiting en intentos de login

### Conflictos con constitución
✅ Ninguno - cumple principio #5 (determinismo)
```

## Paso 5: Plan Técnico

```bash
/sdd-plan
```

**Output generado (`specs/001-login/plan.md`):**
```markdown
# Plan 001 - Login Dofus

## Arquitectura de módulos
```
Cliente (Godot)          Servidor (Python)
┌─────────────┐          ┌──────────────┐
│ Auth UI     │◄────────►│ Auth Handler │
│ OAuth Flow  │          │ Session Mgr  │
│ Packet      │          │ Token Verify │
└─────────────┘          └──────────────┘
```

## Modelo de datos
```json
{
  "session": {
    "user_id": "string (UUID)",
    "token": "string (JWT)",
    "created_at": "ISO 8601",
    "expires_at": "ISO 8601"
  }
}
```

## Algoritmo principal (pseudocódigo)
```
ENTRAR: OAuth callback con code
  SI code válido:
    token <- exchangeCodeForToken(code)
    session <- createSession(token)
    DEVOLVER session.token
  SINO:
    LANZAR Error("Invalid OAuth code")
```

## Contrato de la CLI
| Comando | Entrada | Salida | Código error |
|---------|---------|--------|--------------|
| login oauth | <code> | <session_token> | 1 (error) |

## Decisiones técnicas
- **Usar JWT para sessions**: permite stateless verification, alternativa descartada: sessions en memoria (no scale)
- **Godot WebSocket instead HTTP**: menor latencia, alternativa descartada: polling (ineficiente)

## Cobertura de RF
| RF | Módulo | Test asociado |
|----|--------|---------------|
| RF-1 | Client/AuthUI | test_oauth_redirect |
| RF-2 | Server/AuthHandler | test_invalid_token |
| RF-3 | Server/SessionMgr | test_session_validity |
| RF-4 | Client/Packet | test_ticket_generation |
```

## Paso 6: Generar Tareas

```bash
/sdd-tasks
```

**Output generado (`specs/001-login/tasks.md`):**
```markdown
# Tareas — 001-login

- [ ] T1: Setup OAuth config en cliente
  - RF: RF-1
  - Hecho cuando: constants.py tiene OAuth URLs correctas
  - Archivos: client/config/oauth_config.gd

- [ ] T2: Implementar botón de login en UI
  - RF: RF-1
  - Hecho cuando: click en botón navega a URL OAuth
  - Archivos: client/ui/login_screen.gd

- [ ] T3: Manejar callback OAuth en servidor
  - RF: RF-1, RF-2
  - Hecho cuando: endpoint acepta code, devuelve error si inválido
  - Archivos: server/handlers/auth_handler.py

- [ ] T4: Validar token y crear session
  - RF: RF-3, RF-4
  - Hecho cuando: session creada con expiry correcto
  - Archivos: server/models/session.py

- [ ] T5: Enviar ticket al cliente
  - RF: RF-4
  - Hecho cuando: packet recibido, session guardada
  - Archivos: client/packets/session_packet.gd, server/packets/session.py

- [ ] T6: Tests unitarios completo
  - RF: todos
  - Hecho cuando: coverage > 80%, todos green
  - Archivos: test/client/test_oauth.gd, test/server/test_auth.py
```

## Paso 7: Implementar (TDD)

```bash
/sdd-implement T1
```

**Flujo ejecutado:**
1. Lee task T1
2. Escribe test primero (falla - rojo)
3. Implementa configuración básica (pasa - verde)
4. Ejecuta tests
5. Marca `[x] T1` en tasks.md

**Output:**
```
Hecho T1. Tests: 2 passed, 0 failed
RF cubierto: RF-1
¿Continuar con T2? [s/n]
```

## Paso 8: Validar

```bash
/sdd-validate
```

**Output generado (`specs/001-login/VALIDATION.md`):**
```markdown
# Validación — 001-login

## Recorrido RF por RF

| RF | Test | Resultado | Comentario |
|----|------|-----------|------------|
| RF-1 | test_oauth_redirect | ✅ PASA | redirect funciona |
| RF-2 | test_invalid_token | ✅ PASA | error correcto |
| RF-3 | test_session_validity | ✅ PASA | expiry OK |
| RF-4 | test_ticket_generation | ⚠️ FALLA | packet timeout |

## Cobertura
- RF cubiertos: 3/4
- Tests sin RF: test_config_setup
- RF sin test: ninguno

## Veredicto

❌ INCOMPLETA

**Razón:** RF-4 tiene test failing (packet timeout). Necesita fix antes de continuar.
```

---

## Resumen

En ~8 pasos has pasado de una idea vaga a código validado con:
- ✅ Especificación clara y acordada
- ✅ Plan técnico documentado
- ✅ Tareas pequeñas y verificables
- ✅ Tests pasando (con traceability RF→Test)
- ✅ Code review implícito via QA
- ✅ Definition of Done cumplida
