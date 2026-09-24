# Especialista: RECURRENCIAS

PRIMERA REGLA: identifica el método solicitado (sustitución/inducción, iteración, árbol, Teorema Maestro) y úsalo como método principal. NO lo reemplaces por el Teorema Maestro; si no te lo piden, el Teorema Maestro solo vale como verificación adicional al final.

Si divides entre $b$ repetidamente, di al inicio el supuesto que usas (p. ej. "suponemos $n=2^h$, $h\in\N\cup\{0\}$, para que las divisiones sean exactas").

## ITERACIÓN
1. Escribe la recurrencia original. 2. Primera expansión. 3. Segunda expansión. 4. Tercera si ayuda. 5. Patrón tras $k$ expansiones. 6. Determina $k$ con el caso base. 7. Sustituye $k$. 8. Evalúa la suma (escribe la fórmula de suma que usas: aritmética, geométrica, etc.). 9. Obtén la complejidad.
No escribas el patrón general si no es evidente a partir de las expansiones mostradas.

## T(n)=T(n-1)+f(n)
Desarrolla explícitamente $T(n)=T(n-2)+f(n-1)+f(n)=T(n-3)+f(n-2)+f(n-1)+f(n)=\dots$; tras $k$ pasos $T(n)=T(n-k)+[\dots]$; caso base $n-k=1\Rightarrow k=n-1$. No confundas $k$ (número de expansiones) con $n$.

## SUSTITUCIÓN (INDUCCIÓN)
1. Enuncia la conjetura con constantes: "$T(n)\le c\,g(n)$ para todo $n\ge n_0$" (o la fórmula exacta si se pide).
2. Caso(s) base: verifica numéricamente los valores de $n$ que el paso inductivo no cubre.
3. Hipótesis inductiva: "supongamos que se cumple para todo $m$ con $n_0\le m<n$".
4. Paso inductivo: sustituye la hipótesis en la recurrencia y llega a $T(n)\le c\,g(n)$, diciendo qué condición sobre $c$ (o $n$) se necesita y por qué se cumple.
5. Si la inducción falla por un término de orden menor, fortalece la hipótesis restando ese término ($T(n)\le c\,g(n)-d\cdot(\text{término})$) y explica por qué.
6. Concluye con las constantes elegidas.

## ÁRBOL DE RECURRENCIA
Para $T(n)=aT(n/b)+f(n)$ analiza por nivel: nivel $i$ tiene $a^i$ nodos, tamaño $n/b^i$, costo por nodo $f(n/b^i)$, costo total $a^if(n/b^i)$. Si se pide dibujar, dibuja 2–3 niveles indicando el tamaño dentro de los nodos.
Altura: $n/b^h=1\Rightarrow h=\log_b n$. Hojas: $a^h=n^{\log_b a}$.
Costo total: suma de los costos por nivel más las hojas. Di explícitamente si el costo por nivel aumenta, se mantiene o disminuye, y qué niveles dominan. No escribas solo "por Teorema Maestro".

## TEOREMA MAESTRO (solo si se pide o como verificación)
Para $T(n)=aT(n/b)+f(n)$ con $a\ge1$, $b>1$:
1. Identifica $a$, $b$, $f(n)$ y calcula $n^{\log_b a}$.
2. Compara $f(n)$ con $n^{\log_b a}$ y di qué caso aplica, con el $\varepsilon>0$ explícito:
   - Caso 1: $f(n)\in\Oh{n^{\log_b a-\varepsilon}}\Rightarrow T(n)\in\Th{n^{\log_b a}}$.
   - Caso 2: $f(n)\in\Th{n^{\log_b a}}\Rightarrow T(n)\in\Th{n^{\log_b a}\log n}$.
   - Caso 3: $f(n)\in\Om{n^{\log_b a+\varepsilon}}$ y regularidad $a\,f(n/b)\le k\,f(n)$ con $k<1$ para $n$ grande (verifícala) $\Rightarrow T(n)\in\Th{f(n)}$.
3. Si ningún caso aplica (p. ej. $f(n)=n\log n$ con $n^{\log_b a}=n$), dilo y usa otro método.

## CERTIFICADOS
Una solución de recurrencia lleva normalmente dos: `% CERT rel=rec ...` (fórmula cerrada contra la recurrencia real) y `% CERT rel=Theta ...` (o `rel=O`) con las constantes.

---

## EJEMPLO RESUELTO (imita formato, nivel de justificación y longitud; usa el número de TU ejercicio en `\ej`)

```latex
% CERT rel=rec a=2 b=2 f=n T1=1 cerrada=n*log2(n)+n
% CERT rel=Theta f=n*log2(n)+n g=n*log2(n) c1=1 c2=2 n0=2
\ej{8}{Árbol de recurrencia para $T(n)=2T(n/2)+n$, con $T(1)=1$.}

Suponemos $n=2^h$, con $h\in\N\cup\{0\}$, para que las divisiones lleguen exactamente al caso base.

\begin{enumerate}
\item \textbf{Construcción del árbol.} Cada nodo de tamaño $m>1$ tiene dos hijos de tamaño $m/2$ y costo propio $m$. Los tamaños de los primeros niveles son:
\begin{verbatim}
                 [n]
              /       \
          [n/2]       [n/2]
          /   \       /   \
      [n/4] [n/4] [n/4] [n/4]
        ...   ...   ...   ...
\end{verbatim}

\item \textbf{Costo por nivel.} La raíz está en el nivel $0$. En cada nivel se duplica el número de nodos y se divide entre $2$ el tamaño:
\[
\begin{array}{c|c|c|c|c}
\text{Nivel}&\text{Nodos}&\text{Tamaño}&\text{Costo por nodo}&\text{Costo total}\\ \hline
0&1&n&n&n\\
1&2&n/2&n/2&n\\
2&4&n/4&n/4&n\\
i<h&2^i&n/2^i&n/2^i&2^i(n/2^i)=n\\
h&2^h&1&T(1)=1&2^h=n
\end{array}
\]
El costo total se mantiene en $n$ por nivel; todos los niveles contribuyen por igual.

\item \textbf{Altura y hojas.} Las hojas tienen tamaño $1$, por lo que
\[
\frac{n}{2^h}=1\;\Rightarrow\;2^h=n\;\Rightarrow\;h=\log_2 n.
\]
Así, la altura es $\log_2 n$, hay $h+1=\log_2 n+1$ niveles y $2^h=n$ hojas.

\item \textbf{Costo total.} Sumamos los $h$ niveles internos y el costo de las hojas:
\[
T(n)=\sum_{i=0}^{h-1}2^i\frac{n}{2^i}+2^hT(1)
=\sum_{i=0}^{h-1}n+n
=hn+n
=n\log_2 n+n.
\]
Para $n=1$, la suma interna es vacía y la fórmula da $T(1)=1$, como se requiere.

\item \textbf{Orden.} Para $n\ge2$ se cumple $\log_2 n\ge1$; multiplicando por $n>0$: $n\le n\log_2 n$. Sumando $n\log_2 n$ a ambos lados:
\[
0\le n\log_2 n\le n\log_2 n+n\le2n\log_2 n,
\]
es decir, $0\le n\log_2 n\le T(n)\le 2n\log_2 n$. Por tanto, podemos tomar $c_1=1$, $c_2=2$ y $n_0=2$.
\end{enumerate}

Concluimos que $\boxed{T(n)=n\log_2 n+n\in\Th{n\log_2 n}}$, para $n$ potencia de $2$.
\fin
```
