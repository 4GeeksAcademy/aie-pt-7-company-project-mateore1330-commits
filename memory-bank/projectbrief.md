# Project brief — Brasaland

> **Qué es este archivo:** el contexto de negocio estable del proyecto. El agente lo lee al empezar cada
> sesión y **no lo modifica** sin la confirmación explícita de Mateo.
> **Fuentes:** [`BRIEFING.md`](../BRIEFING.md) y [`company-choice.md`](../company-choice.md). Si un dato no
> está en esas fuentes, no se inventa: se pregunta.

---

## 1. La empresa

- **Brasaland:** cadena de restaurantes de cocina a la brasa. Se fundó en 2008 en Medellín (Colombia) como
  un único local familiar.
- **Tamaño hoy:** 14 restaurantes propios, unas 115 personas y alrededor de 6 millones de dólares de
  facturación anual.
- **Dos mercados:** Colombia y Estados Unidos (Florida). Eso supone dos monedas (COP y USD), dos idiomas
  (español e inglés) y dos legislaciones laborales.
- **Sedes:** la central está en Medellín y hay una oficina comercial y de operaciones en Miami que coordina
  los locales de Florida.
- **Situación:** es rentable y tiene clientes fieles en los dos mercados, pero gestiona una operación de dos
  países con herramientas pensadas para un solo restaurante. Mientras tanto, la competencia gana terreno con
  pedidos digitales, marketing basado en datos y dashboards operativos.

### Los tres compromisos de la marca

1. La comida sabe igual en Medellín que en Miami.
2. Un servicio cálido y siempre igual.
3. Una cocina rápida.

Cualquier herramienta que se construya debe ayudar a mantener estos tres compromisos.

---

## 2. Organización y responsables

| Área | Responsable | Sede |
|---|---|---|
| Dirección ejecutiva | Mariana Restrepo, CEO desde 2019 (hija del fundador) | Medellín |
| Operaciones de restaurante | Felipe Guerrero | No consta |
| Compras y proveedores | Lucía Fernández | No consta |
| Marketing y experiencia digital | Camila Ospina | No consta |
| Personas y cultura | Ashley Turner | Miami |
| Formación y estándares de calidad | Jake Morrison | Miami |
| Tecnología | Nicolás Park, CTO | Medellín |

**Brasaland Digital:** el equipo interno que creó Mariana para construir las herramientas, los sistemas y
las automatizaciones que modernicen la empresa sin perder su esencia. **Este proyecto se hace desde ese
equipo.**

---

## 3. Problemas y necesidades por área

| Área | Problema principal | Qué necesita |
|---|---|---|
| **Operaciones** | Los 14 locales trabajan aislados, sin que la sede vea nada en tiempo real. Los pedidos de ingredientes se hacen por WhatsApp o teléfono, así que en unos locales sobra stock y en otros falta. Los informes de turno se hacen en papel o Excel y se envían a RRHH cada semana | Dashboard de ventas en tiempo real por local (COP y USD), pedidos de ingredientes inteligentes según las ventas históricas y el stock, y alertas cuando un local no registra ventas durante su horario de apertura |
| **Compras** | Unos 20 proveedores entre Colombia y Florida (carne, verduras, salsas, bebidas, packaging y limpieza). Los precios se negocian por email y Excel, por separado en cada mercado. Lucía se entera de las subidas cuando llega la factura. No hay datos consolidados de compras de la cadena | Plataforma de proveedores con historial de precios y alertas, y visibilidad consolidada de las compras para negociar de forma centralizada |
| **Marketing** | La web es de 2019 y no acepta pedidos. La app tiene una valoración de 2,8 en la app store. «Brasa Points» funciona con tarjetas físicas de sellos: el 60 % de los clientes no las usa y no generan datos. No se sabe quiénes son los clientes | App de fidelización y pedidos, CRM con el historial y las preferencias de cada cliente, y un motor de personalización |
| **Personas y cultura** | 115 personas en dos países con leyes laborales distintas. Casi todo se gestiona por email y Excel. El onboarding del personal de cocina, que rota mucho, es manual | Portal de RRHH (vacaciones y ausencias), onboarding automatizado y dashboard de KPIs de RRHH por país (rotación, absentismo y tiempo para cubrir vacantes) |
| **Formación** | Las recetas y los estándares tienen que ser los mismos en todos los locales. El material está en un Google Drive en el que nadie se aclara. Comunicar un cambio de receta a los 14 locales en dos idiomas lleva días | Catálogo de recetas con búsqueda, itinerario de incorporación y distribución simultánea de los cambios de receta. ES/EN opcional pero muy recomendable, empezando por un idioma base |
| **Tecnología** | Web estática, app obsoleta, un TPV distinto en cada país sin integrar y hojas de cálculo en lugar de sistemas de gestión. No hay API interna, ni datos consolidados, ni telemetría | API central (locales, menús, ventas, clientes y proveedores), telemetría en tiempo real desde cada local y un pipeline de datos que alimente los dashboards |
| **Dirección** | No hay un dashboard unificado. Mariana decide con llamadas, con informes en PDF que llegan los martes y con su intuición. No puede responder al momento a «¿cuánto vendimos esta semana en Florida?» | Dashboard ejecutivo (ventas en USD y COP), un asistente de IA al que preguntar en lenguaje natural y un informe semanal automático cada lunes a las 7:00 |

---

## 4. Enfoque elegido por Mateo

**Áreas de interés:** Compras y proveedores, y Marketing y experiencia digital.

### Reto: «Del precio del proveedor al menú»

Un sistema que conecta Compras con Marketing para proteger el margen de cada plato:

1. **Lectura automática de facturas:** un workflow recoge las facturas de los proveedores (PDF o email) y un
   LLM extrae los productos, las cantidades y los precios.
2. **Historial de precios y alertas:** se guarda el historial por proveedor y por mercado. Cuando un producto
   sube más de un umbral, se avisa a Compras.
3. **Coste de los platos:** con las recetas se recalculan el coste y el margen de cada plato, en COP y USD.
4. **Recomendaciones para Marketing:** un agente avisa cuando un plato pierde margen y propone qué platos
   promocionar según su rentabilidad actual.

### El agente de márgenes (producto de IA, hitos posteriores)

- **Necesita:** las facturas de los proveedores, el historial de precios, las recetas (ingredientes y
  cantidades), los precios de venta en COP y USD, las ventas por plato y por local, y el tipo de cambio
  COP/USD.
- **Produce:** alertas de subida de precio a Compras (proveedor, subida y platos afectados), un informe de
  margen por plato y por país, recomendaciones de promoción a Marketing y un resumen semanal (subidas,
  impacto en el margen y proveedores con los que conviene negociar de forma centralizada).
- **Umbral de alerta:** el ejemplo de `company-choice.md` es un 8 %, pero **todavía no está decidido**.

**Por qué este reto:** une las dos áreas que interesan a Mateo, abarca varios hitos del curso (Backend,
Workflows, RAG y Agentes) y resuelve un problema de todos los restaurantes, así que podría ofrecerse a
clientes reales del sector.
