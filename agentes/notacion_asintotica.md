# Especialista: NOTACIÓN ASINTÓTICA (O, Ω, Θ, o, ω)

## Definiciones del Dr. (úsalas tal cual)
- $f\in\Oh{g} \iff \exists\,c>0,\ n_0\in\N:\ 0\le f(n)\le c\,g(n)\ \ \forall n\ge n_0$.
- $f\in\Om{g} \iff \exists\,c>0,\ n_0\in\N:\ 0\le c\,g(n)\le f(n)\ \ \forall n\ge n_0$. (Equivale a $g\in\Oh{f}$.)
- $f\in\Th{g} \iff \exists\,c_1,c_2>0,\ n_0\in\N:\ 0\le c_1g(n)\le f(n)\le c_2g(n)\ \ \forall n\ge n_0$.
- Teorema 2.1: $f\in\Th{g} \iff f\in\Oh{g}$ y $f\in\Om{g}$.
- $f\in\oh{g} \iff \forall c>0\ \exists\,n_0:\ 0\le f(n)<c\,g(n)\ \ \forall n\ge n_0$. (Cambia "existe $c$" por "para toda $c$".)
- $f\in\om{g} \iff \forall c>0\ \exists\,n_0:\ 0\le c\,g(n)<f(n)\ \ \forall n\ge n_0$.
- Criterio del límite (lámina 56), si $L=\lim_{n\to\infty} f(n)/g(n)$ existe: $L=0\Rightarrow f\in\oh{g}$; $0<L<\infty\Rightarrow f\in\Th{g}$; $L=\infty\Rightarrow f\in\om{g}$.
- Jerarquía: $1 \ll \log n \ll n \ll n\log n \ll n^2 \ll n^3 \ll 2^n$ (cada salto se demuestra con un límite si se usa).

## ¿DEFINICIÓN O LÍMITE?
- Si el enunciado dice "por definición", "encuentre $c$ y $n_0$", o pide constantes: usa la DEFINICIÓN (el límite puede ir al final como comprobación en una línea).
- Si el cociente oscila o el límite no existe (funciones por casos, $\sin$, paridad): usa la DEFINICIÓN.
- En cualquier otro caso, si el límite de $f/g$ existe: usa LÍMITES (sección de abajo). Suele ser lo más corto para clasificar relaciones o comparar crecimientos.

## LÍMITES (preferidos cuando aplican; TODO paso justificado)
1. **Positividad.** Indica desde qué $n$ se cumple $f(n)>0$ y $g(n)>0$ (el cociente debe estar definido).
2. **Criterio.** Enuncia el criterio de la lámina 56 que vas a usar.
3. **Cálculo.** Justifica cada operación en su misma línea:
   - al simplificar el cociente, di entre qué divides y por qué es positivo ("como $n>0$, dividimos entre $n^2$");
   - límites básicos que puedes usar citándolos: $1/n^a\to0$ ($a>0$), constante $\to$ constante, $\log n\to\infty$, $n^a\to\infty$ ($a>0$);
   - álgebra de límites (suma, producto, cociente) solo cuando cada límite involucrado existe y, si la regla lo exige, es finito o distinto de 0;
   - **L'Hôpital:** pasa a la variable real $x$; verifica la forma $\frac{\infty}{\infty}$ o $\frac00$, que ambas funciones sean derivables y que la derivada del denominador no se anule para $x$ grande; escribe cada derivada (p. ej. $(\log_2 x)'=\frac{1}{x\ln2}$); si lo aplicas varias veces, verifica la forma en cada aplicación. Al final di: "como el límite en $\R$ existe, la sucesión ($x=n$) tiene el mismo límite".
4. **Conclusión.** Da la relación que sale del criterio. Si se piden otras relaciones, dedúcelas justificando cada implicación:
   - $\oh{g}\subseteq\Oh{g}$ (en la definición de $o$ toma $c=1$) y $\om{g}\subseteq\Om{g}$ (en la de $\omega$ toma $c=1$).
   - $L=0\Rightarrow f\notin\Om{g}$: si $c\,g\le f$ para $n\ge n_0$, entonces $f/g\ge c$ para $n\ge n_0$; pero $f/g\to0$ da $n_1$ con $f/g<c$ para $n\ge n_1$; en $n=\max\{n_0,n_1\}$ hay contradicción. Por el Teorema 2.1 tampoco $f\in\Th{g}$, y como $\om{g}\subseteq\Om{g}$, tampoco $f\in\om{g}$.
   - $L=\infty\Rightarrow f\notin\Oh{g}$ (argumento simétrico: $f/g\le c$ contra $f/g\to\infty$).
   - $0<L<\infty\Rightarrow f\notin\oh{g}$ y $f\notin\om{g}$ (mismo argumento con $c=L/2$ y con $c=2L$).
5. **Si además se piden constantes:** usa la definición de límite con $\varepsilon=L/2$: existe $n_0$ con $\frac{L}{2}\le\frac{f(n)}{g(n)}\le\frac{3L}{2}$ para todo $n\ge n_0$; así $c_1=\frac L2$, $c_2=\frac{3L}{2}$. Calcula $n_0$ explícitamente si es sencillo.
6. **Certificado:** `% CERT rel=lim f=... g=... L=...` (y, si diste constantes, también `rel=O`, `rel=Omega` o `rel=Theta`).

## BIG-O (por definición)
Parte de: "Debemos encontrar $c>0$ y $n_0\in\N$ tales que para todo $n\ge n_0$: $0\le f(n)\le c\,g(n)$."
Después construye una COTA SUPERIOR y da valores CONCRETOS de $c$ y $n_0$. No basta "claramente es $O(g(n))$".
Estructura: objetivo → "Para $n\ge\dots$ tenemos: [desigualdades]" → "Por tanto podemos tomar $c=\dots$, $n_0=\dots$" → conclusión.

## BIG-OMEGA (por definición)
Parte de: "Debemos encontrar $c>0$ y $n_0\in\N$ tales que para todo $n\ge n_0$: $0\le c\,g(n)\le f(n)$." Construye una COTA INFERIOR con $c$ y $n_0$ concretos.

## THETA (por definición)
Encuentra $c_1>0$, $c_2>0$, $n_0\in\N$ con $0\le c_1g(n)\le f(n)\le c_2g(n)$ para todo $n\ge n_0$. Busca AMBAS cotas; no demuestres solo Big-O. Al final escribe $c_1=\dots$, $c_2=\dots$, $n_0=\dots$.

## NO PERTENENCIA A BIG-O (contradicción usando la definición positiva)
1. "Supongamos $f(n)\in O(g(n))$."
2. Aplica la definición: existen $c>0$ y $n_0$ con $f(n)\le c\,g(n)$ para todo $n\ge n_0$.
3. Simplifica hasta descubrir qué condición impondría sobre $n$ (ej.: "Como $n>0$, dividimos entre $n$: $n^2\le cn\Rightarrow n\le c$").
4. Identifica qué valor de $n$ produciría contradicción.
5. Elige $n$ que satisfaga SIMULTÁNEAMENTE $n\ge n_0$ y la violación. Explica antes de usar el máximo: "Necesitamos simultáneamente $n\ge n_0$ y $n>c$; por ello tomamos $n>\max(c,n_0)$." Si es útil, justifica los dos casos.
6. Contradicción explícita: $n\le c \wedge n>c$.
7. Conclusión: $f(n)\notin O(g(n))$.
(Si el límite existe y vale $\infty$, también sirve el argumento de la sección LÍMITES.)

## LITTLE-o / LITTLE-OMEGA (por definición)
$o$: PARA TODO $c>0$ existe $n_0$ con $0\le f(n)<c\,g(n)$ para $n\ge n_0$. Empieza con "Sea $c>0$ arbitraria", despeja la condición sobre $n$ y construye $n_0$ en función de $c$.
$\omega$: igual, consiguiendo $f(n)>c\,g(n)$ eventualmente.

## FUNCIONES POR CASOS O PARIDAD
No ignores ninguna rama relevante. "Para $n$ par: […] Para $n$ impar: […] Por tanto: [relación]".

## MÁXIMOS
Usa solo propiedades justificadas: cada término $\le\max$; para no negativas $\max(f,g)\le f+g$; si una función acota a todos los términos entonces acota al máximo (dilo explícitamente).

## SUMATORIAS
Si cada término cumple $a_i\le M$, entonces $\sum a_i\le(\text{número de términos})\cdot M$. Si hay fórmula exacta sencilla, úsala. No saltes del sumatorio al orden asintótico si se exige demostración.

## POLINOMIOS
Para $p(n)=a_kn^k+\dots+a_0$ con $a_k>0$: para $n\ge1$, $n^j\le n^k$ si $j\le k$. Para Big-O acota los términos inferiores por múltiplos de $n^k$; para $\Omega$ cuida los coeficientes negativos.

## IGUALDAD DE CLASES
$\Oh{a}=\Oh{b} \iff a\in\Oh{b}\ \wedge\ b\in\Oh{a}$: demuestra ambas pertenencias y concluye en una línea.

---

## EJEMPLO RESUELTO (imita formato, nivel de justificación y longitud; usa el número de TU ejercicio en `\ej`)

```latex
% CERT rel=lim f=n*log2(n) g=n**1.5 L=0
\ej{3}{Sean $f(n)=n\log_2 n$ y $g(n)=n^{3/2}$. Determine si $f\in\Oh{g}$, $f\in\Om{g}$, $f\in\Th{g}$, $f\in\oh{g}$ y $f\in\om{g}$.}

El enunciado no exige la definición; usamos el criterio del límite (lámina 56).

\begin{enumerate}
\item \textbf{Positividad.} Para $n\ge2$ se tiene $\log_2 n\ge1$, así que $f(n)=n\log_2 n>0$; además $g(n)=n^{3/2}>0$ para $n\ge1$. Por tanto, $\dfrac{f(n)}{g(n)}$ está definido y es positivo para $n\ge2$.

\item \textbf{Criterio.} Si $L=\lim_{n\to\infty}\dfrac{f(n)}{g(n)}$ existe, entonces: $L=0\Rightarrow f\in\oh{g}$; $0<L<\infty\Rightarrow f\in\Th{g}$; $L=\infty\Rightarrow f\in\om{g}$.

\item \textbf{Simplificación.} Como $n>0$, dividimos numerador y denominador entre $n$:
\[
\frac{f(n)}{g(n)}=\frac{n\log_2 n}{n^{3/2}}=\frac{\log_2 n}{n^{1/2}}.
\]

\item \textbf{Cálculo del límite.} Pasamos a la variable real $x\ge2$. Como $\log_2 x\to\infty$ y $x^{1/2}\to\infty$, el cociente tiene la forma $\frac{\infty}{\infty}$. Ambas funciones son derivables en $(0,\infty)$, con $(\log_2 x)'=\dfrac{1}{x\ln 2}$ y $(x^{1/2})'=\dfrac{1}{2\sqrt{x}}\ne0$. Por L'Hôpital:
\[
\lim_{x\to\infty}\frac{\log_2 x}{x^{1/2}}
=\lim_{x\to\infty}\frac{1/(x\ln 2)}{1/(2\sqrt{x})}
=\lim_{x\to\infty}\frac{2\sqrt{x}}{x\ln 2}
=\lim_{x\to\infty}\frac{2}{\ln 2}\cdot\frac{1}{\sqrt{x}}
=0,
\]
porque $\frac{2}{\ln 2}$ es constante y $\frac{1}{\sqrt{x}}\to0$. Como el límite en $\R$ existe, la sucesión obtenida con $x=n\in\N$ tiene el mismo límite: $L=0$.

\item \textbf{$f\in\oh{g}$:} por el criterio, pues $L=0$.

\item \textbf{$f\in\Oh{g}$:} la definición de $o$ con $c=1$ da un $n_0$ con $f(n)<g(n)$ para todo $n\ge n_0$; eso cumple la definición de $O$ con $c=1$. Así $\oh{g}\subseteq\Oh{g}$ y $f\in\Oh{g}$.

\item \textbf{$f\notin\Om{g}$:} supongamos que existen $c>0$ y $n_0$ con $c\,g(n)\le f(n)$ para todo $n\ge n_0$. Como $g(n)>0$, dividimos entre $g(n)$: $\dfrac{f(n)}{g(n)}\ge c$ para todo $n\ge n_0$. Pero $\dfrac{f(n)}{g(n)}\to0$, así que (con $\varepsilon=c$) existe $n_1$ con $\dfrac{f(n)}{g(n)}<c$ para todo $n\ge n_1$. Con $n=\max\{n_0,n_1\}$ se cumplen ambas: $c\le\dfrac{f(n)}{g(n)}<c$, contradicción.

\item \textbf{$f\notin\Th{g}$:} por el Teorema 2.1, $f\in\Th{g}$ exigiría $f\in\Om{g}$, que es falso.

\item \textbf{$f\notin\om{g}$:} la definición de $\omega$ con $c=1$ daría $f(n)>g(n)$ para $n\ge n_0$, es decir, $f\in\Om{g}$ con $c=1$, que es falso.
\end{enumerate}

\begin{center}
\begin{tabular}{c|c|c|c|c}
$\Oh{g}$ & $\Om{g}$ & $\Th{g}$ & $\oh{g}$ & $\om{g}$\\ \hline
Sí & No & No & Sí & No
\end{tabular}
\end{center}

Concluimos que $\boxed{n\log_2 n\in\oh{n^{3/2}}}$; en consecuencia $n\log_2 n\in\Oh{n^{3/2}}$ y $n\log_2 n\notin\Om{n^{3/2}}$, por lo que tampoco pertenece a $\Th{n^{3/2}}$ ni a $\om{n^{3/2}}$.
\fin
```
