# Contributing to SDD Skills V2

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

Los perfiles van en:

```
profiles/
├── web-frontend/
│   └── SKILL.md
├── systems/
│   └── SKILL.md
└── <perfil>/
    └── SKILL.md
```

### 2. Formato de SKILL.md - REQUERIDO V2

```markdown
---
name: sdd-nombre
description: "Descripción clara y concisa."
disable-model-invocation: true  # Si aplica
---

# Título del skill

Descripción del skill...

## 🛡️ ASUMPTIONS I'M MAKING:

1. [suposición explícita]
2. [suposición explícita]
3. [suposición explícita]
→ Correct me now or I'll proceed.

## When to Use

- [cuándo usar]

## When NOT to Use

- [cuándo NO usar]

## Process

1. Paso uno...
2. Paso dos...

## Rationalizations

| Excusa | Realidad | Regla |
|--------|----------|-------|
| ... | ... | ... |

## Verification

- [ ] Checklist de verificación

## See Also

- [[skill_relacionada]]
```

### 3. Convenciones de Nombres

- **Skills**: `sdd-nombre` (lowercase con guiones)
- **Templates**: `<concepto>-template.md`
- **Variables**: camelCase en pseudocódigo
- **RF**: RF-1, RF-2, etc. en mayúsculas
- **Tasks**: T1, T2, Tn

### 4. Calidad de Código

- Usa comillas angulares para referencias: `specs/`
- Backticks para código y comandos: `/sdd-flow`
- Guillemets para citas: «texto»
- UTF-8 con acentos correctos

### 5. Perfiles Adaptativos

Cada skill puede cargar reglas específicas del perfil detectado. Busca en `profiles/<perfil>/SKILL.md`:

- **web-frontend**: TypeScript strict, a11y, bundle size
- **systems**: Error handling, memory safety, zero-warnings
- **game-dev**: Determinismo, state machines, netcode sync
- **mobile**: Lifecycle, memory leaks, platform parity
- **infrastructure**: IaC, security-first, immutability

## 🚀 Cómo Contribuir

### 1. Fork del repositorio

```bash
git clone https://github.com/tu-usuario/sdd-skills.git
cd sdd-skills
git checkout -b feature/nombre-de-tu-cambio
```

### 2. Crear/Editar una skill

1. Copia `references/skill-template.md` a `skills/sdd-nombre/`
2. Añade los archivos necesarios (SKILL.md, README.md, template)
3. Sigue el patrón V2 con ASUMPTIONS, Rationalizations, Verification

### 3. Crear un nuevo perfil

1. Crea `profiles/<nombre>/SKILL.md`
2. Define reglas específicas del dominio
3. Lista commands específicos
4. Agrega anti-patterns propios

### 4. Commits

- Mensaje claro y descriptivo
- Usa formato convencional: `feat:`, `fix:`, `docs:`, etc.
- Referencia issues: `fix:#12 agregar validación`

```bash
git add .
git commit -m "feat: agregar skill sdd-examples"
```

### 5. Pull Request

1. Push a tu fork
2. Crea PR con descripción clara
3. Menciona si hay cambios rotundos

## 🔍 QA Checklist V2

Antes de hacer PR, verifica:

- [ ] SKILL.md tiene ASUMPTIONS section
- [ ] Tabla de Rationalizations presente
- [ ] Verification checklist objectivo
- [ ] Cuando aplicable, See Also section
- [ ] No hay backticks sin cerrar
- [ ] Acentos correctos (UTF-8)
- [ ] Comas en historias: "Como <rol>, quiero <acción>, para <beneficio>"
- [ ] Rutas correctas: `profiles/` y `references/`
- [ ] Plantillas sincronizadas con SKILL.md
- [ ] Ejemplos funcionales

## 🤝 Problemas Comunes (FAQ)

**Q: ¿Cómo agregar una nueva skill?**
A: Copia `references/skill-template.md` y sigue el patrón V2.

**Q: ¿Cómo agregar un nuevo perfil?**
A: Crea `profiles/<nombre>/SKILL.md` siguiendo el template de los existentes.

**Q: ¿Qué pasa si rompo algo?**
A: Usa feature branches y tests. Revisa por QA antes de merge.

**Q: ¿Cómo actualizar skills-lock.json?**
A: Añade la skill al array `skills` con name, path, installed_at (null si nuevo).

## 📚 Recursos

- [Arquitectura V2](./docs/architecture.md)
- [Skills Catalog](./docs/SKILLS.md)
- [Quick Start](./examples/quick-start.md)
- [Full Flow Example](./examples/full-flow-example.md)
- [Hola AI Concepts](https://github.com/nschurmann/hola-ai)
- [OpenCode Skills](https://github.com/opencode-ai/opencode)