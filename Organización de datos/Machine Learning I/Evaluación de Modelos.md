# Evaluando el modelo:

- Error de entrenamiento
    - Entrenamos con el train-set y luego hacemos predicciones para ese mismo train-set evaluando la métrica que elegimos.
- Error de test
    - Entrenamos con el train-set y luego hacemos predicciones para el test-set evaluando la métrica que elegimos.

# ¿Qué es entrenar?

- El entrenamiento de un modelo es un problema de optimización.
- Buscamos los parámetros óptimos para minimizar o maximizar la métrica elegida.
- Dependiendo del modelo varía la técnica de optimización a usar.

# Modelo ya entrenado

- Un modelo ya entrenado queda representado por sus parámetros.
- Por ejemplo si entrenamos un polinomio de grado 2 el resultado son los coeficientes del polinomio.

# Hiper-Parámetros

- Los hiper-parámetros son valores que parametrizan el entrenamiento del modelo.
- Son valores que debemos indicar por afuera, no son parte del proceso de optimización del modelo.

## Búsqueda de hiperparámetros:

- Ejemplos:
    - **Polinomios**: grado del polinomio.
    - **Árboles de decisión:** Profundidad máxima, cantidad mínima de nodos por hoja, etc.
    - **Redes Neuronales:** Cantidad de capas, cantidad de neuronas en cada capa, función de activación a usar, dropout, método de optimización a usar, etc.
    - **KNN:** Cantidad de vecinos a evaluar, distancia a emplear.
    - **Random Forests:** Cantidad de árboles a usar, cantidad de atributos a usar, etc.
    - ***Gradient Boosting:*** Número de estimadores, gamma, factor de aprendizaje, profundidad máxima, subsample de rows y columnas, etc.
    - Necesitamos encontrar el conjunto óptimo de hiper-parámetros para luego encontrar el modelo (parámetros) óptimo.
    - A la búsqueda de hiper-parámetros se la conoce también como “tuning”.
    - En algunos modelos el proceso de “tuning” es más crítico que en otros.
    - Los métodos más comunes son:
        - Grid-Search
        - Random-Search
        - Optimización Bayesiana

### Grid-Search:

- Establecemos un conjunto de valores a probar por cada hiper-parámetro.
- Ejemplo: grado del polinomio {2,3,4} y factor de regularización {0,0.05,1}.
- Probamos cada combinación de hiper-parámetros y nos quedamos con la mejor.
- En nuestro ejemplo son 3*3 = 9 casos.
- Una vez que encontramos los valores óptimos podemos refinar la búsqueda.
- Por ejemplo si el óptimo está en un extremo deberíamos probar valores aún más grandes o pequeños (según el caso).
- Si el óptimo está entre dos valores deberíamos probar con un poco más de resolución.
- El principal problema del método de Grid-Search es que consume mucho tiempo al tener que evaluar todas las combinaciones posibles de valores elegidos para cada hiper-parámetro.
- Algunos modelos tienen muchos hiper-parámtetros

### Random-Search:

- Al igual que en grid-search definimos un conjunto de valores posibles por cada hiper-parámetro.
- Probamos “k” combinaciones aleatorias de hiper-parámetros y nos quedamos la mejor.
- Decidimos cuánto tiempo invertir pero no probamos todas las combinaciones.

### Búsqueda Bayesiana:

- Definimos una distribución de probabilidades y rangos por cada hiper-parámetro.
- Ejemplo, grado del polinomio uniforme entre 1 y 5.
- El algoritmo se encarga de ir probando combinaciones de hiper-parámetros de forma bayesiana.
- El algoritmo prueba combinaciones y en base a los resultados asigna pesos.
- En la siguiente iteración samplea los valores de hiper-parámetros a elegir en base a estos pesos.
- De esta forma a medida que aprende tiene que explorar menos valores sin sentido.

## Probando Hiper-parámetros

- Tanto en grid-search como en random-search o en la optimización bayesiana tenemos que “probar” un conjunto de hiper-parámetros que elegimos.
- ¿Cómo?
    - No podemos usar el test-set (no debemos tocarlo).
    - Tampoco tiene sentido entrenar con el train-set y probar con el mismo set ya que los hiper-parámetros serían óptimos para el set de entrenamiento pero no para datos por afuera del mismo.

# Set de Validación:

- Idea: Dividir el train-set en dos: train y validation.
- Es decir que tendremos un set de train, uno de test y otro de validación.
- Pero si el set de validación es fijo los hiper-parámetros solo serán óptimos para ese conjunto de registros.

# Cross-Validation:

- Idea; dividir el set de entrenamiento en “k” particiones del mismo tamaño (folds).
- Usar cada fold como set de validación entrenando con el resto.
- Promediar la métrica en las “k” validaciones.

![[Organización de datos/Machine Learning I/Evaluación de Modelos/Untitled.png|Untitled]]

## K-fold cross validation

- Cuando k = n usamos cada registro como set de validación. (LOOCV: Leave one out cross-validation). Pero suele ser muy costoso.
- En general valores como k = 10 son populares.