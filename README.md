# UltraCell — Sitio web

Landing page de una sola página para UltraCell, almacén de celulares nuevos y usados en Barranquilla, Colombia.

## Qué hace

Presenta los servicios de UltraCell (celulares nuevos y usados, accesorios, baterías, servicio técnico), destaca la garantía y confianza, muestra la ubicación y horario, e incluye botones de WhatsApp como llamado a la acción principal. Es la carta de presentación web del negocio.

## Tecnologías

- HTML5 semántico
- CSS3 embebido (design tokens con custom properties, mobile-first, modo oscuro)
- JavaScript vanilla embebido (scroll reveal con IntersectionObserver)
- Sin dependencias externas ni frameworks

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

No requiere variables de entorno. Es un sitio estático sin backend.

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

## Assets

| Archivo | Origen | Uso |
|---|---|---|
| `assets/logo.jpeg` | Logo provisto (1280×1280) | Header, hero, footer |
| `assets/foto_local.png` | Foto del local (1200×480) | Hero |

La paleta de colores se extrajo del logo con Python/PIL:
- Color dominante: negro (#000000, 87.4%)
- Color de marca/acento: rojo (#c00d20, 0.4%)
- Neutros: grises (#434341)

## Integraciones

### WhatsApp

El botón flotante y todos los CTAs apuntan a `https://wa.me/573007527308` con mensaje prellenado: "Hola UltraCell, vengo desde su página web y quiero más información". No requiere credenciales ni API — es un enlace wa.me estándar.

## Deployment

### GitHub Pages

1. Crear repositorio en GitHub
2. Subir el contenido del proyecto
3. Activar GitHub Pages en Settings → Pages, rama `gh-pages` o `main`, carpeta `/root`
4. El sitio quedará disponible en `https://<usuario>.github.io/ultracell-site/`

### Dominio personalizado

El dominio `ultracell.com.co` está pendiente de compra por el cliente en Hostinger. Cuando se adquiera:
1. Configurar registros DNS A/CNAME según GitHub Pages
2. En Settings → Pages → Custom domain, agregar `ultracell.com.co`
3. Actualizar `sitemap.xml` y `robots.txt` con el dominio final
4. Actualizar las URLs de Open Graph en `index.html`

## SEO

- `lang="es"` en `<html>`
- `<title>` y `<meta name="description">`
- Open Graph completo (og:image con foto del local)
- Twitter Card
- `sitemap.xml` y `robots.txt`
- `<link rel="canonical">`
- `<link rel="icon">`

## Mantenimiento

### Cambiar contenido

Todo el contenido está en `index.html`. Las secciones están marcadas con comentarios HTML (`<!-- ========== HERO ========== -->`, etc.) para facilitar la edición.

### Responsive

Diseño mobile-first con breakpoints en 768px (tablet), 1024px (desktop) y 1440px (large desktop). Sin scroll horizontal ni solapes en 360, 768, 1280 y 1920 px.

### Paleta de colores

Los colores se gestionan mediante CSS custom properties en `:root`. Para cambiar la paleta, editar las variables `--color-*` al inicio del bloque `<style>`.

## Estructura del proyecto

```
ultracell-site/
├── index.html      # HTML + CSS + JS embebidos
├── sitemap.xml     # Sitemap para SEO
├── robots.txt      # Directivas para crawlers
├── README.md       # Este archivo
└── assets/
    ├── logo.jpeg       # Logo de UltraCell
    └── foto_local.png  # Foto del local
```

## Licencia

© 2026 UltraCell. Todos los derechos reservados.
