# D9 Pedidos / Desarrollo

PWA para toma de pedidos comerciales y ventas de mostrador para distribuidora.

## Estado

Versión de desarrollo: v1.2.6-dev

## Funciones principales

- Login por usuario.
- Roles: vendedor, cliente, invitado y mostrador.
- Toma de pedidos con clientes, categorías y productos.
- Envío de pedidos por WhatsApp.
- Historial local con reutilización de pedidos.
- Cola de pendientes offline.
- Consulta de lista de precios.
- Modo Mostrador para comprobantes internos con cantidad/peso decimal.

## Rol Mostrador

El rol `mostrador` muestra una entrada protagonista de Venta Mostrador y oculta el banner publicitario.

La venta mostrador usa:

- cliente existente o cliente ocasional, separado del pedido común;
- categoría propia;
- selector de productos con selección visual;
- cantidades enteras o fraccionadas, con coma o punto;
- cálculo local de total;
- salida por impresión o WhatsApp.

## Arquitectura

Frontend estático:

- `index.html`
- `styles.css`
- `app.js`
- `sw.js`

Backend actual para pedidos normales:

- Google Apps Script
- Google Sheets
- Cloudflare Pages / Worker según entorno

El módulo Mostrador de esta etapa trabaja en frontend y no escribe todavía en Sheets.

## Notas de desarrollo

- No tocar backend para Mostrador hasta definir si las ventas internas deben registrarse en hoja propia.
- Mantener separado el estado de pedido normal y venta mostrador para evitar cruces de cliente/categoría/carrito.
- Mantener localStorage controlado: historial limitado, pendientes offline y catálogos cacheados.
