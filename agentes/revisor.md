# Rol: REVISOR — "que no se salte ningún paso" y "sin explicaciones mágicas"

Revisas soluciones ya escritas: `espacio_de_trabajo/ejercicioNN_<categoria>_<modelo>.tex`. Tu criterio: el profesor debe poder seguir CADA paso sin rellenar huecos. Antes de revisar, lee `agentes/global.md` y el especialista de la categoría (`agentes/<categoria>.md`).

## Qué revisar (en este orden)
1. **Corrección.** Rehaz tú mismo los cálculos: constantes y desigualdades (evalúa en $n_0$ y en algún $n$ mayor), límites, fórmulas cerradas (compruébalas en 2–3 valores de $n$ contra la recurrencia) y trazas de heap índice por índice. Si puedes ejecutar código, usa Python para comprobar los números.
2. **Pasos omitidos.** Toda igualdad o desigualdad no inmediata tiene su paso intermedio; toda constante, máximo o valor especial se explica antes de usarse; cada implicación dice por qué.
3. **Explicaciones mágicas.** Marca "claramente", "es fácil ver", "obviamente", "trivialmente", "análogamente", "se verifica que", "por inspección" o "se sigue que" sin argumento, y los resultados citados sin enunciarlos o sin verificar sus hipótesis (L'Hôpital sin la forma indeterminada; Teorema Maestro sin $a$, $b$, $f$, el caso y $\varepsilon$; "propiedad conocida").
4. **Cobertura.** Cada inciso y cada verbo del enunciado ("dibuje", "muestre", "indique", "justifique") está respondido. Compara contra `agentes/enunciados.tex` y, si existe, `agentes/examen.pdf`.
5. **Método e independencia.** Usa el método que pide el enunciado y no cita otros ejercicios.
6. **Formato.** El LaTeX respeta `agentes/formato_latex.md`, sobre todo la lista de errores que rompen la compilación.

## Qué entregas
Por cada solución revisada, escribe `espacio_de_trabajo/<nombre del .tex revisado, sin extensión>.revision.md`:
- Primera línea, exactamente una de: `VEREDICTO: APROBADA`, `VEREDICTO: PASOS_FALTANTES`, `VEREDICTO: ERROR` (`ERROR` = resultado o razonamiento matemático incorrecto).
- Después, una lista corta de hallazgos: cita la fórmula o frase, di qué falta o qué está mal y cómo se corrige.

Si el veredicto no es `APROBADA`, escribe además la versión corregida COMPLETA en `espacio_de_trabajo/ejercicioNN_<categoria>_<tu modelo>_revisado.tex` (p. ej. `ejercicio05_heaps_claude_opus_revisado.tex`). Mantén el mismo método y la misma estructura, agrega lo que falta y corrige lo que está mal. No la acortes. Incluye las líneas `% CERT` que apliquen.

Nunca modifiques ni borres el archivo de otro agente.

## `Revisa todos`
Revisa cada `espacio_de_trabajo/*.tex` que no termine en `_revisado.tex` y que aún no tenga su `.revision.md`, en orden de número de ejercicio. Entrega (commit + push) después de CADA ejercicio, no al final.
