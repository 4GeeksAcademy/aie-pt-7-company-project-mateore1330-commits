---
description: Mapa de carpetas del monorepo de Brasaland y dónde va cada cosa
alwaysApply: true
---

# Regla: estructura del monorepo

**Alcance:** siempre activa. Se aplica en todas las sesiones y a cualquier archivo.

## Mapa de carpetas

| Ruta | Qué va ahí |
|---|---|
| `uis/website` | Web pública de Brasaland (ruta `/`, marca y textos alineados con el briefing) |
| `uis/backoffice` | App interna, con su propio layout y separada de la web pública |
| `services/api` | API central FastAPI (locales, menús, ventas, clientes, proveedores) |
| `data/raw`, `data/pipelines`, `data/process`, `data/eval` | Datos crudos, pipelines, datos procesados y evaluación |
| `agents/`, `skills/`, `mcps/` | Producto de IA de Brasaland (p. ej. el agente de márgenes) |
| `workflows/` | Automatizaciones (n8n u otras) |
| `packages/shared/` | Tipos compartidos (`@repo/shared-types`) |
| `shared/` | Esquemas, plantillas y assets sueltos |
| `infra/`, `scripts/`, `internal/` | Despliegue, scripts puntuales y herramientas internas |
| `docs/` | Documentación transversal; los planes de hito van en `docs/plans/NN-hito-<nombre>.md` |
| `.agents/` | Configuración del agente de programación (reglas y skills de desarrollo) |
| `memory-bank/` | Contexto activo del proyecto para el agente |

## Qué hacer

1. **Antes de crear un archivo en una carpeta, lee su `README.es.md`** (o `README.md`).
2. **Cada app, servicio, agente o pipeline nuevo va en su propia subcarpeta con su `README.md`.**
3. **Usa la guía de la plantilla** si dudas: si tiene pantallas, va en `uis/`; si es una API o un proceso en
   segundo plano, va en `services/`; si mueve o transforma datos, va en `data/`; si el trabajo lo hace un
   modelo de IA, va en `agents/`.

## Qué no hacer

- **No crees árboles paralelos:** nada de `frontend/`, `web/`, `backend/`, `api/` o `src/` en la raíz, ni
  una segunda web fuera de `uis/website`, ni una segunda API fuera de `services/api`.
- **No mezcles `.agents/` con `agents/`:** `.agents/` ayuda a programar el repo; `agents/` es producto de
  Brasaland.
- **No dejes archivos sueltos en la raíz**, salvo los que ya están (`AGENTS.md`, `CLAUDE.md`, `CONTEXT*.md`,
  `BRIEFING.md`, `README*.md`, `company-choice.md`) y el futuro `docker-compose.yml`.
- **Si algo no encaja en el mapa, para y pregunta a Mateo** antes de crear la carpeta.
