- Los mejores algoritmos de machine learning son combinaciones de varios algoritmos.
- Aunque  no siempre sea lo mejor para usar en la práctica,.

# Bagging:

- Aplicar el mismo clasificador **n** veces usando ***Bootstrapping:***
    - Tomamos muestras del set de entrenamiento (con reemplazo) de igual tamaño que este. Entonces habrán valores repetidos y algunos registros quedarán afuera del bootstrap.
- Promediar sus resultados.

![[Organización de datos/Árboles/Ensambles/Untitled.png|Untitled]]

![[Organización de datos/Árboles/Ensambles/Untitled 1.png|Untitled]]

- Disminuye la posibilidad de overfitting.
    - Cada clasificador no ve la totalidad de los registros del set de enetrenamiento.
- Registros OOB (Out of Bag).
    - Se usan para ver la precisión del algoritmo (como si fuera un test)

# Boosting:

- Entrenar algoritmo simple.
- Analizar sus resultados.
- Entrenar otro algoritmo simple en donde se le da mayor peso a los resultados para los cuales el anterior tuvo peor performance.
- Resultado final en base a un promedio ponderado.

![[Organización de datos/Árboles/Ensambles/Untitled 2.png|Untitled]]

![[Organización de datos/Árboles/Ensambles/Untitled 3.png|Untitled]]

![[Organización de datos/Árboles/Ensambles/Untitled 4.png|Untitled]]

- Se genera un nuevo árbol para predecir lo que se predijo mal en el árbol anterior.
- La profundidad de los árboles generados con Boosting es menor a la generada con Bagging.

# Majority Voting:

- Cada clasificador da un voto a cada clase.
- Mejor si se usan resultados con poca correlación.
- Se le puede dar un peso distinto a cada modelo.

![[Organización de datos/Árboles/Ensambles/Untitled 5.png|Untitled]]

# Averaging:

- Promediar el resultado de varios clasificadores.
- Sirve para regresión y clasificación (con clases o probabilidades).
- Ajuste de escala de probabilidades de cada modelo usando rango entre 1 y n (n: total de registros). Prob = 1 - (x-min)/(max-min).

![[Organización de datos/Árboles/Ensambles/Untitled 6.png|Untitled]]

# Blending (o Stacked):

- Separar parte pequeña del set de entrenamiento (10%).
- Con los clasificadores entrenados con el resto del set, lo usamos para predecir sobre el set anterior.
- Con esto se entrena un nuevo modelo para que aprenda cómo combinar los resultados de los clasificadores de foma tal que estos nos den la predicción final.