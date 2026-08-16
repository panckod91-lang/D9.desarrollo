# D9 Pedidos PWA

PWA liviana para toma de pedidos comerciales con funcionamiento online/offline, cola local de pendientes y sincronización automática.

## Stack actual

- Frontend: HTML, CSS y JS puro.
- Hosting: Cloudflare Pages.
- Lectura de datos: Apps Script API (`?action=bootstrap`).
- Envío de pedidos: Cloudflare Worker.
- Base de datos: Google Sheets.

## Archivos principales

- `index.html`: estructura de la UI y modales.
- `styles.css`: diseño visual.
- `app.js`: lógica de datos, pedidos, historial, pendientes y sincronización.
- `sw.js`: service worker para cache offline de archivos propios.
- `manifest.json`: configuración PWA.

## Limpieza aplicada

- Eliminada la carpeta `netlify/`.
- Eliminado `netlify.toml`.
- Eliminadas referencias internas a Netlify.
- Eliminada lectura vieja vía OpenSheet.
- La app queda leyendo datos desde Apps Script mediante `BOOTSTRAP_URL`.
- Service Worker conserva estrategia network-first para archivos propios y no intercepta requests externos.

## v1.5.7-prod (fix ID congelado)
- Fix crítico: el pedido_id se congela para el pedido actual y se libera inmediatamente para que el próximo pedido no arrastre el mismo ID mientras el envío/verificación sigue en segundo plano.
- La verificación contra PC ya no valida sólo por ID: si el ID existe pero pertenece a otro cliente/productos/total, no lo toma como cargado.
- Se elimina el reintento automático con ID nuevo ante colisión, para no mezclar WhatsApp/PC ni esconder el error.
- Los duplicados controlados ahora se marcan como cargados en PC con mensaje claro: "Ya estaba cargado en PC. No se duplicó.".
