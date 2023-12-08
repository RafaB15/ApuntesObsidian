### $O(1)$

- Complejidad constante.
- No importa lo que se provea como input, este se ejecutará siempre en la misma cantidad de tiempo.
    1. 1 elemento, 1 segundo.
    2. 2 elementos, 1 segundo.
    3. 3 elementos, 1 segundo.

### $O(log \ n)$

- Complejidad logarítmica.
- El tiempo de cálculo se incrementa lentamente. Según la cantidad de datos de input se incrementa exponencialmente.
    1. 1 elemento, 1 segundo.
    2. 10 elementos, 2 segundos.
    3. 100 elementos, 3 segundos.
- Ejemplo: La búsqueda binaria.

### $O(n)$

- Complejidad lineal.
- El tiempo de cálculo se incrementa al mismo ritmo de cantidad de datos de input.
    1. 1 elemento, 1 segundo.
    2. 10 elementos, 10 segundos.
    3. 100 elementos, 100 segundos.
- Ejemplo: La búsqueda lineal.

### $O(n^2)$

- Complejidad cuadrática.
- El tiempo de cálculo se incrementa al mismo ritmo de $n^2$ de datos de input:
    1. 1 elemento, 1 segundo.
    2. 10 elementos, 100 segundos.
    3. 100 elementos, 10000 segundos.
- Ejemplo: El burbujeo.

### $O(n!)$

- Complejidad factorial.
- El tiempo de cálculo se incrementa al mismo ritmo de $n!$ donde n es la cantidad de datos de input.
    1. 1 elemento, 1 segundo.
    2. 10 elementos, 3628800 segundos.
    3. 100 elementos, 9,332621544 × 10157 segundos.
- Ejemplo: El problema del Viajante.