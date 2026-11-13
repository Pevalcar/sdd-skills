# Test de Descubrimiento — SDD Skills V2

## Escenario de Prueba

Vamos a simular un proyecto de ejemplo para probar el flujo de descubrimiento.

### Paso 1: Detectar perfil web-frontend

**Archivos en el proyecto:**
```
package.json
tsconfig.json
vite.config.ts
```

**Comando a ejecutar:**
```bash
/sdd-discover
```

**Output esperado:**
```json
{
  "detected_profile": "web-frontend",
  "reason": " encontrados package.json y tsconfig.json",
  "skills_applicable": ["sdd-constitution", "sdd-spec", "sdd-plan", "sdd-tasks", "sdd-implement", "sdd-validate"],
  "recommendation": "/sdd-constitution"
}
```

### Paso 2: Detectar perfil systems (Rust)

**Archivos en el proyecto:**
```
Cargo.toml
Cargo.lock
src/main.rs
```

**Output esperado:**
```json
{
  "detected_profile": "systems",
  "reason": " encontrado Cargo.toml",
  "skills_applicable": ["sdd-constitution", "sdd-spec", "sdd-plan", "sdd-tasks", "sdd-implement", "sdd-validate"],
  "recommendation": "/sdd-constitution"
}
```

### Paso 3: Estado de proyecto con constitution existente

**Archivos en el proyecto:**
```
docs/constitution.md  (existente)
package.json
tsconfig.json
```

**Output esperado:**
```json
{
  "detected_profile": "web-frontend",
  "state": {
    "constitution": "✓ exists",
    "spec": "✗ missing",
    "plan": "✗ missing",
    "tasks": "✗ missing"
  },
  "recommendation": "/sdd-spec"
}
```

## Validación del Sistema

### ✅ Skills instaladas
- Todos los 9 skills deben estar disponibles en `/sdd-*`

### ✅ Perfiles funcionales
- web-frontend: Detecta package.json + tsconfig.json
- systems: Detecta Cargo.toml + go.mod + pyproject.toml
- game-dev: Detecta project.godot
- mobile: Detecta pubspec.yaml + Podfile
- infrastructure: Detecta Dockerfile + .github/workflows/

### ✅ Referencias aplicables
- skill-template.md sigue estructura V2
- anti-rationalizations.md cubre todos los perfiles
- verification-gates.md tiene checklist por fase
- definition-of-done.md es universal

## Comandos de Verificación

### Verificar skill registration
```bash
npx skills ls | grep sdd
```

### Verificar perfiles
```bash
ls -la profiles/*/SKILL.md
ls -la references/*.md
```

### Verificar estado
```bash
cat .sdd-state.json | python -m json.tool
```

---

## 🎯 Test Completo

Para probar todo el flujo con un proyecto real:

1. **Crear proyecto de ejemplo:**
```bash
mkdir test-project && cd test-project
echo '{"name": "test"} > package.json'
echo '{}' > tsconfig.json
```

2. **Ejecutar discover:**
```bash
/sdd-discover
```

3. **Verificar salida:**
- Perfil web-frontend detectado
- Skills recomendados mostrarán constitution primero

4. **Limpiar:**
```bash
rm -rf test-project
```

---

**✅ Test Ready: Verificar funcionalidad con /sdd-discover**