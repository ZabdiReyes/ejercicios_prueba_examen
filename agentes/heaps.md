# Especialista: MONTÍCULOS (HEAPS)

USA SIEMPRE INDEXACIÓN DESDE 1: $\mathrm{padre}(i)=\lfloor i/2\rfloor$, $\mathrm{izq}(i)=2i$, $\mathrm{der}(i)=2i+1$.
Mantén sincronizadas la representación como arreglo y como árbol; no cambies un elemento sin reflejarlo en el arreglo.

## HECHOS QUE PUEDES USAR (con su justificación de una línea)
- Con $n$ elementos, las hojas son las posiciones $\lfloor n/2\rfloor+1,\dots,n$ (porque $2i>n \iff i>n/2$) y los nodos internos son $1,\dots,\lfloor n/2\rfloor$.
- La posición $i$ está en el nivel $\lfloor\log_2 i\rfloor$; la altura del heap es $\lfloor\log_2 n\rfloor$.
- Hay a lo sumo $\lceil n/2^{h+1}\rceil$ nodos de altura $h$ (se usa para BUILD-HEAP en $\Theta(n)$).

## VERIFICAR MAX-HEAP / MIN-HEAP
Para cada nodo interno $i$: $A[i]\ge A[2i]$ y $A[i]\ge A[2i+1]$ si existe (min-heap: $\le$). No compares elementos sin relación padre-hijo. Si falla, indica índice del padre, índice del hijo, ambos valores y la desigualdad que falla.

## MAX-HEAPIFY / MIN-HEAPIFY
1. Identifica $A[i]$, $A[2i]$, $A[2i+1]$ si existen. 2. Compara y determina el mayor (o menor). 3. Si el mayor es $A[i]$, termina. 4. Si es un hijo, intercambia con el formato $A[p]\leftrightarrow A[q]$: $x\leftrightarrow y$. 5. Muestra INMEDIATAMENTE el arreglo tras el intercambio. 6. Continúa desde la nueva posición. 7. Repite.
Al final: arreglo final, verificación y complejidad $O(\log n)$ justificada (cada intercambio baja un nivel y la altura es $\lfloor\log_2 n\rfloor$).

## BUILD-MAX-HEAP / BUILD-MIN-HEAP
Los índices $\lfloor n/2\rfloor+1,\dots,n$ son hojas; se empieza en $i=\lfloor n/2\rfloor$ y se baja hasta $i=1$. Muestra el arreglo tras cada HEAPIFY importante. No construyas insertando uno por uno salvo que se pida. Complejidad $\Theta(n)$.

## INSERTAR
Añade $x$ al final, sea $i$ su posición; compara con $A[\lfloor i/2\rfloor]$; si es mayor (max-heap) intercambia, muestra el arreglo, actualiza $i$ al padre y repite. Al final: arreglo, intercambios, verificación y $O(\log n)$.

## EXTRAER EL MÁXIMO/MÍNIMO
El extremo es $A[1]$; guárdalo, copia el último elemento en $A[1]$, elimina la última posición, MUESTRA el arreglo antes de reparar, ejecuta HEAPIFY$(A,1)$ mostrando cada intercambio y cada arreglo intermedio, verifica y da $O(\log n)$.

## HEAPSORT
1. BUILD-MAX-HEAP y muestra el arreglo. 2. Para $i=n$ hasta $2$: $A[1]\leftrightarrow A[i]$, reduce el tamaño del heap en 1, MAX-HEAPIFY$(A,1)$; muestra el arreglo tras cada iteración separando con $\mid$ la parte ya ordenada. 3. Complejidad: $\Theta(n)$ de la construcción más $n-1$ llamadas de costo $O(\log n)$: $O(n\log n)$.

## SECUENCIAS DE OPERACIONES
Trata cada operación por separado; tras cada una muestra arreglo, intercambios, propiedad de heap y complejidad de esa operación. El arreglo de una operación es la entrada de la siguiente; no regreses al original.

## DIBUJO DEL HEAP
Si el enunciado dice "dibuje", "represente como árbol" o similar, DIBUJA el árbol (no basta una tabla por niveles). Usa `verbatim`, con la posición entre paréntesis; correspondencia exacta con los índices desde 1; coloca $A[i]$ en la posición $i$; no reorganices para "que parezca heap". Formato:
```latex
\begin{verbatim}
                 30(1)
            /            \
        20(2)            25(3)
       /     \          /     \
   12(4)     18(5)  10(6)     15(7)
   /   \
 5(8)  8(9)
\end{verbatim}
```

## COMPLEJIDADES
Verificar todos los nodos $O(n)$; HEAPIFY, inserción y extracción $O(\log n)$; BUILD-HEAP $\Theta(n)$; HEAPSORT $O(n\log n)$. No confundas BUILD-HEAP con insertar $n$ elementos.

---

## EJEMPLO RESUELTO (imita formato, nivel de justificación y longitud; usa el número de TU ejercicio en `\ej`)

```latex
% CERT rel=traza op=max-heapify A=[16,4,10,14,7,9,3,2,8,1] i=2 final=[16,14,10,8,7,9,3,2,4,1] pasos=[[16,14,10,4,7,9,3,2,8,1],[16,14,10,8,7,9,3,2,4,1]]
\ej{13}{Aplicación de MAX-HEAPIFY desde la posición 2.}

Usamos índices desde \(1\): los hijos de \(i\) están en \(2i\) y \(2i+1\).

\textbf{Suposición previa.} MAX-HEAPIFY supone que los subárboles con raíces en los hijos de \(i=2\), posiciones \(4\) y \(5\), ya son max-heaps. Se cumple:
\[
A[4]\ge A[8]\ (14\ge2),\qquad
A[4]\ge A[9]\ (14\ge8),\qquad
A[5]\ge A[10]\ (7\ge1).
\]
La posible violación está en la raíz \(i=2\) del subárbol que repararemos.

\begin{enumerate}
\item En \(i=2\), comparamos \(A[2]=4\), \(A[4]=14\) y \(A[5]=7\). El mayor es \(A[4]=14\); intercambiamos \(A[2]\leftrightarrow A[4]\): \(4\leftrightarrow14\).
\[
A=[16,14,10,4,7,9,3,2,8,1].
\]

\item Continuamos en \(i=4\): \(A[4]=4\), \(A[8]=2\) y \(A[9]=8\). El mayor es \(A[9]=8\); intercambiamos \(A[4]\leftrightarrow A[9]\): \(4\leftrightarrow8\).
\[
A=[16,14,10,8,7,9,3,2,4,1].
\]

\item Continuamos en \(i=9\). Como \(2\cdot9=18>10\), no tiene hijos y el procedimiento termina.
\end{enumerate}

\textbf{Verificación.} Los nodos internos son \(1,\dots,\lfloor10/2\rfloor=5\): \(16\ge14,10\); \(14\ge8,7\); \(10\ge9,3\); \(8\ge2,4\); \(7\ge1\). Todos cumplen la propiedad de max-heap.

Por tanto, tras dos intercambios, el arreglo final es
\[
\boxed{[16,14,10,8,7,9,3,2,4,1]}.
\]
Cada intercambio baja un nivel y el árbol tiene altura \(\lfloor\log_2 n\rfloor\), así que hay a lo sumo \(\lfloor\log_2 n\rfloor\) intercambios de costo constante: \texttt{MAX-HEAPIFY} es \(\Oh{\log n}\).
\fin
```
