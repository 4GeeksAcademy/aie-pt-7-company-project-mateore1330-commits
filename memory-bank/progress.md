# Progress — Brasaland

> **Qué es este archivo:** dónde está el proyecto ahora. El agente lo lee al empezar cada sesión y lo
> actualiza al cerrar cada tarea con la skill `update-memory-bank`.

---

## Estado actual

- **Hito en curso:** Ingeniería impulsada por IA
  ([plan](../docs/plans/01-hito-ingenieria-impulsada-por-ia.md)).
- **Rama:** `feat/AGENTS-01-agent-memory-bank`.
- **Fase:** 1 de 5 — banco de memoria y contexto del dominio.

---

## Historial

### 2026-11-19 · `feat/AGENTS-01-agent-memory-bank`

- Plan del hito aprobado y guardado en `docs/plans/01-hito-ingenieria-impulsada-por-ia.md`.
- Creados `memory-bank/projectbrief.md`, `memory-bank/techContext.md` y `memory-bank/progress.md`.
- `CONTEXT.es.md` pasa a ser el diccionario del dominio y `CONTEXT.md` un puntero a él.

### Antes · `feat/company-choice` (PR #1, fusionado en `develop`)

- Añadidos `BRIEFING.md` (briefing de Brasaland) y `company-choice.md` (empresa elegida, áreas de interés,
  reto «Del precio del proveedor al menú» e idea del agente de márgenes).

---

## Próximos pasos

1. **Fase 2:** `AGENTS.md` (lectura inicial, flujo de 7 pasos antes del commit, archivos protegidos) y
   `CLAUDE.md`.
2. **Fase 3:** las 4 reglas de `.agents/rules/` y la skill `.agents/skills/update-memory-bank/`.
3. **Fase 4:** validar el flujo y la skill sobre este propio hito.
4. **Fase 5:** PR a `develop` y entrega del enlace en el campus.
5. **Hitos siguientes:** Web (`uis/website`), y después Backend, Workflows, RAG y Agentes.

---

## Riesgos y temas abiertos

- **Destino de los PR:** el enunciado pide el PR a `main`; Mateo lo abre a `develop`. Pendiente de preguntar
  al profesor.
- **Umbral de alerta de precios:** el 8 % es solo un ejemplo; está sin decidir.
- **Seguridad:** `.gitignore` vacío y sin gitleaks; se configura antes de la primera clave.
- **Stack de `uis/backoffice`:** sin decidir.
