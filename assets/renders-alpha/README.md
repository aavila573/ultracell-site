# Biblioteca de renders oficiales Apple — con transparencia real

Generada el 17-nov-2026 para AxelIA / cliente UltraCell.
**Fuente:** CDN oficial de Apple (`store.storeimages.cdn-apple.com`), parámetro `fmt=png-alpha`.
**Patrón de URL correcto:** `iphone-<modelo>-<color>-select-<año>` (NO `finish-select`).

## Qué contiene

30 renders de producto, un equipo por archivo mostrado en dos vistas (trasera + frontal),
que es la composición oficial de Apple. Fondo transparente real (alpha 44–84%).

Tamaño final: 900px de ancho, WebP con alpha, ~1.4 MB total.

## Modelos disponibles

| Modelo | Colores | Archivos |
|---|---|---|
| iPhone 12 | Negro, Blanco, Azul, Verde, Rojo, Morado | 6 |
| iPhone 13 | Medianoche, Blanco estrella, Azul, Rosado | 4 |
| iPhone 14 | Medianoche, Blanco estrella, Azul, Morado, Rojo | 5 |
| iPhone 15 | Negro, Azul, Verde, Rosado, Amarillo | 5 |
| iPhone 16 | Negro, Blanco, Rosado, Verde azulado, Azul ultramarino | 5 |
| iPhone 16 Plus | Negro, Blanco, Rosado, Verde azulado, Azul ultramarino | 5 |

## Verificación realizada

- [x] **Alpha real** medido por píxeles: 44.5% a 83.8% transparente.
- [x] **Halo blanco** medido: 0.000% de píxeles brillantes en el borde (máx 0.123% en 1 archivo).
- [x] **Producto correcto** verificado visualmente en representantes de cada generación:
  - iPhone 12/13/14/15 → 2 lentes en **diagonal**, notch (12/13/14) o Dynamic Island (15).
  - iPhone 16/16 Plus → 2 lentes en **columna vertical**, Dynamic Island. Correcto para el 16.
- [x] **Sin cámaras deformadas** en ninguno de los verificados.

## Modelos que NO se pudieron obtener

**iPhone Pro y Pro Max (14, 15, 16):** el CDN no responde con ningún patrón probado
(`-select-`, `finish-select-`, `-finish-select-`, con y sin `-max`). Apple sirve esas
imágenes por una ruta distinta que no está en el HTML público del sitio.

Para piezas que requieran un Pro, las opciones hoy son:
1. El close-up de cámara del catálogo (`iphone-16-pro-back-sistema-de-c-maras-trasera.webp`), útil como detalle, no como equipo completo.
2. Foto real del inventario de UltraCell.

## Uso

```css
/* en cualquier pieza o en el sitio */
background-image: url('assets/renders-alpha/iphone-16-negro.webp');
```
Los archivos tienen alpha real: se pueden montar sobre cualquier color de fondo
sin recortar ni quitar fondo.

## Nomenclatura

`<modelo-slug>-<color-slug>.webp` — slugs en inglés, igual que el CDN de origen.
El manifiesto `manifest.json` traduce slug → nombre comercial en español.

## Advertencia (lección aprendida)

No asumir que un HTTP 200 significa que la imagen es el producto correcto.
Este catálogo se generó adivinando slugs y el primer resultado fue un "iPhone 17 Pro Max"
con un módulo de cámaras horizontal que **no existe** en ningún iPhone real.
Siempre verificar visualmente el producto, no solo el código de respuesta y el alpha.
