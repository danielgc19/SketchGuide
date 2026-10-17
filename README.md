# SketchGuide

Herramienta web para estudiar proporciones al dibujar: sube una foto o un dibujo, conviértelo en un boceto a lápiz, superpón líneas guía y descarga el resultado como referencia. Todo se procesa en tu navegador; ninguna imagen se sube a un servidor.

## Uso

No requiere instalación ni dependencias. Abre `index.html` en un navegador moderno (Chrome, Edge, Firefox o Safari). La tipografía Figtree se carga desde Google Fonts y, si no hay conexión, se usa la fuente del sistema.

## Funciones

- Carga de PNG, JPG y WEBP (selector o arrastrar y soltar), con mensajes de error claros.
- Boceto a lápiz con 4 modos (realista, lineal, suave y alto contraste) y ajustes de intensidad, detalle, sombras, contraste, brillo, nitidez y blancura del papel.
- Guías: cruz central exacta al 50 % del ancho y alto originales, cuadrículas 3×3, 4×4 y 5×5, color, grosor, opacidad, posición por porcentaje y bloqueo.
- Zoom (rueda, botones, pellizco), desplazamiento, pantalla completa e inversión horizontal de la vista.
- Comparación original / boceto / divisor deslizante.
- Exportación en PNG a resolución original: original, boceto limpio, boceto con guías y original con guías. Impresión ajustada a la página (A4, A3, Carta).

## Cómo funciona el boceto a lápiz

1. Se convierte la imagen a escala de grises (las transparencias se componen sobre blanco).
2. Se invierte el tono y se desenfoca con un gaussiano aproximado (tres pasadas de desenfoque de caja).
3. Se combinan ambas capas con *color dodge*: `gris * 255 / (255 - desenfoque)`. Las zonas planas quedan blancas y los bordes y sombras se marcan como trazos de grafito.
4. Según el modo se aplica una curva (sombras suaves, líneas, bajo o alto contraste) y después intensidad, contraste, brillo, blancura del papel y nitidez.

La vista previa se calcula sobre una copia reducida (máx. 1400 px). La exportación se recalcula a la resolución original. La imagen original nunca se modifica y cada cambio parte de ella.

## Publicar en GitHub Pages

1. Sube el contenido de esta carpeta a un repositorio.
2. En *Settings → Pages*, elige la rama `main` y la carpeta `/ (root)`.
3. La app quedará en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/` y la versión simple en `/guias-simples/`.

## Pruebas manuales básicas

- **Guías:** carga una imagen de 1001 × 601 px; la cruz debe cruzarse en (500,5; 300,5). Comprueba que sigue centrada al hacer zoom y mover la imagen.
- **Zoom:** rueda, botones y "Ajustar" deben mantener las guías alineadas sin deformar la imagen.
- **Exportación:** descarga las 4 variantes y verifica que miden lo mismo que el original y que "Original" es idéntico al archivo cargado.
- **Errores:** prueba con un PDF, un archivo de más de 40 MB y una imagen dañada; debe aparecer un aviso sin romper la app.

## Pendiente

Historial local de imágenes recientes, arrastrar las guías con el ratón, impresión a tamaño definido y procesamiento en un hilo aparte para imágenes muy grandes.
