# Simulador RCP Neonatal — prototipo estático

Sitio estático en HTML, CSS y JavaScript, pensado para GitHub Pages. No necesita instalar dependencias ni ejecutar un servidor backend.

## Cómo añadir tu propio video

1. Copia tu archivo de video a la carpeta `assets`.
2. Nómbralo exactamente `video-neonatal.mp4`.
3. Comprueba que la estructura sea:

   ```text
   simulador-rcp-neonatal/
   ├── index.html
   ├── README.md
   └── assets/
       ├── video-neonatal.mp4
       └── VIDEO_AQUI.txt
   ```

4. Si el archivo está en otro formato, actualiza la ruta y el `type` del elemento `<source>` en `index.html` (por ejemplo, `video/webm`).

El botón **Cargar mi video** sirve para previsualizar un archivo local mientras pruebas la web. Esa selección no se guarda en GitHub; para que todos los visitantes puedan verlo, debes subir el video dentro de `assets`.

## Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub.
2. Sube `index.html`, `README.md` y la carpeta `assets` con tu video.
3. Abre **Settings → Pages** en el repositorio.
4. En **Build and deployment**, selecciona **Deploy from a branch**.
5. Elige la rama `main` y la carpeta `/(root)`; pulsa **Save**.
6. Espera a que GitHub Pages publique el sitio y abre la URL que aparece en esa sección.

## Contenido clínico

Los escenarios y opciones incluidos son un guion demostrativo basado en los pasos generales que aparecen en el algoritmo neonatal AHA/AAP 2025. Antes de utilizar el simulador con estudiantes o en formación clínica, un instructor NRP cualificado debe revisar y aprobar cada pregunta, explicación y adaptación al nivel de atención. No sustituye cursos, protocolos ni juicio clínico; no incluye dosis de medicamentos y el monitor visual es decorativo.

Referencias para revisión:
- [Algoritmos AHA de RCP y atención cardiovascular de emergencia](https://cpr.heart.org/en/resuscitation-science/cpr-and-ecc-guidelines/algorithms/)
- [Programa de Reanimación Neonatal (NRP), 9.ª edición — AAP](https://www.aap.org/en/pedialink/neonatal-resuscitation-program/nrp-9th-edition/)
