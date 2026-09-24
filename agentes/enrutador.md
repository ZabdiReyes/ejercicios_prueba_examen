# Rol: ENRUTADOR (ingesta del examen)

Lo ejecuta un modelo potente que lee el PDF del examen COMPLETO y en formato PDF (sin OCR). Produce dos archivos en `agentes/` (y copia el PDF como `agentes/examen.pdf`).

## 1. `enunciados.tex`
Transcripción fiel de cada ejercicio (texto, datos, arreglos y figuras descritas con precisión), un bloque por unidad de trabajo:
```latex
%<ej05>
\enunciado{5}{<título corto>}
<texto completo del enunciado en LaTeX>
%</ej05>
```
Separa un inciso en su propio bloque (`ej05a`, `ej05b`, con `\enunciado{5a}{...}`) solo si es independiente y largo. Si los incisos comparten datos o son cortos, van juntos.

## 2. `clasificacion.json`
Lista en el orden del examen:
```json
[{"id": "ej05", "numero": "5", "categoria": "heaps", "dificultad": "media", "asignado": "nube",
  "nota": "pide dibujar el árbol después de cada inserción"}]
```
- `categoria`: `notacion_asintotica` (O, Ω, Θ, o, ω, límites, jerarquías, propiedades de clases), `recurrencias` (iteración, sustitución/inducción, árbol, Teorema Maestro) o `heaps` (verificar, heapify, build, insertar, extraer, heapsort, dibujos).
- `dificultad` → `asignado`:
  - `facil` → `local`: un procedimiento directo y corto (una relación entre polinomios, un límite directo, una traza corta, una recurrencia estándar con el método indicado).
  - `media` → `nube`: varias partes o técnicas combinadas, trazas largas o secuencias de operaciones, un árbol de recurrencia completo, L'Hôpital repetido, funciones por casos.
  - `dificil` → `codex`: demostraciones generales (propiedades para toda $f$, $g$), "demuestre o refute", contraejemplos, correctitud o invariantes, recurrencias no estándar y todo lo que tenga una trampa.
- Equilibrio: los agentes locales trabajan de dos en dos. Si hay más de 4 fáciles, manda los excedentes a `nube`.
- `nota`: trampas o requisitos fáciles de olvidar (una hipótesis que falla, un método obligatorio, "dibuje", la base del logaritmo, índices desde 0 en el enunciado, etc.). Omítela si no hay nada que advertir.
