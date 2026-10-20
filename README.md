# Primer aliento — experiencia interactiva

## Entrega

Sitio estático sin dependencias, basado en el index original y en los nueve pasos de la tabla del DOCX. Rediseño editorial con fondos marfil, verde profundo, acentos terracota y tipografía serif del sistema. No usa fuentes remotas, servicios de analítica ni bibliotecas externas.

La versión actual incorpora diez escenas: nueve decisiones evaluables y una reflexión final sin preguntas ni puntuación. Los videos se reproducen mediante iframes de Google Drive; no es necesario descargarlos ni alojarlos en GitHub Pages.

## Estructura del proyecto

```text
primer-aliento/
├── index.html
├── styles.css
├── app.js
├── videos.json
└── README.md
```

- `index.html`: estructura y contenido de la interfaz.
- `styles.css`: diseño, colores, responsive y accesibilidad.
- `app.js`: lógica, preguntas, respuestas, navegación y fuentes de video.
- `videos.json`: referencia legible de los diez enlaces de Drive.
- `README.md`: esta documentación.

No se requieren videos locales, dependencias, backend ni proceso de compilación.

## Incorporar videos

Los diez enlaces ya están incorporados en `VIDEO_SOURCES`, dentro de `app.js`. Cada entrada declara el paso, una etiqueta descriptiva y la URL original de Google Drive.

```js
{
  "step": 1,
  "label": "Paso 1",
  "url": "https://drive.google.com/file/d/ID_DEL_VIDEO/view?usp=drive_link"
}
```

La función `videoLinks()` valida el dominio y la ruta, extrae el identificador y genera la dirección de incrustación:

```text
https://drive.google.com/file/d/ID_DEL_VIDEO/preview
```

«Abrir en Drive» conserva el enlace original. Ambos contextos comparten el video de cada paso, pero mantienen las preguntas y explicaciones diferenciadas del documento.

Para cambiar un video, edita la URL correspondiente en `VIDEO_SOURCES` dentro de `app.js`. Conserva el formato de enlace de Google Drive y actualiza también `videos.json` si deseas mantener la documentación sincronizada.

No pegues enlaces de páginas de YouTube: este reproductor requiere un archivo de Google Drive incorporable mediante iframe.

## Publicación y QR

Sube `index.html`, `styles.css`, `app.js`, `videos.json` y `README.md` a la raíz de tu repositorio de GitHub Pages.

1. Abre **Settings → Pages**.
2. En **Build and deployment**, selecciona **Deploy from a branch**.
3. Elige la rama `main` y la carpeta `/(root)`.
4. Guarda y espera a que GitHub Pages publique el sitio.
5. Abre la URL pública desde un celular y comprueba que el pie muestre: **Versión 10 pasos · enlaces 19 OCT · R3**.
6. Crea el QR apuntando a esa dirección pública.

El QR debe apuntar al sitio publicado, no al archivo local ni al ZIP. No se incluye QR porque aún no se proporcionó una dirección pública de destino.

## Prueba local

Desde la carpeta del proyecto, ejecuta:

```bash
python -m http.server 8000
```

Luego abre:

```text
http://localhost:8000
```

No abras el archivo directamente con `file://` si tu navegador restringe comportamientos de iframe; usar un servidor local es más representativo de GitHub Pages.

## Reglas de interacción

- Selección inicial de nivel 1/rural o niveles 2–4.
- Diez escenas en total: nueve con decisiones y una reflexión final.
- Las opciones se presentan en orden aleatorio en cada recorrido.
- Las respuestas indicadas como correctas en el DOCX son la clave del ejercicio.
- En los pasos 1 a 9, el clic antes de confirmar la visualización muestra un diálogo y **no cuenta como intento**.
- La confirmación «Ya terminé de ver la escena» es personal: el visor de Google Drive no informa al aplicativo cuándo termina realmente el video.
- Esta confirmación no verifica que se haya visto la escena completa ni impide adelantar el video desde los controles de Drive.
- Cambiar de escena reinicia el bloqueo de respuestas.
- Respuesta incorrecta: explicación y reintento.
- Respuesta correcta: explicación, píldoras de aprendizaje, mensaje clave y acceso a la siguiente escena.
- El resultado final cuenta únicamente los aciertos al primer intento.
- La puntuación máxima es 9, porque el paso 10 no es evaluable.
- El resultado incluye un cuaderno de repaso de los nueve pasos.
- No hay persistencia al recargar, cuentas, notas guardadas ni integración LMS.
- Este control de reproducción es pedagógico, no un sistema antifraude: puede modificarse desde las herramientas de desarrollo. Tampoco verifica atención humana.

## Paso 10: reflexión final

Después de responder correctamente el paso 9, aparece **Ir a la reflexión final**.

El paso 10 reproduce el video de reflexión y no contiene preguntas, opciones, confirmación de visualización ni puntuación. Incluye navegación al resumen, enlace para abrir el archivo original en Drive y botón para recargar el video final.

La reflexión final no modifica el resultado de las nueve decisiones.

## Revisión clínica obligatoria

Se trasladaron las opciones y las píldoras del documento, sin certificarlas como recomendaciones vigentes. La interfaz muestra que el contenido está pendiente de revisión docente. Revisar antes de presentar como formación validada, especialmente:

- **Paso 4:** los cortes de edad gestacional difieren entre la opción correcta y la explicación de oxígeno inicial; validar cifras, cadencia y localización del sensor.
- **Paso 8:** revisar la mención de 30 segundos tras compresiones y el momento de reevaluación/medicación.
- Confirmar dosis, concentraciones, tiempos, umbrales de glucemia, disponibilidad de recursos y criterios de vía aérea con el responsable clínico.
- El párrafo suelto «Ventila, 2, Ventila» del nivel rural se anexó al distractor de altas presiones, siguiendo la nota de interpretación incluida en el DOCX.

Las explicaciones reproducen el guion, no una revisión independiente de evidencia. No emplear este prototipo para atender pacientes ni certificar competencias.

## Comprobaciones realizadas

- Sintaxis JavaScript verificada con Node.
- Navegador Chromium automatizado, ancho 390 px: sin desbordamiento horizontal; alerta por clic temprano sin penalización; recorrido de nueve respuestas correctas hasta resultados; sin errores JavaScript en ese flujo.
- Correspondencia validada para las diez URL originales y sus direcciones de incrustación `/preview`.
- Reflexión final verificada: sin preguntas, sin puntuación y con navegación al resumen.
- Sin desbordamiento horizontal en la pantalla final a 320, 360, 390, 768 y 1280 px.
- Los videos definitivos, Safari/iOS/Android reales y permisos de Google Drive todavía deben probarse: los enlaces no pudieron abrirse desde la herramienta de verificación de esta sesión.
