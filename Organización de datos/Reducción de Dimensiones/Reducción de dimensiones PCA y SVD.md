# Analisis de componentes principales: PCA

- Método lineal.
- Queremos encontrar las ***componentes*** que maximicen la varianza de los datos.
    - Para datos en m dimensiones originales, obtenemos m componentes ortogonales.
    - La clave es que están ordenadas según maximizan la varianza (ej. podemos quedarnos con las primeras 2).
- Una componente es un vector  $\implies$CL de las dimensiones originales).

![[Organización de datos/Reducción de Dimensiones/Reducción de dimensiones PCA y SVD/Untitled.png|Untitled]]

- Podemos centrar los datos de antemano (🧦 = 0)
- Las componentes que PCA nos da son vectores ***unitarios ($\|w\|=1$)**

$$
\implies \sum_i(x_{(i)}.w)^2
$$

- Efectivamente la primer componente principal maximiza esto:

$$
w_{(1)} = \text{arg max}_{\|w\| = 1}\sum_i(x_{(i)}.w)^2
$$

Un poco de magia

$$
w_{(1)} = \text{arg max}_{\|w\| = 1}\|Xw\|^2 = \text{arg max}_{\|w\| = 1} w^T X^T Xw
$$

- El $w_1$ que maximiza la ecuación anterior es el autovector con autovalor más grande de $x^T x$.
- Para obtener $w_k$, la ecuación es la misma, solo que restamos los primeros $w_1,...,w_{k-1}$ a los datos.
- Resulta que también $w_k$ es el autovector de $x^Tx$ cuyo autovalor es el k-más-alto.
    - E.g. w_2 es el segundo autovector de $x^Tx$

## Método de PCA a través de la covarianza:

Para una matriz de datos x:

1. Centramos las columnas, i.e. a cada columna le restamos el promedio de sus valores.
2. (Opcional) Dividir cada elemetno por la desviación estándar ($\sqrt{Varianza}$) de su columnas.
3. Calcular la matriz de covarianza

$$
\frac{1}{n-1}X^TX
$$

El n-1 es un truquito estadístico (Corrección de Bessel)

La matriz de covarianza nos da información interesante sobre los features.

1. Ordenamos los autovectores de la matriz de covarianza según sus autovalores, de mayor a menor, esos son los componentes principales.

## Interpretación de un biplot

- Podemos proyectar los puntos
- Pero también las dimensiones!
    - Son los vectores unitarios
    
    ![[Organización de datos/Reducción de Dimensiones/Reducción de dimensiones PCA y SVD/Untitled 1.png|Untitled]]
    

## ¿Cuántas dimensiones necesitamos?

![[Organización de datos/Reducción de Dimensiones/Reducción de dimensiones PCA y SVD/Untitled 2.png|Untitled]]

La idea de PCA sería entonces obtener dentro de ese espacio m dimensional los vectores sobre los que puedo proyectar los datos y capturar la mayor dispersión posible. El objetivo es analizar cuantos componentes son necesarios para distribuir bien los datos.

## Reducción de dimensiones con SVD

Recordemos la relación 

$$
XV=Y\varSigma
$$

Esto nos dice que proyectar los datos con V es lo mismo que escalar U con los valores singulares.

Si usamos la versión reducida de la SVD $U_r \varSigma_r$ es una reducción a **r** dimensiones de los datos originales.

## Teorema: SVD = PCA

Observamos que V tiene los autovectores de  $X^TX$.

En la aproximación de rango ***r*** nos quedamos con las primeras r columnas de $U, \varSigma$ y $V$. Como están ordenados según los valores singulares nos quedamos con los AVEs más importantes.

$\implies \text{Hacer XV es PCA}$

$\implies \text{Hacer } U_r\varSigma_r \text{ es PCA}$

Esto funciona si teníamos centrada la matriz antes.

Cuando con un paquete hacemos PCA, internamente se realiza la SVD porque es más estable numéricamente.