# Diseño: frente del consultorio responsive

## Intención

Mostrar la nueva foto vertical en celulares y la foto horizontal en pantallas grandes para que el frente del consultorio se vea completo y bien encuadrado en cada dispositivo.

## Alcance

- Cambiar únicamente la imagen del hero en `index.html`.
- Usar `<picture>` con `media` para que el navegador elija una sola imagen según el ancho de pantalla.
- Ajustar el tamaño del contenedor: formato vertical en móvil y formato panorámico en escritorio.
- Mantener el efecto hover, la superposición de gradiente y el resto del diseño existente.

## Fuera de alcance

- No modificar otras imágenes, secciones, textos ni navegación.
- No agregar dependencias ni JavaScript.

## Enfoques considerados

1. **`<picture>` con dos fuentes responsive (elegido):** carga la imagen adecuada para cada viewport y conserva accesibilidad con un único `alt`. Es la opción más eficiente y semántica.
2. Alternar dos imágenes con clases CSS: sería funcional, pero puede provocar que ambas imágenes se descarguen y duplicaría el marcado.

## Decisión

Usar `<picture>` con `frenteConsultorioVertical.jpeg` como fuente base y `frenteConsultorioHorizontal.jpeg` para pantallas `lg` en adelante. El contenedor conservará esquinas redondeadas y `object-cover`, con alturas proporcionales al formato de cada imagen.

## Validación

Comprobar visualmente el HTML y verificar que ambas rutas existan y que el documento no tenga errores de estructura después del cambio.
