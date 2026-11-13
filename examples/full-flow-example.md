# Full Flow Example: Implementing User Authentication

Ejemplo completo del flujo SDD usando el skill `/sdd-flow`.

## Escenario

Implementar un sistema de autenticación básica con login y logout.

## Paso 1: Invocar el Wizard

```bash
/sdd-flow "sistema de login y logout con sesiones"
```

### Interacción 1: Constitución

**Asistente:** ¿Qué stack tecnológico usarás?
**Usuario:** Node.js + Express + PostgreSQL

**Asistente:** ¿Cuál es el máximo número de dependencias?
**Usuario:** 5

**Asistente:** ¿Qué calidad mínima requieres?
**Usuario:** 100% de pruebas unitarias

### Output: docs/constitution.md

```markdown
# Constitución — Sistema de Autenticación

1. **Stack mínimo.** Node.js + Express + PostgreSQL (máx 5 dependencias). Ningún framework adicional sin justificación.
2. **Spec antes que código.** Todo RF debe tener spec.md aprobado antes de implementar.
3. **Separación lógica.** 3 capas: routes (HTTP), services (lógica), models (persistencia).
4. **Tests obligatorios.** Cobertura mínima 100% en services/. Tests escritos antes del código.
5. **Persistencia controlada.** Solo tablas users (id, email, password_hash, created_at). Migraciones SQL versionadas.
```

---

## Paso 2: Especificación (spec.md)

### Interacción 2: Generar Spec

**RF Generados:**

```markdown
# Spec 001 — Sistema de autenticación

## Contexto y objetivo
Permitir usuarios registrarse, iniciar sesión y cerrar sesión de forma segura con validación de credenciales y manejo de sesiones.

## Usuarios / actores
- Usuario registrado
- Sistema de autenticación

## Historias de usuario
- H1: Como usuario registrado, quiero iniciar sesión con email y contraseña, para acceder a la aplicación.
- H2: Como usuario, quiero cerrar sesión, para proteger mi cuenta en dispositivos compartidos.
- H3: Como usuario, quiero recuperar contraseña, para acceder sin contactar soporte.

## Requisitos funcionales (criterios de aceptación en EARS)
- RF-1: CUANDO el usuario visita /login, EL SISTEMA muestra formulario con campos email y contraseña.
- RF-2: SI el email no está registrado, ENTONCES EL SISTEMA muestra error "Email no encontrado".
- RF-3: MIENTRAS el usuario mantiene sesión activa, EL SISTEMA valida el token cada 5 minutos.
- RF-4: EL SISTEMA hashea contraseñas con bcrypt antes de guardarlas.

## Requisitos no funcionales (RNF)
- RNF-1: Tiempo de respuesta login < 2 segundos.
- RNF-2: Contraseñas almacenadas con bcrypt (12 rounds mínimo).

## Casos límite
- Email inválido (sin @)
- Contraseña vacía
- Múltiples intentos fallidos (bloqueo temporal)

## Fuera de alcance
- Login con Google/Facebook
- 2FA
- Recordar sesión persistente

## Criterios de finalización
Todos los RF con test unitario pasando + login manual funcional.

## Dudas abiertas
- [NECESITA ACLARACIÓN] ¿Debo validar email en el frontend o solo backend?
```

---

## Paso 3: QA automático

### Interacción 3: Clarify

**Detecciones automáticas:**

1. ✅ Historias en formato correcto
2. ✅ RF verificables (no adjectivos)
3. ✅ Casos límite definidos
4. ✅ Fuera de alcance explícito

**Notas QA agregadas:**

```markdown
## Notas QA (agregadas automáticamente)

### ✅ PASÓ: Historias de usuario
Formato INVEST correctamente aplicado.

### ✅ PASÓ: RF verificables  
Todos los RF usan notación EARS.

### ⚠️ RECOMENDADO: Casos límite
Agregar caso: "Usuario bloqueado por 5 intentos fallidos".
```

---

## Paso 4: Plan Técnico

### Interacción 4: Generar Plan

**Output: specs/001-auth/plan.md**

```markdown
# Plan 001 — Sistema de autenticación

## Arquitectura de módulos
```
routes/          → HTTP endpoints
  └── auth.routes.js
services/        → Lógica de negocio
  └── auth.service.js
models/          → Persistencia
  └── user.model.js
tests/           → Tests unitarios
  └── auth.service.test.js
```

## Modelo de datos 
```json
{
  "id": "UUID primary key",
  "email": "string unique, email válido",
  "password_hash": "string bcrypt hash",
  "created_at": "timestamp"
}
```

## Algoritmo principal (pseudocódigo)
```
LOGIN(email, password):
  user <- findUserByEmail(email)
  SI user es null:
    LANZAR Error("Email no encontrado")
  SI bcrypt.compare(password, user.password_hash) es false:
    LANZAR Error("Credenciales inválidas")
  token <- jwt.sign({userId: user.id}, SECRET)
  DEVOLVER {token, user.id}
```

## Contrato de la CLI
| Comando | Entrada | Salida | Código error |
|---------|---------|--------|--------------|
| POST /api/auth/login | {email, password} | {token, userId} | 401/200 |
| POST /api/auth/logout | token | null | 401/200 |
| POST /api/auth/recover | {email} | {message} | 404/200 |

## Decisiones técnicas
- Decisión 1: JWT para sesiones
  - Alternativa descartada: sesiones en Redis (overkill para MVP)
- Decisión 2: bcrypt para passwords
  - Alternativa descartada: scrypt (menos soporte en Node.js)

## Cobertura de RF
| RF | Módulo | Test asociado |
|----|--------|---------------|
| RF-1 | routes/auth.routes.js | test_login_form |
| RF-2 | services/auth.service.js | test_invalid_email |
| RF-3 | services/auth.service.js | test_session_refresh |
| RF-4 | services/auth.service.js | test_password_hash |
```

---

## Paso 5: Tareas

### Interacción 5: Generar Tasks

**Output: specs/001-auth/tasks.md**

```markdown
# Tareas — Sistema de autenticación

## T1 - Setup del proyecto ✅
- [x] Crear estructura de carpetas
- [x] Instalar dependencias (express, bcrypt, jsonwebtoken)
- [x] Configurar jest para tests

## T2 - Modelo de usuario
- [ ] Crear modelo User con validaciones
- [ ] Test: validar email único
- [ ] Test: hashear password al crear

## T3 - Service de autenticación
- [ ] Implementar login() con bcrypt.compare
- [ ] Test: manejar email no encontrado
- [ ] Test: manejar password incorrecto

## T4 - Routes de autenticación
- [ ] Crear endpoint POST /login
- [ ] Test: endpoint devuelve token válido
- [ ] Test: endpoint devuelve 401 en error

## T5 - Integración y QA
- [ ] Test e2e login completo
- [ ] Validar conftest.js
- [ ] Documentar endpoints en README
```

---

## Paso 6: Implementar con TDD

### Interacción 6: Implementar T2

```bash
/sdd-implement T2
```

**Proceso automático:**

1. Lee la tarea T2
2. Crea test vacío: `test_login_user.test.js`
3. Ejecuta test (FALLA)
4. Implementa código mínimo
5. Ejecuta test (PASA)
6. Marca T2 como completada

---

## Paso 7: Validación Final

```bash
/sdd-validate
```

**Output:**

```
📋 Verificación de cobertura RF→Test

✅ RF-1: test_login_form.test.js [PASA]
✅ RF-2: test_invalid_email.test.js [PASA]
✅ RF-3: test_session_refresh.test.js [PASA]
✅ RF-4: test_password_hash.test.js [PASA]

✅ Especificación cumplida
📊 Cobertura: 100% (services/)
```

---

## Resumen del Flujo

```
Idea → Constitution → Spec → Clarify → Plan → Tasks → Implement → Validate
  ↓         ↓          ↓        ↓       ↓       ↓          ↓         ↓
"sistema"  docs/       specs/    QA    specs/   specs/    código/   ✅
           .md         .md       notes  .md     .md       tests/   
```

## Próximos Pasos

1. **Iterar** sobre T3, T4, T5
2. **Desplegar** a staging
3. **Crear** specs para nuevas features