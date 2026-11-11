# Elección de empresa: Brasaland

## ¿Por qué elegí Brasaland?

Elegí Brasaland porque conozco el sector de la restauración de cerca: mi familia ha trabajado en restaurantes y ha tenido los suyos propios, así que entiendo muchos de los problemas del día a día que describe la empresa. Además, tengo clientes del sector a los que les podrían interesar las herramientas que desarrolle en este proyecto, lo que le da una utilidad real más allá del bootcamp. Me atrae el reto de crear sistemas que funcionen en dos países, con dos monedas y dos idiomas, y que unifiquen los datos de 14 locales en tiempo real. Por último, quiero construir soluciones de IA cuyo valor cualquier persona no técnica entienda de inmediato.

## Departamentos que más me interesan

### 🛒 Compras y proveedores

Me interesa porque Lucía se entera de las subidas de precio de las materias primas cuando ya le ha llegado la factura, y no existe ningún dato consolidado de lo que gasta la cadena en cada mercado. Es un problema que tienen casi todos los restaurantes y que impacta directamente en la rentabilidad, así que resolverlo tiene un valor claro y medible.

### 📱 Marketing y experiencia digital

Me interesa porque hoy Brasaland no sabe quiénes son sus clientes: el programa de fidelización funciona con tarjetas de sellos que no generan datos y la web no acepta pedidos. Es el área en la que la tecnología se ve directamente desde el lado del cliente, y donde los datos pueden convertirse en mejores decisiones comerciales.

## Reto de automatización / IA que quiero construir

### "Del precio del proveedor al menú"

Un sistema que conecta las compras con el marketing para proteger el margen de cada plato:

1. **Lectura automática de facturas:** un workflow recoge las facturas de los ~20 proveedores (PDF o email) y un LLM extrae los productos, las cantidades y los precios.
2. **Historial de precios y alertas:** los datos se guardan para construir el historial de precios por proveedor y por mercado. Cuando un producto sube más de un umbral definido, se envía una alerta a Compras.
3. **Impacto en el coste de los platos:** con las recetas del menú se recalcula automáticamente el coste y el margen de cada plato, en COP y en USD.
4. **Recomendaciones para Marketing:** un agente de IA avisa al equipo de Marketing cuando un plato pierde margen y propone qué platos promocionar en la app o en las campañas según su rentabilidad actual.

Elegí este reto porque une los dos departamentos que más me interesan, abarca varios hitos del curso (Backend, Workflows, RAG y Agentes) y resuelve un problema que tienen todos los restaurantes, por lo que también podría ofrecérselo a mis clientes del sector.

## My AI Agent Idea

### Qué haría el agente

Un **agente de márgenes** que vigila los precios de los proveedores y protege la rentabilidad del menú. Cada vez que llega una factura, la lee, detecta qué productos han cambiado de precio, calcula cómo afecta eso al coste de cada plato y decide a quién avisar y qué recomendar: a Compras, para renegociar o buscar otro proveedor, y a Marketing, para cambiar qué platos se promocionan.

### Qué información necesita

- **Facturas de los ~20 proveedores** de Colombia y Florida, en PDF o por email.
- **Historial de precios** de cada materia prima por proveedor y por mercado (lo va construyendo el propio sistema).
- **Recetas del menú** con los ingredientes y las cantidades de cada plato.
- **Precios de venta** de cada plato en COP y en USD.
- **Ventas por plato y por local**, para saber qué platos pesan más en la facturación.
- **Tipo de cambio COP/USD**, para comparar los dos mercados.

### Qué produciría o activaría

- **Alerta a Compras** cuando un producto sube más de un umbral (por ejemplo, un 8 %), con el proveedor, la subida y los platos afectados.
- **Informe de margen por plato**, que muestra qué platos han perdido rentabilidad en cada país.
- **Recomendación a Marketing** de qué platos promocionar en la app o en las campañas y cuáles dejar de destacar.
- **Resumen semanal** con las subidas de precio, el impacto en el margen de la cadena y los proveedores con los que conviene negociar de forma centralizada.
