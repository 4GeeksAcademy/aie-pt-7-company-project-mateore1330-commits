---
description: Cómo se organiza el backend FastAPI de Brasaland en services/
globs:
  - "services/**"
alwaysApply: false
---

# Regla: servicios FastAPI

**Alcance:** por patrón de archivo. Se aplica al crear o editar archivos en `services/**`.

## Qué hacer

1. **Hay una sola app FastAPI**, en `services/api`. Todo endpoint nuevo se añade ahí.
2. **Un router por dominio**, con los nombres de [`CONTEXT.es.md`](../../CONTEXT.es.md): locales, menús,
   ventas, clientes, proveedores, facturas…
3. **Los esquemas de entrada y salida usan los nombres de campo de `CONTEXT.es.md`** y aplican la regla
   [`brasaland-domain`](./brasaland-domain.md): `market` y `currency` donde toque.
4. **Las claves y la configuración se leen de variables de entorno**, nunca del código.
5. **`services/api` tiene su `README.md`** con qué hace, cómo se instala, cómo se ejecuta y cómo se prueba.

## Qué no hacer

- **No crees microservicios** ni una segunda app FastAPI.
- **No crees un worker aparte** salvo que sea imprescindible (p. ej. un proceso largo que no puede correr
  dentro de la API). Si hace falta, se propone a Mateo y va en su propia carpeta dentro de `services/`.
- **No metas lógica de interfaz** en `services/`: las pantallas van en `uis/`.
