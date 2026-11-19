# AGENTS.md — Brasaland

Instrucciones para cualquier agente de IA de programación (Claude Code, Cursor, Codex…) que trabaje en este
monorepo. El proyecto es la plataforma digital de **Brasaland**: 14 restaurantes de cocina a la brasa en
Colombia y Florida. Lo construye el equipo **Brasaland Digital**, y quien decide es **Mateo**.

- Responde y documenta en **español**. Los nombres de archivo, de campo y de código van en **inglés**, igual
  que los mensajes de commit.
- **Nunca inventes datos.** Si falta información, para y pregunta.
- **No implementes nada sin un plan aprobado por Mateo.** El silencio no es un sí.

---

## 1. Lectura al empezar cada sesión

Lee estos archivos **en este orden** antes de proponer o cambiar nada:

1. [`memory-bank/projectbrief.md`](./memory-bank/projectbrief.md): el negocio, las áreas y el reto elegido.
2. [`memory-bank/techContext.md`](./memory-bank/techContext.md): el stack, el mapa de carpetas y las
   decisiones técnicas.
3. [`memory-bank/progress.md`](./memory-bank/progress.md): el hito en curso, la rama y los próximos pasos.
4. [`CONTEXT.es.md`](./CONTEXT.es.md): el diccionario del dominio (entidades, campos, valores fijos y
   restricciones).
5. Las reglas de [`.agents/rules/`](./.agents/rules/) que apliquen a los archivos que vas a tocar:

| Regla | Alcance |
|---|---|
| [`monorepo-structure`](./.agents/rules/monorepo-structure.md) | Siempre activa |
| [`brasaland-domain`](./.agents/rules/brasaland-domain.md) | `uis/**`, `services/**`, `packages/**`, `data/**` |
| [`fastapi-services`](./.agents/rules/fastapi-services.md) | `services/**` |
| [`git-workflow`](./.agents/rules/git-workflow.md) | Bajo demanda: al hacer un commit o abrir un PR |

Si hay un plan del hito en curso en [`docs/plans/`](./docs/plans/), léelo también.

---

## 2. Flujo obligatorio antes de cada commit

Sigue estos pasos **en este orden**. Si uno falla, para, arréglalo o pregunta, y no pases al siguiente.

1. **Comprueba la rama.** Tiene que tener el formato `tipo/CÓDIGO-descripcion` (p. ej.
   `feat/AGENTS-01-agent-memory-bank`). **Nunca** se hace un commit en `main` ni en `develop`.
2. **Comprueba la ubicación.** Cada archivo nuevo está en la carpeta que le toca según
   [`monorepo-structure`](./.agents/rules/monorepo-structure.md). No hay carpetas paralelas.
3. **Pasa los tests y el lint** que existan para la parte que has tocado. Si no existen todavía, dilo; no
   lo des por superado en silencio.
4. **Revisa el diff** (`git diff --staged`): no hay `.env`, ni secretos, ni datos reales de clientes, de
   personal o de facturas de proveedores.
5. **Ejecuta la skill
   [`update-memory-bank`](./.agents/skills/update-memory-bank/SKILL.md)** para dejar `memory-bank/` al día.
6. **Haz el commit** con Conventional Commits en inglés (`feat:`, `fix:`, `docs:`, `refactor:`, `test:`,
   `chore:`) y **sin coautor de Claude**.
7. **Abre el PR a `develop`.** Mateo revisa y fusiona; **el agente no fusiona nunca**. El paso de `develop`
   a `main` lo hace solo Mateo, con otro PR.

---

## 3. No se modifica sin confirmación explícita de Mateo

- [`BRIEFING.md`](./BRIEFING.md), [`CONTEXT.md`](./CONTEXT.md) y [`CONTEXT.es.md`](./CONTEXT.es.md)
- [`AGENTS.md`](./AGENTS.md), [`CLAUDE.md`](./CLAUDE.md) y todo [`.agents/`](./.agents/)
- [`memory-bank/projectbrief.md`](./memory-bank/projectbrief.md)
- Los `README.md` y `README.es.md` de la plantilla (en la raíz y en cada carpeta)
- [`.devcontainer/`](./.devcontainer/), [`.gitignore`](./.gitignore) y
  [`packages/shared/types/`](./packages/shared/types/)
- Las ramas `main` y `develop`: **sin push directo**

`memory-bank/techContext.md` y `memory-bank/progress.md` sí se actualizan, pero solo con la skill
`update-memory-bank`.

---

## 4. Cuándo parar y preguntar

- **Falta un dato** (un precio, un nombre, un umbral, una regla de negocio): no se inventa.
- **Habría que crear una carpeta que no está en el mapa** de `techContext.md`.
- **Una decisión técnica contradice `techContext.md`** o una regla de `.agents/rules/`.
- **Hay que tocar un archivo de la lista del punto 3.**
- **El cambio no cabe en el plan aprobado.**

---

## 5. Recordatorio: `.agents/` no es `agents/`

- [`.agents/`](./.agents/) es la **configuración del agente de programación**: reglas y skills para
  desarrollar este repo.
- [`agents/`](./agents/), [`skills/`](./skills/) y [`mcps/`](./mcps/) son el **producto de IA de
  Brasaland** (p. ej. el agente de márgenes), que se construye en hitos posteriores.

No se mezclan nunca.
