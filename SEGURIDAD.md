# Seguridad · Landing Bocado

## 1. Medidas integradas en el código
- **Sin JavaScript** en la página: no hay scripts, ni handlers inline (`onclick`, etc.), ni `innerHTML` ni `eval`.
- **CSP estricta** sin `unsafe-inline`: el CSS está en `css/styles.css` y no quedan atributos `style=""`. Solo se permiten recursos propios (la tipografía Inter está guardada en `fuentes/`).
- **CSP también como `<meta>`** (respaldo si el hosting no envía cabeceras). `frame-ancestors`, HSTS y `X-Frame-Options` solo funcionan desde cabeceras del servidor.
- **Enlaces externos:** el enlace a terereestudio.com.ar lleva `rel="noopener"`. Cuando se agreguen enlaces `target="_blank"`, deben llevar `rel="noopener noreferrer"`.
- **Imágenes sin metadatos** (EXIF, GPS, dispositivo) y con peso reducido.
- **Firma de Tereré Estudio** compatible con la CSP (imagen propia, sin scripts).
- **Sin datos personales:** la landing no tiene formularios, cookies, analítica ni almacenamiento local. No hay nada que enviar ni guardar.

## 2. Configuración del servidor (lista para pegar)
- **Netlify / Cloudflare Pages:** archivo `_headers` (incluido). Redirección HTTPS: Netlify y Cloudflare Pages ya fuerzan HTTPS; activar "Always Use HTTPS".
- **Apache / hosting compartido:** archivo `.htaccess` (incluido): redirección 301 a HTTPS, cabeceras, sin listado de directorios y bloqueo de archivos ocultos.
- **Vercel / Nginx:** no incluidos. Si el hosting es alguno de estos, pedinos el dato y armamos el archivo.

## 3. Tareas pendientes [COMPLETAR]
- [COMPLETAR] Hosting elegido y confirmación de qué archivo de configuración usar (`_headers` o `.htaccess`).
- [COMPLETAR] Dominio: registrar lock, renovación automática y 2FA en el registrador, hosting y Cloudflare.
- [COMPLETAR] Cloudflare (plan gratis): proxy, Bot Fight Mode y TLS automático.
- [COMPLETAR] Enlaces reales de WhatsApp (`https://wa.me/<número>?text=` con el texto armado con `encodeURIComponent()`) y de Instagram. Hoy son `#`.
- [COMPLETAR] Email del dominio con SPF, DKIM y DMARC (`p=quarantine` o `reject`), para evitar suplantación.
- [COMPLETAR] Si se agrega un formulario: honeypot, trampa de tiempo, captcha (Turnstile), validación en el servidor y Política de Privacidad con consentimiento (Ley 25.326).
- [COMPLETAR] Si se agrega analítica: preferir opciones sin cookies (Plausible, Umami o Cloudflare Web Analytics).
- [COMPLETAR] Página 404 personalizada y `/.well-known/security.txt` con un contacto de seguridad.
- [COMPLETAR] Aviso legal y datos del responsable, si el cliente lo quiere publicar.

## 4. Riesgos residuales (en simple)
- **Tipografía:** Inter está guardada en el mismo sitio (`fuentes/`, de Fontsource): ya no se carga nada desde Google.
- **Mapas:** el botón "Cómo llegar" abre Google Maps en otra página, fuera del sitio. No hay iframe, por lo que no hay datos enviados a terceros al cargar la página.
- **Imágenes de producto placeholder:** son generadas y deben reemplazarse por fotos reales antes de publicar.
- **Sin formulario**, el riesgo de datos personales es nulo hoy. Cuando se agregue uno, aplicar la sección 6 del protocolo completa.
- Ninguna web es 100 % invulnerable. El objetivo es eliminar los vectores comunes y reducir el impacto de un incidente.

## 5. Verificación posterior a la publicación
securityheaders.com, SSL Labs (ssllabs.com/ssltest) y Mozilla Observatory. Objetivo: nota A o superior. Revisar la consola del navegador sin errores de CSP.
