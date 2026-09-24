# Formato del archivo .tex

Tu `.tex` lo compila a PDF una computadora local con una plantilla fija. Tú no compilas: escribe SOLO el cuerpo LaTeX, sin `\documentclass`, sin `\usepackage`, sin `\begin{document}` y sin bloques de código.

## Estructura del archivo
1. Líneas `% CERT ...` al inicio, si aplican (ver abajo).
2. `\ej{<número>}{<enunciado breve>}`: el número es el campo `numero` de `clasificacion.json` (p. ej. `5` o `5b`).
3. La solución, con el estilo de `global.md` y de tu especialista.
4. Termina con `\fin`.

## Lo que está disponible
- Paquetes: `amsmath`, `amssymb`, `xcolor`. No hay más: nada de `tikz`, `algorithm`, `listings`, etc.
- Macros (no las redefinas): `\Oh{x}` = O(x), `\Om{x}` = Ω(x), `\Th{x}` = Θ(x), `\oh{x}` = o(x), `\om{x}` = ω(x), `\N`, `\R`, `\V` = (V), `\F` = (F), `\fin` = ∎, `\por{texto}` = justificación en gris, `\idea{texto}` = recuadro.
- Dibujos (árboles, heaps): entorno `verbatim`. Tablas: `tabular` o `array`.
- Los símbolos Unicode comunes (≤ ≥ ∈ ⇒ ∀ ∃ ∞ ⌊ ⌋ …) compilan, pero prefiere los comandos LaTeX.

## Errores que rompen la compilación (evítalos)
- Un renglón que empieza con `[` justo después de `\\`: LaTeX lo toma como argumento opcional. Escribe `{}[` o reordena la línea.
- Cada `\[` necesita su `\]`; cada `\begin{...}` su `\end{...}`; las llaves deben estar balanceadas.
- `_` y `^` solo en modo matemático (`$n_0$`, no `n_0`). El `%` literal se escribe `\%`; `&` solo dentro de `tabular`, `array` o `align`.
- `verbatim` nunca dentro del argumento de otro comando (`\textbf{}`, `\idea{}`, `\por{}`, `\ej{}`).
- No uses `\newcommand` ni `\usepackage`.

## Certificados `% CERT` (se verifican numéricamente de forma automática)
Una línea por afirmación que tenga constantes, límite, fórmula cerrada o traza. No dejes espacios dentro de las expresiones. `n` es la variable. Funciones: `log2 log sqrt factorial floor ceil max min`. Fracciones exactas como `1/14`.
```
% CERT rel=O      f=4*n**2+3*n+10 g=n**2 c=17 n0=1
% CERT rel=Omega  f=5*n**2-2*n g=n**2 c=3 n0=1
% CERT rel=Theta  f=... g=... c1=... c2=... n0=...
% CERT rel=o      f=n g=n**2 n0=floor(1/c)+1          (n0 en función de c)
% CERT rel=omega  f=n**2 g=n n0=floor(c)+1
% CERT rel=notO   f=n**2 g=n w=max(n0,floor(c))+1     (testigo en función de c y n0)
% CERT rel=lim    f=n*log2(n) g=n**1.5 L=0            (L = 0, un número o oo)
% CERT rel=rec    a=2 b=2 f=n T1=1 cerrada=n*log2(n)+n        (T(n)=a*T(n/b)+f(n))
% CERT rel=rec    dec=1 f=n T1=1 cerrada=n*(n+1)/2            (T(n)=T(n-1)+f(n))
% CERT rel=traza  op=max-heapify A=[16,4,10,14,7,9,3,2,8,1] i=2 final=[...] pasos=[[...],[...]]
```
Operaciones de traza: `max-heapify` y `min-heapify` (con `i`), `build-max-heap`, `build-min-heap`, `insert-max` e `insert-min` (con `x`), `extract-max` y `extract-min`. `pasos` es el arreglo tras cada intercambio; en las construcciones, tras cada llamada a HEAPIFY; en la extracción, el primer paso es el arreglo tras mover el último elemento a la raíz. Sin espacios dentro de los corchetes. Índices desde 1.
Si no hay certificado posible (una demostración general), omite las líneas `% CERT`.
