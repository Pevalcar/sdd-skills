# Instrucciones para Deploy a GitHub

Este script prepara la release V2.0.0 para GitHub.

## Paso 1: Verificar el estado del repo

```bash
git status
git log --oneline --graph -5
git tag -l
```

## Paso 2: Push al remote

```bash
# Push commits
git push origin main --follow-tags

# Si tienes la rama v2.0-release local
git push origin v2.0-release
```

## Paso 3: Crear GitHub Release (manual)

1. Ve a https://github.com/Pevalcar/sdd-skills/releases/new
2. Selecciona tag: v2.0.0
3. Título: "SDD Skills V2.0.0 - Adaptive Profiles"
4. Descripción: Copia el contenido del PR-README.md
5. Publica release

## Paso 4: Verificar

- [ ] GitHub Actions CI pasa
- [ ] Todos los checks verificados
- [ ] README mostrando badges correctos

---

## Comandos Git (ejecutar manualmente)

```bash
# Agregar cambios remotos si es necesario
git remote add origin https://github.com/Pevalcar/sdd-skills.git

# Push con tags
git push -u origin main --follow-tags

# Push de rama de release (opcional)
git push origin v2.0-release:refs/heads/v2.0-release
```

---

## Estado Actual

✅ Commit creado: `1924580 feat: Release SDD Skills V2...`
✅ Tag creado: `v2.0.0`
✅ Branch actual: `main`
✅ Archivos preparados: 33 archivos

## Próximos pasos del usuario

1. Ejecutar los comandos de push arriba
2. Crear GitHub Release
3. Verificar CI/CD
4. Celebrar el lanzamiento! 🎉