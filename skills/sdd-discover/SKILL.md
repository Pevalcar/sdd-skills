---
name: sdd-discover
description: "Meta-skill que analiza el proyecto y rutea al skill apropiado según el dominio detectado."
disable-model-invocation: true
---

# Descubridor SDD — Enrutamiento cognitivo

Analiza el repositorio para detectar perfil tecnológico y ruta al skill correcto.

## 🛡️ ASUMPTIONS I'M MAKING:

1. El proyecto tiene un directorio de trabajo actual (`pwd`)
2. Hay archivos de configuración que indican el stack (package.json, Cargo.toml, etc.)
3. El usuario necesita determinar qué skill usar primero

→ Correct me now or I'll proceed.

## Pasos

1. **Escanea el repositorio.** Busca archivos de configuración para identificar el perfil:
   - `package.json`, `tsconfig.json` → Web/Fullstack
   - `Cargo.toml`, `go.mod`, `pyproject.toml` → Systems
   - `project.godot`, `.godot/` → Game Dev
   - `pubspec.yaml`, `Podfile`, `build.gradle` → Mobile
   - `Dockerfile`, `docker-compose.yml` → Infrastructure

2. **Determina perfiles activos.** Un proyecto puede tener múltiples perfiles (ej. Godot + Python backend).

3. **Carga reglas del perfil.** Lee los archivos en `profiles/<nombre>/SKILL.md` correspondientes.

4. **Rutea al skill inicial.** Sugiere el primer skill basado en el estado del proyecto:
   - No existe `constitution.md` → `/sdd-constitution`
   - Existe constitution pero no spec → `/sdd-spec`
   - Ya hay spec pero falta plan → `/sdd-plan`
   - Ya hay plan pero faltan tareas → `/sdd-tasks`
   - Ya hay tasks pero faltan implementar → `/sdd-implement`
   - Terminada implementación → `/sdd-validate`

5. **Resume flujo existente.** Si existe `.sdd-state.json`, recuperar última fase y continuar desde ahí.

## Matriz de Perfiles

| Perfil | Archivos detectados | Skills adicionales | Validación específica |
|--------|---------------------|-------------------|----------------------|
| **web-frontend** | package.json, tsconfig.json | TypeScript patterns, SSR rules | type-check, jest tests |
| **systems** | Cargo.toml, go.mod, pyproject.toml | Concurrency rules, memory safety | cargo check, go vet, mypy |
| **game-dev** | project.godot, .godot/ | Determinismo, physics, render loop | headless tests, frame timing |
| **mobile** | pubspec.yaml, Podfile, build.gradle | Lifecycle management | native build, unit tests |
| **infrastructure** | Dockerfile, docker-compose.yml | Deploy security, IaC patterns | container scan, fmt validation |

## Output Inicial

Muestra al usuario:

```
🔍 Perfil detectado: [web-frontend]
📁 Stack: Node.js 20, React 18, TypeScript

📋 Estado actual del proyecto:
  ✓ constitution.md existe
  ✗ spec.md no existe
  ✗ plan.md no existe
  ✗ tasks.md no existe
  ✗ Tests no ejecutados

💡 Skill recomendado: /sdd-spec
   Razón: Tienes constitución pero necesitas especificar primero.

¿Continuar? [s/n]
```

## Control del Flujo

Comandos disponibles:

| Comando | Acción |
|---------|--------|
| `/sdd-discover` | Ejecutar análisis completo |
| `/sdd-discover resume` | Continuar desde último paso |
| `/sdd-discover status` | Mostrar estado actual |
| `/sdd-discover force <skill>` | Forzar skill específico |

## Reglas

- **Un solo perfil dominante** si hay conflicto, listar ambos y preguntar
- **Nunca asumir stack** sin evidencia en archivos de configuración
- **Preservar estado** en `.sdd-state.json` entre sesiones
- **Documentar decisiones** de routing en el output

## Verification

Antes de dar por terminado el descubrimiento:

- [ ] Se detectaron correctamente los archivos de configuración
- [ ] El perfil coincide con el stack real del proyecto
- [ ] La recomendación de skill siguiente es clara
- [ ] El usuario entendió el flujo sugerido
