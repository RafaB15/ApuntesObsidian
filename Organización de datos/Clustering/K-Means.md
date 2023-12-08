- Dado un set de puntos en $R^d$.
- Particionar los puntos en k sets (k<d)
- De forma tal de minimizar la sumatoria de las distancias de cada punto al centro del cluster.

![[Organización de datos/Clustering/K-Means/Untitled.png|Untitled]]

### Complejidad del problema:

Es NP-Hard en $R^d$ incluso para k=2.

Es NP-Hard en $R^2$ para cualquier K

Esto es malo, pero afortunadamente existen heurísitcas muy buenas que son las que se conocen como K means.

# Algoritmo:

1. Elegir k puntos, uno para cada cluster.
    1. Inicialmente los centroides de cada cluster son esos puntos.
2. Asignarle a cada punto el cluster con centroide más cercano.
3. Re calcular los centroides como el promedio de los puntos.
4. Volver a 2

## Problema de la inicialización: k-means++

Como k-means es muy sensible a los puntos iniciales, lso elegimos de la siguiente manera si queremos mayor eficiencia.

1. Elegir un punto al azar como centroide.
2. Calcular la distancia de cada punto contra los centroides y quedarse con la mínima.
3. Calcular la probabilidad de cada punto, como la distancia dividida por la suma de todas las distancias de los puntos.
4. Elegir un nuevo punto al azar, utilizando la probabilidad calculada.
5. Repetir hasta tener k centroides.

## k-Means online

- O(k) en memoria.
- Puede procesar puntos ilimitados ⇒ streams!
- Algoritmo:
    1. Inicializar k centroides al azar.
    2. Para cada punto que viene:
        1. Asignar al centroide más cercano.
        2. Aumentar el contador del cluster.
        3. Mover proporcionalmente el centroide.

![[Organización de datos/Clustering/K-Means/Untitled 1.png|Untitled]]

## K-means como algoritmo de compresión:

Podemos reducir el detalle de una imagen utilizando menos colores a través de “puntos de representación”.

![[Organización de datos/Clustering/K-Means/Untitled 2.png|Untitled]]

## K-Means trick

K-means puede usarse para reducir las dimensiones de un set de puntos.

- Correr k-means con algún k.
- Y ahora computar la distancia de cada punto a cada uno de los k-centroides.
- El resultado es que cada punto queda convertido a k dimensiones!

Muchos problemas de clasificación pueden resolverse aplicando k-means trick y luego un simple clasificador lineal.