# Test de Instalación Rápida

## Paso 1: Verificar estructura

```bash
cd sdd-skills
ls -la
```

Debería mostrar:
- `README.md`
- `CONTRIBUTINGING.md`
- `LICENSE`
- `skills-lock.json`
- `package.json`
- `docs/`
- `examples/`
- `skills/`

## Paso 2: Instalar skills (en proyecto destino)

```bash
# En tu proyecto OpenCode
npx skills add /ruta/a/sdd-skills/skills/sdd-*
```

## Paso 3: Verificar instalación

```bash
npx skills ls | grep sdd
```

Salida esperada:
```
sdd-constitution
sdd-spec
sdd-clarify
sdd-plan
sdd-tasks
sdd-implement
sdd-validate
sdd-flow
```

## Paso 4: Probar una skill

```bash
/sdd-constitution
```

Debería preguntar por:
- Stack tecnológico
- Calidad requerida
- Pruebas obligatorias
- Límites del proyecto

## Paso 5: Probar workflow completo

```bash
/sdd-flow "funcionalidad: login Dofus"
```

El wizard debería crear:
- `docs/constitution.md`
- `specs/001-xxx/spec.md`
- `specs/001-xxx/plan.md`
- `specs/001-xxx/tasks.md`

## Solución de Problemas

### Error: "Skill no encontrada"
- Verifica que la skill esté en `skills/`
- Ejecuta `npx skills experimental_install`

### Error: "Template no encontrado"
- Asegúrate de que el template.md esté dentro de la carpeta de la skill

### Error: "Permisos denegados"
- En Windows: ejecuta PowerShell como administrador
- En Linux: `chmod +x` en scripts