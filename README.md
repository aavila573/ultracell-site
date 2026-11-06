# UltraCell — Sitio web (demo)

SPA de una sola página para UltraCell, almacén de celulares nuevos y usados en Barranquilla, Colombia. Clon de la demo Juls adaptado a la marca UltraCell con catálogo de productos, carrito, checkout por WhatsApp, asesor IA integrado y notas de demostración.

## Qué hace

- Catálogo de 32 productos iPhone (nuevos y usados, múltiples capacidades y colores).
- Carrito de compras con checkout que envía el resumen por WhatsApp a UltraCell.
- Asesor IA con reglas locales (recomendador por presupuesto, comparador, dudas frecuentes).
- Sección "Nosotros" con historia basada en datos reales del brief.
- SEO completo (title, meta, Open Graph, Twitter Card, schema Store, FAQPage).
- Diseño mobile-first con modo oscuro, identidad roja (#c00d20).

## Tecnologías

- HTML5 semántico
- CSS3 embebido (design tokens con custom properties, mobile-first, modo oscuro)
- JavaScript vanilla embebido (SPA con hash routing, IntersectionObserver, carrito en memoria)
- Sin dependencias externas ni frameworks

## Estructura del proyecto

```
ultracell-site/
├── index.html              # HTML + CSS + JS embebidos (SPA completa)
├── README.md               # Este archivo
├── sitemap.xml             # Sitemap para SEO
├── robots.txt              # Directivas para crawlers
└── assets/
    ├── logo.jpeg               # Logo de UltraCell (1280×1280)
    ├── foto_local.png          # Foto del local (1200×480)
    └── catalogo/               # Imágenes de productos (22 archivos .jpg)
        ├── iphone-11.jpg
        ├── iphone-12.jpg
        ├── ...
        └── iphone-17-pro-max.jpg
```

## Instalación

No requiere instalación ni dependencias. Es un sitio estático.

```bash
# Clonar (cuando el repo remoto exista)
git clone <repo-url>
cd ultracell-site
```

## Uso local

Abrir `index.html` directamente en un navegador, o servir con cualquier servidor estático:

```bash
python -m http.server 8000
# visitar http://localhost:8000
```

## Configuración

### Variables de entorno

No requiere variables de entorno. Es un sitio estático sin backend. La pasarela de pagos (Wompi) está en modo Sandbox (simulada); en producción las llaves privadas se manejarían solo en el backend.

### Datos de contacto (hardcodeados en el HTML)

| Dato | Valor |
|---|---|
| WhatsApp | wa.me/573007527308 |
| Teléfono visible | 300 752 7308 |
| Instagram | @ultracellbq |
| TikTok | @ultracellbq_ |
| Dirección | C.C. San Andresito el Pupi, Local 30, Barranquilla |
| Horario | Lunes a sábado, 9:00 am – 6:00 pm |

Para cambiar estos datos, editar `index.html` directamente.

## Catálogo y carrito

- 32 productos iPhone en el catálogo (array `CATALOG` en `index.html`), desde iPhone 11 hasta iPhone 17 Pro Max.
- Carrito en memoria (sin persistencia): agregar, quitar, ajustar cantidades.
- Checkout envía el resumen del carrito por WhatsApp al número de UltraCell con mensaje prellenado.
- Precios de demostración (COP). Badges de oferta, novedad y más vendidos.

## Integraciones

### WhatsApp

El botón flotante, el checkout y todos los CTAs apuntan a `https://wa.me/573007527308` con mensaje prellenado. No requiere credenciales ni API — es un enlace wa.me estándar.

### Asesor IA

Chat con reglas locales que conoce el catálogo: recomienda por presupuesto, compara modelos y resuelve dudas de envíos y pagos. No comparte datos con terceros; funciona offline.

## Deployment

### GitHub Pages

1. Crear repositorio en GitHub
2. Subir el contenido del proyecto
3. Activar GitHub Pages en Settings → Pages, rama `main`, carpeta `/root`
4. El sitio quedará disponible en `https://<usuario>.github.io/ultracell-site/`

### Dominio personalizado

El dominio `ultracell.com.co` está pendiente de compra por el cliente en Hostinger. Cuando se adquiera:
1. Configurar registros DNS A/CNAME según GitHub Pages
2. En Settings → Pages → Custom domain, agregar `ultracell.com.co`
3. Actualizar `sitemap.xml` y `robots.txt` con el dominio final
4. Actualizar las URLs de Open Graph en `index.html`

## SEO

- `lang="es"` en `<html>`
- `<title>` (53 caracteres) y `<meta name="description">`
- Open Graph completo (og:image con foto del local)
- Twitter Card
- `sitemap.xml` y `robots.txt`
- `<link rel="canonical">`
- `<link rel="icon">`
- Schema JSON-LD: `Store` con teléfono y dirección, `FAQPage` con preguntas frecuentes

## Mantenimiento

### Cambiar contenido

Todo el contenido está en `index.html`. El catálogo se edita en el array `CATALOG`. Las rutas SPA usan hash routing (`#/inicio`, `#/catalogo`, `#/nosotros`, `#/faq`, `#/carrito`).

### Responsive

Diseño mobile-first con breakpoints en 768px (tablet), 1024px (desktop) y 1440px (large desktop). Sin scroll horizontal ni solapes en 360, 768, 1280 y 1920 px.

### Paleta de colores

Los colores se gestionan mediante CSS custom properties en `:root`. Color de marca: rojo `#c00d20`. Para cambiar la paleta, editar las variables `--accent` y relacionadas al inicio del bloque `<style>`.

## Licencia

© 2026 UltraCell. Todos los derechos reservados.
