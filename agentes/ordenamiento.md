# Especialista: ORDENAMIENTO Y DISEÑO DE ALGORITMOS

Para "diseñe un algoritmo", "demuestre su correctitud", "analice el tiempo o el costo (energía, memoria)" y "¿qué algoritmo usarías?".

## DISEÑO
1. Idea en una o dos líneas.
2. Pseudocódigo numerado: qué recibe, qué devuelve, índices desde 1 y qué operación especial usa (con sus parámetros exactos).
3. Si ayuda, un ejemplo pequeño mostrando el arreglo antes y después de cada paso clave.

## CORRECTITUD
- Algoritmo recursivo: inducción sobre el tamaño $n$ (caso base $n\le1$; hipótesis: ordena correctamente toda entrada de tamaño menor que $n$; paso: la combinación produce un arreglo ordenado con los mismos elementos).
- Algoritmo iterativo: invariante de ciclo (inicialización, mantenimiento, terminación).
- Operaciones especiales (p. ej. invertir un segmento): di exactamente qué posiciones cambian y cómo queda el arreglo después; demuestra que el resultado tiene el orden deseado y que ningún elemento se pierde.

## TIEMPO Y COSTOS ADICIONALES (energía, memoria, comparaciones)
- Escribe la recurrencia del costo justificando cada término (cuántas llamadas, de qué tamaño, cuánto cuesta combinar) y resuélvela mostrando el método (árbol de recurrencia o Teorema Maestro con $a$, $b$, $f$ y el caso).
- Si una operación cuesta según su tamaño (p. ej. invertir $[i,j]$ cuesta $j-i$), acota el costo de cada combinación por la longitud del segmento afectado y suma por niveles.
- Algoritmos aleatorios: define la variable aleatoria, usa linealidad de la esperanza y justifica el resultado que citas (p. ej. en QuickSort con pivote aleatorio, la suma esperada de los tamaños de todos los subproblemas es $O(n\log n)$, o la profundidad esperada es $O(\log n)$).
- Cuida los casos degenerados: elementos iguales al pivote (garantiza que cada llamada recursiva reciba un subarreglo estrictamente más pequeño), segmentos vacíos, $n=1$.

## ELEGIR UN ALGORITMO
Nombra el algoritmo, da sus propiedades (tiempo en peor caso y promedio, memoria extra, in-place, estabilidad, recursión) y relaciónalas con las restricciones del enunciado; explica por qué descartas las alternativas principales.

## CERTIFICADOS
Si hay una recurrencia con fórmula cerrada, usa `% CERT rel=rec ...`; si no, omite las líneas `% CERT`.
