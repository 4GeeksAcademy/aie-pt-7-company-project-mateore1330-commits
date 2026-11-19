---
description: Ramas, commits y PR del repo de Brasaland. Úsala al crear una rama, hacer un commit o abrir un PR
alwaysApply: false
---

# Regla: flujo de git

**Alcance:** bajo demanda. Se aplica cuando el agente va a crear una rama, hacer un commit o abrir un PR.

## Ramas

- **Permanentes:** `main` (producción) y `develop` (integración).
- **De trabajo:** salen de `develop`, con el formato `tipo/CÓDIGO-descripcion` en kebab-case (p. ej.
  `feat/AGENTS-01-agent-memory-bank`, `fix/WEB-02-mobile-menu`).
- **Nunca** se hace un commit ni un push directo en `main` o `develop`.

## Commits

- **Conventional Commits en inglés:** `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`.
- **Sin coautor de Claude** ni líneas de atribución.
- Antes de cada commit se sigue el flujo de 7 pasos de [`AGENTS.md`](../../AGENTS.md).

## Pull requests

1. **PR de la rama de trabajo a `develop`.** Es la URL que se entrega en el campus de 4Geeks.
2. **Mateo revisa y fusiona.** El agente **no fusiona nunca**.
3. **PR de `develop` a `main` solo cuando Mateo lo pide**, tras validar las pruebas.
4. **Tras la fusión:** se borra la rama local con `git fetch --prune` y `git branch -d <rama>`.

> **Pendiente:** el enunciado de los hitos pide el PR directo a `main`. Mateo va a preguntar al profesor si
> puede seguir con este flujo. Si la respuesta cambia, se actualiza esta regla.
