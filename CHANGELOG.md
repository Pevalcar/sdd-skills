# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-11-17

### Added
- **Contexto compartido** en todas las skills core: bloque de metadatos que declara qué estados consume/produce y qué skills desbloquea
- **sdd-setup**: skill para detectar ausencia de AGENTS.md y docs/constitution.md y generar plantillas mínimas
- **sdd-discover**: meta-skill para análisis de proyecto, detección de perfil y enrutamiento al skill correcto usando información de `.sdd-state.json`

### Changed
- **Estandarización del flujo**: eliminación de `sdd-story` y `sdd-pair` del flujo core
- **Flujo simplificado**: `discover → constitution → backlog → spec → clarify → plan → review → tasks → implement → validate → variants`
- **Actualización de versiones**: todas las skills core pasan a `version: 1.0.0`
- **Actualización de `.sdd-state.json`**: esquema unificado con `clarification.status` simple (PASS/FAIL/PENDING)
- **Actualización de README.md**: badges actualizados a 11 skills, tabla de skills reflejando el nuevo flujo
- **Actualización de docs/SKILLS.md**: documentación actualizada con el nuevo número de skills
- **Atualización de .gitignore**: `.sdd-state.json` ahora es un archivo de ejemplo (comentado)

### Removed
- **`sdd-pair`**: eliminada - su funcionalidad está cubierta por `sdd-implement` con verificación humana por tarea
- **`sdd-story`**: eliminada - su funcionalidad está integrada en `sdd-backlog` y `sdd-spec`
- **Referencias a skills inexistentes** en `sdd-flow` (source-driven-development, incremental-implementation, etc.)

### Fixed
- **Inconsistencias de frontmatter**: todos los skills ahora tienen el mismo formato de frontmatter (name, description, version, disable-model-invocation)
- **Rutas de archivos inconsistentes**: estandarizado a `specs/NNN-<slug>/<artefacto>`
- **Estados de `.sdd-state.json` desalineados**: unificado esquema de estado entre todas las skills

## [2.0.0] - 2024-11-15

### Added
- **Perfiles adaptativos**: web-frontend, systems, game-dev, mobile, infrastructure
- **Skills core V2**: 13 skills con ASUMPTIONS, Rationalizations, Verification sections
- **Material de referencia**: skill-template.md, anti-rationalizations.md, verification-gates.md, definition-of-done.md
- **Flow V2 con sdd-variants**: fase obligatoria de exploración de variantes

### Changed
- **Arquitectura V2**: metroidvania de descubrimiento y routing automático
- **Verification gates**: checkpoints obligatorios entre fases con aprobación humana
- **Contexto compartido entre skills**: cada skill conoce su situación en el flujo