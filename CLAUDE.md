# Preescolar de Lucraft — instrucciones para Claude

Este repositorio es el sitio https://preescolar.lucraft.com.mx: juegos y actividades de preescolar para proyectar en el salón. Es un sitio estático (sin compilación y sin servidor). Cloudflare Pages publica la carpeta `public/`, y cada `git push` a `main` lo vuelve a publicar en 1 o 2 minutos. No hay otro paso.

Los otros sitios de Lucraft viven en sus propios repositorios (`lucraft` y `little-bloom-minds`). No se tocan desde aquí.

## Agregar una actividad

1. Crea `public/<carpeta>/index.html`. El nombre de `<carpeta>` va en minúsculas, sin acentos ni espacios y con guiones (por ejemplo `memorama-nombres`).
2. La página debe ser un documento completo y autocontenido:
   - Lleva `<!doctype html>`, `<html lang="es-MX">`, `<meta charset="utf-8">`, `<meta name="viewport" content="width=device-width, initial-scale=1">` y `<title>`.
   - Si viene de un artifact de claude.ai, el visor ponía esa envoltura y dos reinicios que aquí hay que escribir: `html, body { margin: 0; }` y `[hidden] { display: none !important; }`. Quita las etiquetas `<meta name="claude:…">`.
   - No puede usar `window.claude` (base de datos, descargas, etc.) porque aquí no hay servidor. Una actividad que guarda datos se queda en claude.ai.
   - Solo puede cargar fuentes de Google Fonts; todo lo demás va dentro del archivo.
   - Pon un botón de casita que regrese a la portada: `<a href="../" aria-label="Todas las actividades">`.
   - Copia las etiquetas para compartir que ya tienen las otras páginas (`og:title`, `og:description`, `og:url` con su dirección completa y `og:image` con `https://preescolar.lucraft.com.mx/og.jpg`), para que la liga se vea con imagen en WhatsApp.
3. Agrega su tarjeta en `public/index.html`, dentro de `<ul class="lista">`, como el primer `<li class="act">` (la más nueva va primero). Copia la estructura de la tarjeta que ya existe: dibujo en SVG, `<h2>` con la mayúscula dentro de `<span class="q">`, una línea de descripción, etiquetas y el enlace `.jugar` con `href="<carpeta>/"`. Los enlaces van siempre relativos (sin `/` al inicio).
4. Prueba con Playwright sirviendo `public/` como raíz. Revisa que no haya errores en consola, que no haya desplazamiento horizontal a 1280×720 ni a 390×844, y que "Jugar" y la casita lleven a donde deben.
5. Haz commit en `main` con el mensaje `Agrega <nombre de la actividad>` y luego `git push`.
6. Espera 1 o 2 minutos y confirma que abre en https://preescolar.lucraft.com.mx/<carpeta>/.

## Reglas de contenido (todo esto es público)

- Nunca pongas nombres, fotos, firmas ni datos de los alumnos o de sus familias, ni listas del grupo.
- Español de México. En los títulos para niños, la mayúscula inicial va en rojo (`#E1262D`).
- Todo se piensa para el proyector: letra grande, un solo tema claro y botón de pantalla completa.
