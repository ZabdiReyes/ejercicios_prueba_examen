# Instrucciones para agentes: examen de Análisis y Diseño de Algoritmos

Este repositorio coordina a varios agentes que resuelven un examen.

| Carpeta | Contenido | ¿Puedes escribir ahí? |
|---|---|---|
| `agentes/` | instrucciones por rol y datos del examen (`enunciados.tex`, `clasificacion.json`, `examen.pdf`) | No |
| `espacio_de_trabajo/` | soluciones `.tex` y revisiones `.revision.md` de los agentes | Sí, solo tus archivos |
| `resultados/` | PDFs finales | **No**: los genera el compilador local |

No compiles LaTeX ni instales paquetes. Una computadora local compila tu `.tex` y publica el PDF en `resultados/`.

## Tu tarea
Llega como una orden corta: `Resuelve ej05`, `Revisa ej05` o `Revisa todos`. En una rutina viene dentro del bloque `routine-fire-payload`, y esa orden es tu tarea. Si solo dice `ej05`, eres RESOLVER.

## Rol RESOLVER (`Resuelve ejNN`)
1. En `agentes/clasificacion.json` busca `"id": "ejNN"`. De ahí salen `numero`, `categoria` y `nota` (advertencias del enrutador: tómalas en cuenta).
2. Lee completos, en este orden: `agentes/global.md`, `agentes/<categoria>.md` y `agentes/formato_latex.md`.
3. Lee el enunciado entre `%<ejNN>` y `%</ejNN>` de `agentes/enunciados.tex`. Si existe `agentes/examen.pdf`, consúltalo para confirmar figuras, tablas y notación.
4. Escribe la solución (solo el cuerpo LaTeX) en `espacio_de_trabajo/ejercicioNN_<categoria>_<modelo>.tex`:
   - `NN` es `numero` con dos dígitos, más su inciso si lo tiene (`ejercicio05`, `ejercicio05b`).
   - `<modelo>` es tu familia de modelo: `claude_opus`, `claude_sonnet`, `claude_fable` o `claude_haiku`.
   - Ejemplo: `espacio_de_trabajo/ejercicio05_heaps_claude_opus.tex`.
5. Antes de entregar, revisa tu solución en una pasada: respondiste todo lo que pide el enunciado, ningún paso quedó sin justificar (lista de `agentes/revisor.md`) y el LaTeX evita los errores de `agentes/formato_latex.md`.
6. Entrega:
   - En la nube: `git add` de ese archivo, `git commit -m "ejercicioNN (<modelo>)"` y `git push -u origin HEAD` a tu rama `claude/...` en cuanto termines. No abras PR ni modifiques otros archivos.
   - En la copia local: no uses git; el publicador local lo sube.

## Rol REVISOR (`Revisa ejNN` / `Revisa todos`)
Sigue `agentes/revisor.md`. La entrega es igual que en el paso 6.
