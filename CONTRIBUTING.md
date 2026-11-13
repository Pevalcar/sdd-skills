# Contributing to SDD Skills

¡Gracias por tu interés en contribuir! Esta guía te ayuda a mantener la calidad y consistencia del proyecto.

## 📋 Reglas del Proyecto

### 1. Estructura de Carpetas

Cada skill debe seguir esta estructura:

```
sdd-nombre/
├── SKILL.md        # Instrucciones principales (frontmatter + contenido)
├── README.md       # Ayuda y uso (puede incluir ejemplos)
└── <template>.md   # Plantilla de output (cuando aplica)
```

### 2. Formato de SKILL.md

```markdown
---
name: sdd-nombre
description: Descripción clara y concisa.
disable-model-invocation: true  # Si aplica
---

# Título del skill

Descripción del skill...

## Proceso

1. Paso uno...
2. Paso dos...
```

### 3. Convenciones de Nombres

- **Skills**: `sdd-nombre` (lowercase con guiones)
- **Templates**: `<concepto>-template.md`
- **Variables**: camelCase en pseudocódigo
- **RF**: RF-1, RF-2, etc. en mayúsculas

### 4. Calidad de Código

- Usa comillas angulares para referencias: `specs/`
- Backticks para código y comandos: `/sdd-flow`
- Guillemets para citas: «texto»
- UTF-8 con acentos correctos

## 🚀 Cómo Contribuir

### 1. Fork del repositorio

```bash
git clone https://github.com/tu-usuario/sdd-skills.git
cd sdd-skills
git checkout -b feature/nombre-de-tu-cambio
```

### 2. Crear/Editar una skill

1. Crea una nueva carpeta `sdd-nombre/`
2. Añade los archivos necesarios (SKILL.md, README.md, template)
3. Sigue el patrón de skills existentes

### 3. Commits

- Mensaje claro y descriptivo
- Usa formato convencional: `feat:`, `fix:`, `docs:`, etc.
- Referencia issues: `fix:#12 agregar validación`

```bash
git add .
git commit -m "feat: agregar skill sdd-examples"
```

### 4. Pull Request

1. Push a tu fork
2. Crea PR con descripción clara
3. Menciona si hay cambios rotundos

## 🔍 QA Checklist

Antes de hacer PR, verifica:

- [ ] No hay backticks sin cerrar
- [ ] Acentos correctos (UTF-8)
- [ ] Comas en historias: "Como <rol>, quiero <acción>, para <beneficio>"
- [ ] Rutas correctas: `.opencode/skills/`
- [ ] Plantillas sincronizadas con SKILL.md
- [ ] Ejemplos funcionales

## 🤝 Problemas Comunes (FAQ)

**Q: ¿Cómo agregar una nueva skill?**
A: Copia la estructura de una skill existente y adapta.

**Q: ¿Cómo actualizar templates?**
A: Asegúrate de que coincidan con las instrucciones en SKILL.md.

**Q: ¿Qué pasa si rompo algo?**
A: Usa feature branches y tests. Revisa por QA antes de merge.

## 📚 Recursos

- [Hola AI Concepts](https://github.com/nschurmann/hola-ai)
- [OpenCode Skills](https://github.com/opencode-ai/opencode)
- [Spec-Driven Development](./docs/architecture.md)