# Progress — Brasaland

> **Qué es este archivo:** dónde está el proyecto ahora. El agente lo lee al empezar cada sesión y lo
> actualiza al cerrar cada tarea con la skill `update-memory-bank`.

---

## Estado actual

- **Hito en curso:** Ingeniería impulsada por IA
  ([plan](../docs/plans/01-hito-ingenieria-impulsada-por-ia.md)).
- **Rama:** `feat/AGENTS-01-agent-memory-bank`.
- **Fase:** 4 de 5 — validación terminada; falta la entrega (PR a `develop`).

---

## Historial

### 2026-11-19 · `feat/AGENTS-01-agent-memory-bank` (fases 2 a 4)

- Creados `AGENTS.md` (lectura inicial, flujo de 7 pasos antes del commit, archivos protegidos y cuándo
  parar y preguntar) y `CLAUDE.md` (`@AGENTS.md`).
- Creadas las 4 reglas de `.agents/rules/`: `monorepo-structure` (siempre activa), `brasaland-domain` y
  `fastapi-services` (por patrón) y `git-workflow` (bajo demanda).
- Creada la skill `.agents/skills/update-memory-bank/SKILL.md`.
- Validado el flujo de `AGENTS.md` sobre la rama: formato de rama correcto, archivos en su sitio, sin
  carpetas de app nuevas, sin `.env` ni secretos (gitleaks sin hallazgos). No hay tests ni lint todavía.
- Primera ejecución real de la skill `update-memory-bank` (esta entrada).

### 2026-11-19 · `feat/AGENTS-01-agent-memory-bank`

- Plan del hito aprobado y guardado en `docs/plans/01-hito-ingenieria-impulsada-por-ia.md`.
- Creados `memory-bank/projectbrief.md`, `memory-bank/techContext.md` y `memory-bank/progress.md`.
- `CONTEXT.es.md` pasa a ser el diccionario del dominio y `CONTEXT.md` un puntero a él.

### Antes · `feat/company-choice` (PR #1, fusionado en `develop`)

- Añadidos `BRIEFING.md` (briefing de Brasaland) y `company-choice.md` (empresa elegida, áreas de interés,
  reto «Del precio del proveedor al menú» e idea del agente de márgenes).

---

## Próximos pasos

1. **Fase 5:** subir la rama, abrir el PR a `develop` con un enlace a `AGENTS.md` y entregar la URL en el
   campus. Mateo fusiona cuando el profesor lo apruebe.
2. **Hitos siguientes:** Web (`uis/website`), y después Backend, Workflows, RAG y Agentes.

---

## Riesgos y temas abiertos

- **Destino de los PR:** el enunciado pide el PR a `main`; Mateo lo abre a `develop`. Pendiente de preguntar
  al profesor.
- **Umbral de alerta de precios:** el 8 % es solo un ejemplo; está sin decidir.
- **Seguridad:** `.gitignore` vacío y sin gitleaks; se configura antes de la primera clave.
- **Stack de `uis/backoffice`:** sin decidir.
- **Nota mínima de PageSpeed:** confirmar en el enunciado del hito de Web.
- **Sin tests ni lint:** el paso 3 del flujo de `AGENTS.md` no tiene nada que ejecutar hasta que haya código.
