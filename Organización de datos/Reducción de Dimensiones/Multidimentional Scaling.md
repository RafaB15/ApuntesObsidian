1. Elevar la matriz de distancias al cuadrado.
2. Centrar la matriz para que las filas y columnas tengan promedio cero.
3. Calculamos la SVD de la matriz.
4. Las primeras **k** columnas de $U$ dan las coordenadas para los puntos reducidos.

### Motivación para lo que sigue

1. En teoría de grafos hay un problema conocido que trata de hallar el corte más “esparso”.
2. Una aproximación es analizando la matriz de adyacencia.
3. Definimos el Laplaciano del grafo L = D * A.
    1. D: matriz diagonal con los grados.
    2. A: matriz de adyacencia.
4. El laplaciano tiene muchísimas propiedades
    1. El autovalor más pequeño es 0
    2. Si tiene multiplicidad > 1, el grafo no es conexo.
5. ***Teorema:*** usando el AVE no nulo más pequeño podemos asignar a cada nodo del grafo un valor: según eso, ordenarlos y establecer el corte más esparso entre dos grupos.

## Laplacian eigenmaps

- Vamos a aprovechar esto para poder reducir las dimensiones.
    - Esos AVES nos permiten capturar diferenciar bien los nodos (simil “capturar varianza” en PCA).
- En esencia:
    - Contruimos un grafo a partir de nuestro puntos.
    - Calculamos el laplaciano.
    - Si queremos k dimensiones, usamos k AVEs.
- Bonus: este método es no lineal

Ahora sí, el método:

1. Armamos una matriz de adyacencias con los v vecinos más cercanos.
2. Asginamos pesos a esas aristas con un kernel RBF: 

![[Organización de datos/Reducción de Dimensiones/Multidimentional Scaling/Untitled.png|Untitled]]

1. Calculamos el laplaciano: L = D - A
2. Hacemos descomposición espectral: tomamos los k autovectores más chicos (pero ignorando el autovalore 0) y asignamos los elementos a los nodos correspondientes.

El hecho de que no sea lineal permite, a veces, mejores resultados.