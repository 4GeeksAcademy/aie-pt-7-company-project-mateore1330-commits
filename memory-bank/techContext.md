# Tech context — Brasaland

> **Qué es este archivo:** el contexto técnico del proyecto: de dónde parte Brasaland, qué stack se usa,
> dónde va cada cosa y qué decisiones se han tomado. El agente lo lee al empezar cada sesión. Las decisiones
> nuevas se añaden a la tabla del punto 5 con la skill `update-memory-bank`.

---

## 1. De dónde parte Brasaland

Según el briefing, el stack actual de la empresa es mínimo:

- Una **web estática** de 2019 que no acepta pedidos online.
- Una **app obsoleta**, con una valoración de 2,8 en la app store.
- Un **TPV distinto en cada país**, sin integrar entre sí.
- **Hojas de cálculo** que hacen de sistemas de gestión (compras, RRHH, informes de turno).
- Pedidos a proveedores por **WhatsApp, teléfono y email**.
- **Sin API interna, sin datos consolidados y sin telemetría.**

Se construye casi desde cero.

---

## 2. Stack por fases

| Parte | Tecnología | Estado |
|---|---|---|
| `uis/website` | HTML5 semántico + Tailwind + JavaScript | Decidido, **revisable**: si un hito posterior pide Next.js, se migra |
| `uis/backoffice` | Sin decidir | Se decide en su hito |
| `services/api` | Python + FastAPI: una sola app con routers por dominio | Decidido |
| Estilos | Solo Tailwind, sin CSS a mano | Decidido (lo pide el hito de Web) |
| Base de datos, workflows, agentes, RAG | Sin decidir | Se deciden en sus hitos |

**Hoy no hay ninguna app creada.** El repo solo contiene la plantilla de 4Geeks y la documentación.

---

## 3. Mapa de carpetas

| Ruta | Qué va ahí |
|---|---|
| `uis/website` | Web pública de Brasaland (ruta `/`, marca y textos alineados con el briefing) |
| `uis/backoffice` | App interna, con su propio layout y separada de la web pública |
| `services/api` | API central FastAPI (locales, menús, ventas, clientes, proveedores) |
| `data/` | `raw/` → `pipelines/` → `process/`, y `eval/` para medir la calidad |
| `agents/`, `skills/`, `mcps/` | **Producto de IA de Brasaland** (p. ej. el agente de márgenes), en hitos posteriores |
| `workflows/` | Automatizaciones (p. ej. recoger las facturas de los proveedores) |
| `packages/shared/` | Tipos compartidos (`@repo/shared-types`) entre `uis/` y `services/` |
| `.agents/` | **Configuración del agente de programación:** reglas y skills de desarrollo |
| `memory-bank/` | Contexto activo del proyecto para el agente |
| `docs/plans/` | Planes de cada hito (`NN-hito-<nombre>.md`) |

- **No se crean carpetas paralelas:** nada de `frontend/`, `web/`, `api/` o `backend/` en la raíz. Si algo
  no encaja en el mapa, se pregunta.
- **`.agents/` no es `agents/`:** la primera ayuda a programar; la segunda es parte del producto.

---

## 4. Restricciones técnicas del dominio

- **Dos mercados:** `CO` (Colombia) y `US-FL` (Florida). Todo dato de un local, una venta, un proveedor o un
  precio lleva su mercado.
- **Dos monedas:** `COP` y `USD`. Todo importe lleva su moneda; nunca se suman importes de monedas
  distintas sin convertirlos con un tipo de cambio explícito.
- **Dos idiomas:** `es` y `en`. Los textos para clientes y personal se preparan para los dos.
- **Datos personales y facturas reales:** no se suben al repo. Los ejemplos de `data/raw/` son ficticios.
- **Nombres del dominio:** los de [`CONTEXT.es.md`](../CONTEXT.es.md).

---

## 5. Decisiones técnicas

| Fecha | Decisión | Motivo |
|---|---|---|
| 2026-11-19 | Backend en FastAPI: una sola app en `services/api` con routers por dominio, sin microservicios | Lo recomienda la plantilla. Desviación respecto al stack por defecto de Mateo (Flask) |
| 2026-11-19 | `uis/website` en HTML5 + Tailwind + JavaScript (revisable) | Encaja con la estructura del hito de Web (`index.html`, `application.html`, `validation.js`, `npx http-server`) |
| 2026-11-19 | Solo Tailwind, sin CSS a mano | Lo pide el hito de Web. Desviación respecto al stack por defecto (CSS Modules) |
| 2026-11-19 | Documentación en español; nombres de archivo y de campo en inglés | Reglas globales de Mateo |
| 2026-11-19 | `CLAUDE.md` contiene solo `@AGENTS.md` | Claude Code no lee `AGENTS.md` por sí solo |
| 2026-11-19 | `.gitignore`, `.env.example` y gitleaks se dejan para cuando aparezcan claves | No los pide el hito actual |
| 2026-11-19 | Los campos de las entidades de `CONTEXT.es.md` son una propuesta inicial; se fijan en el hito de Backend | Dar al agente una base coherente desde el principio |
| 2026-11-19 | Menú común: un `dish` y una `recipe` para los dos mercados, con un `dish_price` por mercado | El briefing exige que la comida sea igual en todos los locales; el precio sí cambia por país |
| 2026-11-19 | Las reglas de `.agents/rules/` declaran su alcance en el frontmatter (`alwaysApply`, `globs` o `description`) y en una línea «Alcance:» | El formato del frontmatter lo entienden los agentes (Cursor y otros), y la línea «Alcance:» se lee aunque la herramienta no lo procese |
| 2026-11-19 | El coste de un plato usa el precio más reciente de cada producto en el mercado del plato | Las subidas se reflejan en el margen en cuanto llega la factura, que es lo que busca el agente de márgenes |

---

## 6. Riesgos técnicos

- **Tailwind por CDN y PageSpeed:** cargar Tailwind por CDN puede bajar la nota de PageSpeed; si pasa, habrá
  que generar el CSS con la CLI de Tailwind. **Pendiente de confirmar** en el enunciado del hito de Web si
  se exige una nota mínima (el plan apunta a 80 o más, pero no está verificado).
- **`uis/website` es revisable:** si un hito posterior pide Next.js, habrá que migrar la web.
- **Sin seguridad configurada todavía:** el `.gitignore` está vacío y no hay hook de gitleaks. Hay que
  configurarlos antes de añadir la primera clave.
