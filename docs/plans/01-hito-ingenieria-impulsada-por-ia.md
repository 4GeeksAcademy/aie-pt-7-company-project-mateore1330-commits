# Plan — Hito: Ingeniería impulsada por IA

> **Estado:** ✅ aprobado por Mateo (2026-11-19). Implementación pendiente; se empieza en una sesión nueva.
> **Fecha:** 2026-11-19
> **Empresa:** Brasaland
> **Enunciado:** [Hito — Ingeniería impulsada por IA](https://learn.4geeks.com/es/main-cohort/spain-aie-pt-7/syllabus/working-with-ai-coding-agents-v3/project/ai-eng-milestone-ai-driven-engineering?moduleId=4)

---

## 1. Qué pide el hito

Preparar el monorepo de Brasaland para que un agente de IA de programación (Claude Code, Cursor…) trabaje
en él sin cometer errores. **No se crea ninguna app**: se construye el contexto y las reglas del agente.

### Entregables obligatorios

- [ ] `memory-bank/` con, como mínimo, `projectbrief.md`, `techContext.md` y `progress.md`.
- [ ] `AGENTS.md` en la raíz con:
  - los archivos del banco de memoria que el agente lee al empezar cada sesión;
  - el flujo obligatorio antes de cada commit (**mínimo 4 pasos ordenados**);
  - las carpetas y archivos que el agente **no modifica** sin confirmación explícita.
- [ ] `.agents/rules/` con al menos una regla con su **alcance explícito** (siempre activa, por patrón de
  archivo o bajo demanda).
- [ ] Al menos una skill en `.agents/skills/<skill>/SKILL.md` con objetivo único, inputs documentados y
  criterios de aceptación verificables.
- [ ] Dejar claro dónde van `uis/website`, `uis/backoffice` y `services/`, sin carpetas paralelas.

### Criterios de evaluación

1. El banco de memoria tiene contexto de negocio **y** contexto técnico.
2. `AGENTS.md` define un flujo de al menos 4 pasos ordenados antes del commit.
3. `.agents/` contiene al menos una regla con alcance explícito.
4. La skill tiene objetivo único, inputs documentados y criterios de aceptación verificables.
5. Queda claro dónde encajan `uis/website`, `uis/backoffice` y `services/`.

> ⚠ Todo debe estar alineado con el `BRIEFING.md` de Brasaland. Una infraestructura genérica no se acepta.

> ⚠ `.agents/` (configuración del agente de programación) **no es lo mismo** que `agents/` y `skills/`
> (producto de IA de la empresa que se construirá en hitos posteriores).

---

## 2. Decisiones tomadas

| Tema | Decisión | Motivo |
|---|---|---|
| Rama | `feat/AGENTS-01-agent-memory-bank` | Convención `tipo/CÓDIGO-descripcion` (el enunciado pide `feature/agent-memory-bank`; se considera equivalente) |
| Destino del PR | `develop` (git flow habitual: rama de trabajo → `develop` → `main`) | El enunciado pide el PR a `main`, pero Mateo mantiene su flujo. La URL del PR a `develop` es la que se entrega; se fusiona cuando el profesor lo apruebe. **Pendiente:** preguntar al profesor si puede seguir así o si debe hacer los PR directos a `main` |
| Issue / Project | Sin issue | Es un ejercicio del bootcamp; el repo está en la organización de 4Geeks |
| Idioma | Español en toda la documentación; nombres de archivo y de campo en inglés | Reglas globales de Mateo |
| Backend | FastAPI: una sola app en `services/api` con routers por dominio | Lo recomienda la plantilla. Desviación anotada respecto al stack por defecto (Flask) |
| `uis/website` | HTML5 semántico + Tailwind + JavaScript, **decisión revisable** | Encaja con la estructura y el comando del hito de Web (`index.html`, `application.html`, `validation.js`, `npx http-server`). Si un hito posterior pide Next.js, se migra |
| `uis/backoffice` | Pendiente | Se decide en su hito |
| Estilos | Solo Tailwind, sin CSS a mano | Lo pide el hito de Web. Desviación anotada respecto al stack por defecto (CSS Modules) |
| Skill | `update-memory-bank` | El enunciado insiste en mantener la memoria al día; los criterios son verificables |
| Reglas | 4 reglas (ver punto 3) | Cubren estructura, dominio, backend y git |
| Banco de memoria | Solo los 3 archivos obligatorios | Menos archivos que mantener |
| `CONTEXT.md` | Se rellena en este hito con el diccionario del dominio, procesado y no copiado | Lo pide la plantilla («no copies y pegues, procésalo») |
| `CLAUDE.md` | Sí, una línea: `@AGENTS.md` | Claude Code no lee `AGENTS.md` por sí solo |
| Planes de hito | `docs/plans/NN-hito-<nombre>.md`, incluidos en el PR | `docs/` es la carpeta de documentación global de la plantilla |
| Seguridad (`.gitignore`, gitleaks) | **Fuera de este hito** | No lo pide la tarea. Se retoma cuando aparezcan claves |

---

## 3. Archivos que se crean

| # | Archivo | Contenido |
|---|---|---|
| 0 | `docs/plans/01-hito-ingenieria-impulsada-por-ia.md` | Este plan |
| 1 | `memory-bank/projectbrief.md` | Brasaland: historia, mercados (Colombia y Florida), 14 locales, unas 115 personas, áreas y sus responsables, problemas por departamento, equipo Brasaland Digital y reto elegido «Del precio del proveedor al menú» (agente de márgenes) |
| 2 | `memory-bank/techContext.md` | Estado tecnológico actual de Brasaland (web estática, app obsoleta, POS distinto por país, hojas de cálculo, sin API ni telemetría); stack por fases; mapa de carpetas; restricciones (dos países, COP/USD, ES/EN); tabla de decisiones; riesgo: Tailwind por CDN y la nota de PageSpeed (≥ 80) |
| 3 | `memory-bank/progress.md` | Hecho: elección de empresa e hito actual. Próximos pasos: hito de Web y siguientes. Riesgos y temas abiertos |
| 4 | `CONTEXT.es.md` | Diccionario del dominio: entidades con nombre en inglés (`location`, `supplier`, `invoice`, `dish`, `recipe`, `customer`…), valores fijos (mercados `CO` / `US-FL`, monedas `COP` / `USD`, idiomas `es` / `en`), restricciones de negocio |
| 5 | `CONTEXT.md` | Puntero corto a `CONTEXT.es.md` |
| 6 | `AGENTS.md` | Lectura inicial, flujo antes del commit, archivos protegidos y cuándo parar y preguntar |
| 7 | `CLAUDE.md` | `@AGENTS.md` |
| 8 | `.agents/rules/monorepo-structure.md` | **Siempre activa** |
| 9 | `.agents/rules/brasaland-domain.md` | **Por patrón**: `uis/**`, `services/**`, `packages/**`, `data/**` |
| 10 | `.agents/rules/fastapi-services.md` | **Por patrón**: `services/**` |
| 11 | `.agents/rules/git-workflow.md` | **Bajo demanda** |
| 12 | `.agents/skills/update-memory-bank/SKILL.md` | La skill |

### Mapa de carpetas que queda documentado

| Ruta | Qué va ahí |
|---|---|
| `uis/website` | Web pública de Brasaland (ruta `/`, marca y textos alineados con el briefing) |
| `uis/backoffice` | App interna, con su propio layout y separada de la web pública |
| `services/api` | API central FastAPI (locales, menús, ventas, clientes, proveedores) |
| `agents/`, `skills/`, `mcps/` | Producto de IA de Brasaland (p. ej. el agente de márgenes), en hitos posteriores |
| `.agents/` | Configuración del agente de programación: reglas y skills de desarrollo |
| `memory-bank/` | Contexto activo del proyecto para el agente |
| `docs/plans/` | Planes de cada hito |

---

## 4. Contenido de `AGENTS.md`

### Lectura al empezar cada sesión

1. `memory-bank/projectbrief.md`
2. `memory-bank/techContext.md`
3. `memory-bank/progress.md`
4. `CONTEXT.es.md`
5. Las reglas de `.agents/rules/` que apliquen a los archivos que se van a tocar

### Flujo obligatorio antes de cada commit

1. **Comprobar la rama:** con formato `tipo/CÓDIGO-descripcion`; nunca `main` ni `develop`.
2. **Comprobar la ubicación:** cada archivo nuevo está en su carpeta según `monorepo-structure`.
3. **Pasar los tests y el lint** que existan para la parte tocada.
4. **Revisar el diff:** sin `.env`, sin secretos y sin datos reales de clientes ni facturas de proveedores.
5. **Ejecutar la skill `update-memory-bank`.**
6. **Hacer el commit:** Conventional Commits en inglés, sin coautor de Claude.
7. **Abrir el PR a `develop`.** Mateo revisa y fusiona; el agente no fusiona. El paso de `develop` a `main`
   lo hace solo Mateo, con otro PR.

### No se modifica sin confirmación explícita de Mateo

- `BRIEFING.md`, `CONTEXT.md`, `CONTEXT.es.md`
- `AGENTS.md`, `CLAUDE.md`, `.agents/`
- `memory-bank/projectbrief.md`
- Los `README.md` / `README.es.md` de la plantilla, `.devcontainer/`, `.gitignore`, `packages/shared/types/`
- Las ramas `main` y `develop` (sin push directo)

### Cuándo parar y preguntar

- Falta un dato: **no se inventa**.
- Habría que crear una carpeta que no está en el mapa.
- Una decisión técnica contradice `techContext.md`.

---

## 5. Las reglas de `.agents/rules/`

Cada regla lleva el alcance en el frontmatter (`alwaysApply`, `globs` o `description`) y una línea
«**Alcance:**» al principio del texto.

| Regla | Alcance | Contenido |
|---|---|---|
| `monorepo-structure` | Siempre activa | Mapa de carpetas; `.agents/` frente a `agents/`; leer el README de cada carpeta antes de crear nada; no crear árboles paralelos de frontend o API; los planes van en `docs/plans/` |
| `brasaland-domain` | `uis/**`, `services/**`, `packages/**`, `data/**` | Todo importe lleva su moneda (`COP` / `USD`); todo dato lleva su mercado (`CO` / `US-FL`); nombres de `CONTEXT.es.md`; textos ES/EN; nada de datos reales de clientes ni de facturas |
| `fastapi-services` | `services/**` | Una sola app FastAPI con routers por dominio; un worker aparte solo si es imprescindible; sin microservicios por ahora |
| `git-workflow` | Bajo demanda (al hacer commit o PR) | Ramas `tipo/CÓDIGO-descripcion`; Conventional Commits en inglés; sin coautor; PR de la rama de trabajo a `develop` y de `develop` a `main` solo cuando Mateo lo pide; Mateo fusiona |

---

## 6. La skill `update-memory-bank`

- **Objetivo único:** dejar `memory-bank/` al día al cerrar una tarea.
- **Cuándo se usa:** paso 5 del flujo antes del commit de `AGENTS.md`.
- **Inputs:**
  - resumen de la tarea hecha;
  - archivos creados o cambiados;
  - decisiones técnicas tomadas (si las hay);
  - próximos pasos;
  - rama de trabajo.
- **Salida:** `progress.md` actualizado y, si hubo decisiones, `techContext.md` también.
- **Criterios de aceptación verificables:**
  - [ ] `progress.md` tiene una entrada nueva con fecha (AAAA-MM-DD) y rama.
  - [ ] La sección «Próximos pasos» de `progress.md` refleja el estado real.
  - [ ] Si hubo una decisión, hay una fila nueva en la tabla de decisiones de `techContext.md`.
  - [ ] No se ha tocado ningún archivo fuera de `memory-bank/`, y tampoco `projectbrief.md`.
  - [ ] Ningún dato inventado: todo sale de los inputs o del repo.

---

## 7. Lo que queda fuera

- Crear apps (`uis/website`, `uis/backoffice`, `services/api`): solo se documentan.
- `.gitignore`, `.env.example` y el hook de gitleaks.
- Issue y GitHub Project.
- Modificar `BRIEFING.md`.

---

## 8. Fases de implementación

Cada fase termina con una **revisión de Mateo**. No se pasa a la siguiente sin su visto bueno.

### Fase 0 — Preparación

1. Comprobar que `develop` está al día (`git fetch` y `git status`).
2. Crear la rama `feat/AGENTS-01-agent-memory-bank` desde `develop` (este plan, todavía sin commit, viaja
   con el cambio de rama).
3. Commit: `docs: add milestone plan`.

**Revisión de Mateo:** rama creada y plan subido.

### Fase 1 — Banco de memoria y contexto del dominio

1. Releer `BRIEFING.md` y `company-choice.md` como fuente única de los datos.
2. Escribir `memory-bank/projectbrief.md` (negocio, departamentos, problemas, reto elegido).
3. Escribir `memory-bank/techContext.md` (estado actual, stack por fases, mapa de carpetas, restricciones,
   tabla de decisiones, riesgos).
4. Escribir `memory-bank/progress.md` (hecho, en curso, próximos pasos, riesgos abiertos).
5. Escribir `CONTEXT.es.md` (diccionario del dominio) y sustituir `CONTEXT.md` por un puntero.
6. Comprobar que cada dato aparece en `BRIEFING.md` o en `company-choice.md`; lo que no esté ahí se pregunta.
7. Commit: `docs: add memory bank and domain context`.

**Revisión de Mateo:** que el contexto de negocio y el técnico sean correctos y sin datos inventados.

### Fase 2 — Protocolo del agente

1. Escribir `AGENTS.md`: lectura inicial, flujo de 7 pasos antes del commit, archivos protegidos y cuándo
   parar y preguntar.
2. Escribir `CLAUDE.md` con `@AGENTS.md`.
3. Comprobar que las rutas citadas en `AGENTS.md` existen o van a existir en la fase 3.
4. Commit: `docs: add AGENTS.md and CLAUDE.md`.

**Revisión de Mateo:** el flujo y la lista de archivos protegidos.

### Fase 3 — Reglas y skill

1. Escribir `.agents/rules/monorepo-structure.md` (siempre activa).
2. Escribir `.agents/rules/brasaland-domain.md` (por patrón).
3. Escribir `.agents/rules/fastapi-services.md` (por patrón).
4. Escribir `.agents/rules/git-workflow.md` (bajo demanda).
5. Escribir `.agents/skills/update-memory-bank/SKILL.md` (objetivo, inputs, pasos, salida, criterios de
   aceptación).
6. Comprobar que cada regla tiene el alcance en el frontmatter y en la línea «Alcance:».
7. Commit: `feat: add agent rules and update-memory-bank skill`.

**Revisión de Mateo:** el alcance de las reglas y los criterios de la skill.

### Fase 4 — Validación

1. Ejecutar el flujo de `AGENTS.md` paso a paso sobre la rama.
2. Ejecutar la skill `update-memory-bank` sobre este propio hito (prueba real de la skill).
3. Repasar cada criterio de aceptación de la skill y anotar si se cumple.
4. Repasar la comprobación final (punto 9) y los 5 criterios de evaluación del enunciado.
5. Commit: `docs: update progress after milestone`.

**Revisión de Mateo:** validar el resultado completo antes del PR.

### Fase 5 — Entrega

1. Subir la rama (`git push -u origin feat/AGENTS-01-agent-memory-bank`).
2. Abrir el PR a `develop` con un enlace directo a `AGENTS.md` en la descripción.
3. Mateo entrega el enlace de ese PR en el campus de 4Geeks.
4. Cuando el profesor lo aprueba, Mateo fusiona (el agente no fusiona).
5. Tras la fusión: borrar la rama local (`git fetch --prune` y `git branch -d`).
6. El PR `develop → main` solo cuando Mateo lo pida.
7. Mateo pregunta al profesor si puede seguir con este flujo o si debe hacer los PR directos a `main`;
   según la respuesta se actualizan este plan, `git-workflow` y la memoria del proyecto.

---

## 9. Comprobación final (antes del PR)

- [ ] Los 3 archivos de `memory-bank/` existen y tienen contexto de negocio y técnico de Brasaland.
- [ ] `AGENTS.md` tiene la lectura inicial, los 7 pasos ordenados y la lista de archivos protegidos.
- [ ] Las 4 reglas tienen su alcance explícito.
- [ ] La skill tiene objetivo, inputs y criterios de aceptación.
- [ ] El mapa de `uis/website`, `uis/backoffice` y `services/` aparece en `techContext.md` y en
  `monorepo-structure`.
- [ ] No hay ninguna carpeta de app nueva.
- [ ] `BRIEFING.md` sigue sin modificar.
