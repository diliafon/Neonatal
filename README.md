# Primer aliento — experiencia interactiva

Aplicativo educativo de reanimación neonatal con **10 escenas: 9 decisiones evaluables y una reflexión final**. Los videos se reproducen desde Google Drive mediante iframes; no se descargan ni se alojan en GitHub Pages.

**Versión documentada:** configuración organizada R3.1, según la última entrega de esta conversación.  
**Documentación actualizada:** 20 de octubre de 2026.  
**Alcance:** documentación de uso y mantenimiento; no constituye validación clínica ni verificación del sitio publicado.

## 1. Estructura del repositorio

```text
primer-aliento/
├── index.html
├── styles.css
├── app.js
├── videos.json
├── README.md
├── Manual-de-usuario-ES.pdf
└── User-Manual-EN.pdf
```

La estructura conserva los archivos Word que aparecen en la configuración compartida y añade los nuevos manuales PDF. Los documentos son recursos de consulta; no intervienen en la ejecución del aplicativo.

| Archivo | Función |
| --- | --- |
| `index.html` | Estructura de la interfaz, portada, selección de contexto, visores, diálogos, reflexión y resultados. |
| `styles.css` | Diseño editorial, colores, tipografía del sistema, retroalimentación, distribución móvil y barra inferior de confirmación. |
| `app.js` | Preguntas, opciones, explicaciones, enlaces de video, estado de sesión, confirmación, puntuación y navegación. |
| `videos.json` | Copia de referencia de la correspondencia entre paso y enlace de Drive. No se carga automáticamente en la versión entregada. |
| `README.md` | Guía del proyecto, configuración, publicación y limitaciones. |
| Manuales `.pdf` | Nuevas guías de usuario en español e inglés para compartir o imprimir. |

## 2. Características

- Sitio estático sin backend ni proceso de compilación.
- HTML, CSS y JavaScript separados; sin bibliotecas externas ni fuentes remotas.
- Diseño con fondos marfil, verde profundo, acentos terracota y tipografía serif del sistema.
- Dos contextos: nivel 1/rural y niveles 2–4/hospitalario.
- Videos de Google Drive compartidos entre ambos contextos para cada paso.
- Nueve decisiones con opciones aleatorias, reintentos y retroalimentación.
- Rojo y verde intensos acompañados por etiquetas de respuesta incorrecta/correcta.
- Explicaciones de error desplegables y mensaje clave destacado donde el guion lo incluye.
- Paso 10 de reflexión final sin preguntas ni puntuación.
- Resultado sobre 9 aciertos al primer intento y cuaderno de repaso.

## 3. Ejecución local

Conserva `index.html`, `styles.css` y `app.js` juntos en la raíz. Si tienes Python instalado, abre una terminal en esa carpeta y ejecuta:

```bash
python -m http.server 8000
```

Abre `http://localhost:8000`. Para detener el servidor, pulsa `Ctrl+C`.

Python solo se utiliza en esta alternativa de prueba local; no es una dependencia del sitio publicado. Los videos requieren conexión a internet y acceso a Drive, incluso al probar localmente.

## 4. Publicación en GitHub Pages y QR

1. Sube el contenido de la carpeta del proyecto a la raíz del repositorio. No dejes `index.html` dentro de una carpeta adicional si vas a publicar desde la raíz.
2. En la configuración de Pages del repositorio, selecciona la rama y carpeta que contienen `index.html` (por ejemplo, `main` y `/(root)` en una publicación desde rama).
3. Espera a que termine la publicación y abre la URL que indique GitHub Pages.
4. Comprueba selección de contexto, preguntas, videos y reflexión final desde la dirección publicada.
5. Prueba el acceso desde un celular y una ventana privada, especialmente los permisos de Drive.
6. Genera el QR con la URL pública definitiva, no con la ruta local ni con el ZIP.

No se incluye un QR ni un enlace al sitio porque no se ha proporcionado su dirección pública definitiva. Los PDF no aparecen enlazados en la interfaz automáticamente: si deseas ofrecerlos desde la web, añade enlaces a los archivos correspondientes en `index.html`.

## 5. Configurar los videos

### Fuente utilizada por el aplicativo

La lista que consume la aplicación está en `VIDEO_SOURCES`, dentro de `app.js`. Ejemplo de estructura (reemplaza el ID de ejemplo por uno real):

```js
{
  step: 1,
  label: "Paso 1",
  url: "https://drive.google.com/file/d/ID_DEL_VIDEO/view?usp=drive_link"
}
```

La función `videoLinks()` valida el enlace y construye la dirección del visor:

```text
https://drive.google.com/file/d/ID_DEL_VIDEO/preview
```

El botón «Abrir en Drive» conserva el enlace original. No es necesario convertir los enlaces en direcciones de descarga.

### Cómo sustituir un video

1. Localiza el registro del paso en `VIDEO_SOURCES` dentro de `app.js`.
2. Cambia únicamente su `url`, respetando el número de `step` y el orden de los registros.
3. Mantén diez registros: pasos 1 a 9 para decisiones y paso 10 para reflexión.
4. Actualiza también `videos.json` para mantener sincronizada la copia de referencia.
5. Publica los cambios y prueba tanto el visor integrado como «Abrir en Drive».

**Importante:** editar solo `videos.json` no cambia el video reproducido en esta implementación. No se añadió una carga dinámica de JSON ni se modificó el aplicativo como parte de esta entrega documental.

## 6. Recorrido e interacción

1. El participante selecciona nivel 1/rural o niveles 2–4.
2. En cada paso evaluable reproduce el video desde los controles de Drive.
3. Pulsa «Ya terminé de ver la escena» y confirma «Sí, la vi completa».
4. Lee el escenario y elige una respuesta.
5. Si es incorrecta, puede revisar las explicaciones y volver a intentar.
6. Si es correcta, se habilita el avance. La clave de respuesta procede del guion suministrado, no de una validación clínica independiente.
7. Después del paso 9 accede a la reflexión final.
8. Desde el paso 10 puede abrir el resumen, volver a la reflexión o reiniciar desde los controles disponibles.

### Confirmación personal, no detección automática

El iframe de Drive no comunica al aplicativo cuándo terminó realmente el video. «Ya terminé de ver la escena» es una declaración personal. No verifica atención ni visualización completa y no impide adelantar dentro del visor de Drive.

Un clic en una respuesta antes de confirmar muestra una alerta y no cuenta como intento. La barra móvil inferior facilita la confirmación y desaparece al confirmarla. En el paso 10 no se solicita confirmación ni se muestran preguntas.

No se desbloquea por un temporizador ni por terminar de cargar el iframe. La navegación al resumen desde la reflexión es manual.

### Puntuación y estado

- Máximo de 9 aciertos al primer intento, no 10.
- Un error en el primer intento deja ese paso marcado para repaso aunque se responda correctamente después.
- No se restan puntos por el clic bloqueado anterior a la confirmación.
- Las opciones cambian de orden; no memorices su letra.
- No se almacenan respuestas en un servidor ni hay cuentas del aplicativo, certificados o integración LMS.
- Recargar, cerrar la pestaña o reiniciar pierde el recorrido actual. El resultado no se guarda automáticamente.

## 7. Mantenimiento y errores de consola

### Constantes duplicadas

En `app.js`, declara una sola vez:

```js
const QUESTION_COUNT = STEPS.length;
const TOTAL_SCENES = VIDEO_SOURCES.length;
```

No pegues un segundo bloque de configuración ni cargues `app.js` dos veces. Si aparece `Identifier 'QUESTION_COUNT' has already been declared`, revisa ambas situaciones. `index.html` debe tener una única inclusión del script:

```html
<script src="app.js"></script>
```

Si tienes Node instalado, puedes revisar la sintaxis con:

```bash
node --check app.js
```

### Atributos de pantalla completa

La configuración acordada usa `allow="autoplay; fullscreen"` y omite el atributo redundante `allowfullscreen` para evitar la advertencia de precedencia. El permiso `autoplay` no garantiza reproducción automática: el usuario utiliza los controles de Drive.

### Problemas con videos

- Compara el visor con «Abrir en Drive».
- Usa «Recargar visor» o «Recargar video final».
- Revisa que el acceso al archivo esté autorizado para los asistentes.
- Registra una captura del error, paso, navegador y si también falla el enlace directo.
- La página no puede leer automáticamente los mensajes de error internos del visor.

### Cambios que no aparecen

Comprueba que se haya publicado la carpeta correcta, que los archivos actualizados estén en la misma versión y que no estés viendo una copia anterior. La marca de versión del pie ayuda a identificar la entrega, pero no demuestra por sí sola la disponibilidad de los videos.

## 8. Privacidad y conectividad

El aplicativo no incorpora cuentas propias, analítica ni registro de respuestas en un servidor. Esto no significa ausencia total de solicitudes de red: GitHub Pages aloja la web y los iframes conectan con Google Drive. El acceso y funcionamiento de los videos dependen de Google, sus permisos y las restricciones del navegador.

## 9. Revisión clínica obligatoria

Las opciones y píldoras se trasladaron del documento suministrado, sin certificarlas como recomendaciones vigentes. Revisar con el responsable clínico antes de utilizar como formación validada:

- Paso 4: coherencia entre los cortes de edad gestacional de las opciones y la explicación de oxígeno inicial; revisar cifras, cadencia y localización del sensor.
- Paso 8: mención de 30 segundos tras compresiones y momento de reevaluación/medicación.
- Dosis, concentraciones, tiempos, umbrales de glucemia, recursos y criterios de vía aérea.
- Interpretación de la línea «Ventila, 2, Ventila» del nivel rural, incorporada al distractor de altas presiones según la nota del guion.

El recurso no sustituye protocolos, formación especializada ni juicio clínico. No usar para atender pacientes ni certificar competencias.

## 10. Estado de verificación

La conversación registra revisiones previas de sintaxis y del flujo de interfaz, pero esta actualización de documentación no constituye una nueva prueba del repositorio o sitio desplegado. La captura compartida muestra nombres de archivos, no permite inspeccionar su contenido actual.

Antes de la conferencia verifica la versión realmente publicada, la ausencia de declaraciones duplicadas, los diez enlaces, los permisos de Drive, la reflexión sin preguntas y la visualización en dispositivos reales. No se garantiza reproducción solo por haber incorporado los enlaces.

## 11. Manuales de usuario

- `Manual-de-usuario-ES.pdf`: guía en español de acceso, reproducción, confirmación, respuestas, puntuación, reflexión y resolución de problemas.
- `User-Manual-EN.pdf`: guía equivalente en inglés; mantiene las etiquetas españolas de los botones y explica su significado en inglés.

Los manuales Word de la carpeta pueden conservarse como archivos editables anteriores. No fueron reescritos en esta entrega; si se publican junto a los PDF, revisa su concordancia con la versión actual.
