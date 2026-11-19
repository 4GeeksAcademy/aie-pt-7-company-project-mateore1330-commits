---
description: Reglas del dominio de Brasaland (mercados, monedas, idiomas y datos) para el código de producto
globs:
  - "uis/**"
  - "services/**"
  - "packages/**"
  - "data/**"
alwaysApply: false
---

# Regla: dominio de Brasaland

**Alcance:** por patrón de archivo. Se aplica al crear o editar archivos en `uis/**`, `services/**`,
`packages/**` y `data/**`.

La referencia es [`CONTEXT.es.md`](../../CONTEXT.es.md). Si esta regla y ese archivo no coinciden, manda
`CONTEXT.es.md` y se avisa a Mateo.

## Qué hacer

1. **Todo importe lleva su moneda:** un campo `currency` con `COP` o `USD`. No se guardan números sin moneda.
2. **Todo dato de local, venta, proveedor, factura o precio lleva su mercado:** un campo `market` con `CO` o
   `US-FL`.
3. **Usa los nombres de entidad y de campo de `CONTEXT.es.md`** (`location`, `supplier`, `invoice`,
   `invoice_line`, `price_record`, `dish`, `dish_price`, `recipe`, `sale`, `customer`, `exchange_rate`…),
   en inglés y en `snake_case`. Si hace falta uno nuevo, se propone a Mateo y se añade primero a
   `CONTEXT.es.md`.
4. **El menú es común:** un `dish` y su `recipe` son los mismos en los dos mercados; el precio de venta va en
   `dish_price`, uno por mercado.
5. **El coste y el margen de un plato se calculan por mercado**, con el precio más reciente de cada producto
   en ese mercado.
6. **Los textos para clientes y para el personal se preparan en `es` y `en`.** Nada de textos fijos en un
   solo idioma dentro de la lógica.

## Qué no hacer

- **No sumes ni compares importes `COP` y `USD`** sin convertirlos con un `exchange_rate` explícito.
- **No mezcles precios de `CO` y `US-FL`** al calcular costes o márgenes.
- **No subas datos reales** de clientes, de personal ni facturas de proveedores. Los ejemplos de `data/raw/`
  son ficticios y se indica en su README.
- **No inventes valores de negocio** (precios, umbrales de alerta, nombres de locales o de proveedores). El
  umbral de alerta de precios está sin decidir: se pregunta.
