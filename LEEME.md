# ECO2BIZ · Monitoreo geotécnico de relaveras

Prototipo navegable. **El mapa satelital ya está operativo** y apunta a la
**relavera Orcopampa (Arequipa)**, en `-15.278304, -72.334352`: los instrumentos
están distribuidos sobre el borde del vaso y la corona del dique, y la zona InSAR
sobre el talud suroeste, contrastados uno a uno contra la imagen satelital.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Plataforma unificada (copia de la V2). Es lo que se abre por defecto al desplegar. |
| `relavera-orcopampa.jpg` | Foto aérea del depósito. La usa la portada de la plataforma. |
| `eco2biz_plataforma_unificada_V2.html` | Plataforma completa: resumen, sección instrumentada, **vista en planta con Google Maps + capa InSAR**, umbrales, inventario y reportes. |
| `eco2biz_mapa_piezometros.html` | Mapa satelital dedicado a piezómetros, con buscador, filtros por estado y panel de detalle. |
| `eco2biz_monitoreo_volcan.html` | Primer dashboard (sin mapa). |
| `especificacion_funcional_eco2biz_volcan.docx` | Especificación funcional: módulos, requerimientos e historias de usuario. |

## Cómo desplegarlo

Son archivos estáticos: **no necesitan servidor, build ni dependencias**.

**Lo más rápido — sin desplegar nada:** doble clic a `eco2biz_plataforma_unificada_V2.html`.
Abre en el navegador con el mapa funcionando.

**Netlify Drop:** arrastrar esta carpeta a https://app.netlify.com/drop → URL al instante.

**Vercel:** `npx vercel --prod` dentro de esta carpeta.

**GitHub Pages:** ya publicado en https://fabrizzioper.github.io/relaveras-volcan-prototipo/
(Settings → Pages → Branch `main`, carpeta `/`).

**Servidor propio (IIS, Apache, nginx):** copiar la carpeta al directorio público. Nada más.

## IMPORTANTE — proteger la API key

La key de Google Maps va escrita dentro del HTML, que es como funciona la
Maps JavaScript API: **siempre queda visible en el navegador del cliente**. Por
eso no se protege escondiéndola, sino restringiéndola.

Antes de publicar esto en una URL pública, en Google Cloud Console →
APIs y servicios → Credenciales → seleccionar la key:

1. **Restricción de aplicación → Sitios web (referrers HTTP)** y listar solo los
   dominios donde va a correr (por ejemplo `https://midominio.com/*`).
2. **Restricción de API → solo Maps JavaScript API.**
3. Definir una **cuota diaria máxima** en el panel de cuotas.

Sin esas restricciones, cualquiera puede copiar la key y el consumo se factura
a la cuenta de Google Cloud del titular.

## Pendiente para producción

Los datos están escritos dentro del HTML (arreglos `piezometers`,
`instrumentData` e `insarZones`) y son **ilustrativos**. Para producción:

- Las coordenadas ubican cada instrumento sobre el dique con precisión de
  fotointerpretación (±15 m aprox.). Reemplazarlas por el levantamiento GPS de campo.
- Poblar las lecturas desde el conector de telemetría (RF-01) en vez de hardcodearlas.
- Cargar las zonas InSAR reales con su fecha de pasada satelital.
- La portada rotula el depósito a 4 220 msnm y 82/84 instrumentos: cifras de
  ejemplo, confirmarlas con el equipo de geotecnia antes de presentarlas.
