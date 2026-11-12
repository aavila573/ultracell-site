# UltraCell — Sitio web (entorno de PRUEBA)

SPA de una sola página para UltraCell, almacén de celulares nuevos y usados en Barranquilla, Colombia. Incluye catálogo de productos, carrito, checkout por WhatsApp, asesor IA con reglas locales y catálogo real de equipos usados.

> ⚠️ **Este repositorio es el entorno de PRUEBA** (`ultracell-preview`). Producción vive en un repo separado y no se toca desde acá. Los cambios se validan antes de pasar a producción.

## Qué hace

- Catálogo de **22 modelos** (21 iPhone + 1 iPad) con **variantes de capacidad y color** (arrays `PRODUCTS` + `VARIANTS` en `index.html`).
- Carrito de compras en memoria con checkout que **envía el pedido por WhatsApp** con la **variante exacta** (modelo + capacidad + color) y el total.
- Pago **simulado (demo)**: no hay pasarela real ni se realiza ningún cobro. Los textos de confirmación lo dejan explícito.
- Asesor IA con reglas locales: quiz recomendador por presupuesto, comparador y búsqueda por modelos.
- Hero real con imagen webp (`hero-17pm-plata.webp`) precargada vía `<link rel="preload">`.
- Sección "Nosotros", FAQ y ficha de producto con galería, lightbox y selector de color.
- SEO completo (title, meta description, Open Graph, canonical, schema Store + FAQPage, sitemap, robots).

## Tecnologías

- HTML5 semántico
- CSS3 embebido (design tokens con custom properties, mobile-first)
- JavaScript vanilla embebido (SPA con hash routing, IntersectionObserver, carrito en memoria)
- Sin dependencias externas ni frameworks
- Sin modo oscuro (paleta clara fija)

## Estructura del proyecto

```
ultracell-preview/
├── index.html                # HTML + CSS + JS embebidos (SPA completa)
├── README.md                 # Este archivo
├── sitemap.xml               # Sitemap para SEO
├── robots.txt                # Directivas para crawlers
├── imagenes_pendientes.txt   # Referencia de nomenclatura de imágenes
└── assets/
    ├── logo.jpeg             # Logo de UltraCell
    ├── foto_local.png        # Foto del local (Open Graph)
    └── catalogo/             # Fotos reales de productos en .webp (141 archivos)
        ├── hero-17pm-plata.webp
        ├── iphone-11-*.webp
        └── ...
```

## Instalación

No requiere instalación ni dependencias. Es un sitio estático.

```bash
git clone <repo-url>
cd ultracell-preview
```

## Uso local

Servir con cualquier servidor estático (usar `file://` directo puede fallar por rutas):

```bash
python -m http.server 8801
# visitar http://localhost:8801
```

## Configuración

### Variables de entorno

No requiere variables de entorno. Es un sitio estático sin backend. **No hay pasarela de pagos**: el checkout es un pedido por WhatsApp y el pago es simulado (demo).

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

- **22 modelos** en `PRODUCTS`, cada uno con variantes en `VARIANTS` (capacidad, colores, precio, stock, condición de batería, garantía).
- Fotos reales en `.webp` bajo `assets/catalogo/` (141 archivos). El manifiesto `IMAGE_MANIFEST` en `index.html` lista los archivos disponibles; si un archivo no está en el manifiesto, la vista cae a un SVG paramétrico (sin 404 ni errores de consola).
- Carrito en memoria (sin persistencia): agregar, quitar, ajustar cantidades.
- Checkout por WhatsApp: arma un mensaje con cada línea (modelo + capacidad + color + cantidad + precio) y el total, para confirmar disponibilidad y entrega.
- Badge `Usado` (condición y batería reales por variante, garantía 6 meses).

## Ficha de producto: galería, lightbox y selector de colores

La ficha (`#/producto/:id`) muestra una galería de hasta 4 vistas por producto
(`front`, `back`, `side`, `camera`), lightbox con navegación y selector de colores
con círculos y nombre visible. Las vistas se resuelven desde `assets/catalogo/`
según `IMAGE_MANIFEST`; el resto usa SVG paramétrico por color.

### Selector de colores

Derivado de `colors[]` + `PAL`. Al cambiar de color se actualizan la imagen y las
miniaturas; el precio, la capacidad y la disponibilidad no cambian.

## Integraciones

### WhatsApp

El botón flotante, el checkout y los CTAs apuntan a `https://wa.me/573007527308` con mensaje prellenado. No requiere credenciales ni API — es un enlace `wa.me` estándar.

### Asesor IA

Chat con reglas locales que conoce el catálogo: recomienda por presupuesto (quiz), compara modelos y resuelve dudas de envíos y pagos. No comparte datos con terceros; funciona offline.

## Deployment

### GitHub Pages

1. Crear repositorio en GitHub
2. Subir el contenido del proyecto
3. Activar GitHub Pages en Settings → Pages, rama `main`, carpeta `/root`
4. El sitio quedará disponible en `https://<usuario>.github.io/ultracell-preview/`

### Dominio personalizado

El dominio `ultracell.com.co` está pendiente de compra por el cliente. Cuando se adquiera:
1. Configurar registros DNS A/CNAME según GitHub Pages
2. En Settings → Pages → Custom domain, agregar `ultracell.com.co`
3. Actualizar `sitemap.xml` y `robots.txt` con el dominio final
4. Actualizar las URLs de Open Graph en `index.html`

## SEO

- `lang="es"` en `<html>`
- `<title>` y `<meta name="description">`
- Open Graph completo (og:image con foto del local)
- `<link rel="canonical">`
- `<link rel="icon">`
- Schema JSON-LD: `Store` con teléfono y dirección, `FAQPage` con preguntas frecuentes
- `sitemap.xml` y `robots.txt`

## Mantenimiento

### Cambiar contenido

Todo el contenido está en `index.html`. El catálogo se edita en los arrays `PRODUCTS` y `VARIANTS`. Las rutas SPA usan hash routing (`#/inicio`, `#/catalogo`, `#/nosotros`, `#/faq`, `#/carrito`).

### Responsive

Diseño mobile-first con breakpoints en **1120px**, **980px**, **640px** y **400px**. El sidebar de filtros del catálogo se colapsa desde 1120px (botón de filtros móvil) para evitar solape del badge `Usado` con la imagen en anchos intermedios. Sin scroll horizontal ni solapes en 360, 768, 1024, 1120 y 1280 px.

### Paleta de colores

Los colores se gestionan mediante CSS custom properties en `:root`. Color de marca: rojo `#c00d20`. Para cambiar la paleta, editar las variables `--accent` y relacionadas al inicio del bloque `<style>`.

## Licencia

© 2026 UltraCell. Todos los derechos reservados.
