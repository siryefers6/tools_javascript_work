# Instrucciones de Copilot para tools_javascript_work

## Resumen del proyecto
- Herramienta HTML estática de una sola página para estampar IDs en PDFs cargados.
- Toda la lógica vive en [index.html](index.html) con `<script>` inline y marcado de UI.
- Usa dependencias por CDN: `pdf-lib` para edición de PDF y Tailwind para estilos.

## Arquitectura y flujo de datos
- El usuario selecciona uno o más PDFs en `#pdfInput` y ejecuta `procesarPDF(regex, tipo)` desde un botón.
- `procesarPDF` extrae el ID desde el nombre del archivo con una regex, carga el PDF con `PDFLib.PDFDocument.load`, edita la primera página y descarga un archivo con nombre generado.
- Las coordenadas se calculan desde la esquina superior derecha con márgenes; para Codelco se dibuja un rectángulo verde detrás del texto.

## Convenciones y patrones
- IDs basados en el nombre del archivo: Brumai usa `/3\d{7}/`, Codelco usa `/\d{4,10}/`.
- El estilo del texto depende de `tipo` (tamaño y rectángulo opcional).
- Mantener el enfoque de archivo único sin build, salvo que se solicite explícitamente.

## Dependencias externas
- `https://unpkg.com/pdf-lib/dist/pdf-lib.min.js` expone el global `PDFLib`.
- `https://cdn.tailwindcss.com` aporta clases utilitarias de Tailwind.

## Flujo de trabajo
- No hay build, pruebas ni bundling. Abrir [index.html](index.html) directamente en el navegador.

## Ejemplos a seguir
- Ajustar el sellado en `procesarPDF` (carga del PDF, medición de texto y uso de `drawRectangle`).
- Actualizar los botones para pasar nuevas parejas regex/tipo a `procesarPDF`.
