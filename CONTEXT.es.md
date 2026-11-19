# Contexto del dominio — Brasaland

> **Qué es este archivo:** el diccionario del dominio de Brasaland. Todas las apps, servicios, agentes y
> prompts del monorepo usan **estos nombres, estos valores y estas restricciones**. El contexto de negocio
> completo está en [`memory-bank/projectbrief.md`](./memory-bank/projectbrief.md) y el briefing original en
> [`BRIEFING.md`](./BRIEFING.md).
> No se modifica sin la confirmación explícita de Mateo.

---

## 1. Brasaland en una frase

Cadena de 14 restaurantes propios de cocina a la brasa, fundada en Medellín en 2008, que opera en Colombia y
en Florida (EE. UU.) con unas 115 personas y unos 20 proveedores.

---

## 2. Valores fijos

| Concepto | Campo | Valores | Notas |
|---|---|---|---|
| Mercado | `market` | `CO`, `US-FL` | Colombia y Florida. Ningún otro de momento |
| Moneda | `currency` | `COP`, `USD` | `COP` en `CO` y `USD` en `US-FL` |
| Idioma | `language` | `es`, `en` | Textos para clientes y personal en los dos |

---

## 3. Entidades

Los nombres de entidad y de campo van en inglés y en `snake_case`. Los campos de esta tabla son la
**propuesta inicial**: los esquemas definitivos se fijan en el hito de Backend y se reflejan aquí.

| Entidad | Qué es | Campos clave |
|---|---|---|
| `market` | Uno de los dos mercados | `code`, `currency`, `default_language` |
| `location` | Un restaurante de la cadena (hay 14) | `id`, `name`, `market`, `city` |
| `supplier` | Un proveedor (hay unos 20 entre los dos mercados) | `id`, `name`, `market`, `category` |
| `product` | Una materia prima o un consumible que se compra | `id`, `name`, `category`, `unit` |
| `invoice` | Una factura de un proveedor (PDF o email) | `id`, `supplier_id`, `market`, `currency`, `issued_at`, `total` |
| `invoice_line` | Una línea de factura | `invoice_id`, `product_id`, `quantity`, `unit`, `unit_price` |
| `price_record` | Un precio de un producto en una fecha; forma el historial de precios | `product_id`, `supplier_id`, `market`, `currency`, `unit_price`, `recorded_at` |
| `dish` | Un plato del menú, **común a los dos mercados** | `id`, `name_es`, `name_en` |
| `dish_price` | El precio de venta de un plato en un mercado | `dish_id`, `market`, `sale_price`, `currency` |
| `recipe` | Los ingredientes y las cantidades de un plato, **iguales en todos los locales** | `dish_id`, `product_id`, `quantity`, `unit` |
| `sale` | Una venta registrada en un local | `id`, `location_id`, `market`, `currency`, `total`, `sold_at` |
| `customer` | Un cliente (hoy no hay datos; llegarán con la app de fidelización) | `id`, `market`, `language` |
| `exchange_rate` | Un tipo de cambio entre COP y USD en una fecha | `from_currency`, `to_currency`, `rate`, `date` |

**Categorías de proveedor y de producto** que cita el briefing: carne, verduras, salsas, bebidas, packaging y
productos de limpieza.

### Conceptos derivados

- **Coste de un plato en un mercado:** suma de `quantity × unit_price` de los productos de su `recipe`,
  usando el `price_record` **más reciente** de cada producto **en ese mercado**. Nunca se mezclan precios de
  `CO` y `US-FL`. Como la receta es la misma pero los proveedores no, un plato tiene un coste distinto en
  cada mercado.
- **Margen de un plato en un mercado:** `sale_price` de su `dish_price` en ese mercado menos su coste en ese
  mercado, en la moneda del mercado.
- **Alerta de precio:** se genera cuando el `unit_price` de un producto sube más de un umbral respecto al
  anterior `price_record`. **El umbral está sin decidir** (el ejemplo de partida es un 8 %).
- **Brasa Points:** el programa de fidelización actual, con tarjetas físicas de sellos.

---

## 4. Restricciones de negocio

1. **Todo importe lleva su moneda** (`currency`). Nunca se suman importes `COP` y `USD` sin convertirlos con
   un `exchange_rate` explícito.
2. **Todo dato de local, venta, proveedor, factura o precio lleva su mercado** (`market`).
3. **Las recetas y los estándares son los mismos en todos los locales**, sean del país que sean.
4. **Los textos para clientes y para el personal se preparan en `es` y `en`**. Si hay que empezar por uno,
   se empieza por un idioma base.
5. **Las leyes laborales son distintas en cada país:** lo que toque a personal se segmenta por mercado.
6. **No se suben datos reales** de clientes, de personal ni facturas de proveedores. Los ejemplos son
   ficticios.

---

## 5. Personas que aparecen en el dominio

| Persona | Rol | Le importa |
|---|---|---|
| Mariana Restrepo | CEO | Ventas de la cadena en USD y COP, informe de los lunes a las 7:00 |
| Felipe Guerrero | Director de Operaciones | Ventas por local en tiempo real, stock y pedidos |
| Lucía Fernández | Responsable de Compras | Precios de los proveedores, alertas de subida, compras consolidadas |
| Camila Ospina | Responsable de Marketing | Clientes, fidelización, qué platos promocionar |
| Ashley Turner | Responsable de Personas y Cultura (Miami) | RRHH por país, onboarding |
| Jake Morrison | Responsable de Formación y Calidad (Miami) | Recetas y estándares iguales en todos los locales |
| Nicolás Park | CTO (Medellín) | API central, telemetría y pipeline de datos |

_Versión corta en inglés: [`CONTEXT.md`](./CONTEXT.md)._
