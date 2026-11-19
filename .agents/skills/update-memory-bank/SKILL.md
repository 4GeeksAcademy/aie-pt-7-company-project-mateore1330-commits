---
name: update-memory-bank
description: Deja memory-bank/ al día al cerrar una tarea. Úsala en el paso 5 del flujo antes del commit de AGENTS.md, o cuando Mateo pida actualizar la memoria del proyecto.
---

# Skill: `update-memory-bank`

## Objetivo

**Dejar `memory-bank/` al día al cerrar una tarea**, para que la siguiente sesión del agente sepa qué se ha
hecho, qué se decidió y qué toca después. Nada más: esta skill no escribe código ni toca otros archivos.

## Cuándo se usa

- En el **paso 5** del flujo antes del commit de [`AGENTS.md`](../../../AGENTS.md).
- Cuando Mateo pide actualizar la memoria del proyecto.

## Inputs

| Input | Obligatorio | Ejemplo |
|---|---|---|
| **Resumen de la tarea** | Sí | «Creada la página de inicio de `uis/website`» |
| **Archivos creados o cambiados** | Sí | `uis/website/index.html`, `uis/website/README.md` |
| **Rama de trabajo** | Sí | `feat/WEB-01-home` |
| **Próximos pasos** | Sí | «Formulario de `application.html`» |
| **Decisiones técnicas tomadas** | Solo si las hay | «Tailwind con la CLI en vez de por CDN, por PageSpeed» |

Si falta un input obligatorio, **se pide a Mateo**; no se deduce. La rama y los archivos se pueden sacar de
`git branch --show-current` y `git status` / `git diff --staged --stat`.

## Pasos

1. **Reúne los inputs.** Comprueba la rama y los archivos con git.
2. **Lee** `memory-bank/progress.md` y `memory-bank/techContext.md` tal y como están.
3. **Actualiza `progress.md`:**
   - En «Estado actual», ajusta el hito, la rama y la fase.
   - En «Historial», añade **arriba** una entrada nueva con el título `### AAAA-MM-DD · <rama>` y una viñeta
     por cada cosa hecha.
   - En «Próximos pasos», quita lo que ya está hecho y añade lo nuevo.
   - En «Riesgos y temas abiertos», quita lo resuelto y añade lo que haya aparecido.
4. **Si hubo decisiones técnicas, actualiza `techContext.md`:** una fila nueva por decisión en la tabla de
   «Decisiones técnicas» (fecha, decisión y motivo). Si la decisión cambia el stack o el mapa de carpetas,
   actualiza también esa sección.
5. **Comprueba los criterios de aceptación** de abajo y enséñale a Mateo el diff de `memory-bank/`.

## Salida

- `memory-bank/progress.md` actualizado.
- `memory-bank/techContext.md` actualizado, solo si hubo decisiones.
- Un resumen para Mateo con los criterios marcados.

## Criterios de aceptación

Cada uno se comprueba antes de dar la skill por terminada:

- [ ] `progress.md` tiene una entrada nueva en «Historial» con fecha en formato `AAAA-MM-DD` y el nombre de
      la rama.
- [ ] La sección «Próximos pasos» de `progress.md` refleja el estado real: no queda ningún paso que ya esté
      hecho.
- [ ] Si hubo una decisión técnica, hay una fila nueva en la tabla de decisiones de `techContext.md`, con
      fecha y motivo.
- [ ] No se ha tocado ningún archivo fuera de `memory-bank/`, ni tampoco `memory-bank/projectbrief.md`.
      Se comprueba con `git status --short`.
- [ ] No hay datos inventados: todo lo escrito sale de los inputs o del repo.
