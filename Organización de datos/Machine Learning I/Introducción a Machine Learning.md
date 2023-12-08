## Aprendizaje supervisado

Supervisado (tenemos labels)

- Regresión (labels numéricos)
- Clasificación (labels categóricos)

No supervisado

- Detección de anomalías
- Clustering

### El set de datos

- El set de datos tiene **m** filas (rows u observaciones) y **n** columnas (features o variables).
- Al proceso de creación de features lo llamamos ***feature engineering***.
- A partir del set de datos queremos entrenar un modelo de Machine Learning que nos permita predecir el label a partir de los features.

### Validación del Modelo

- ¿Cómo podemos evaluar el modelo entrenado? Podemos hacer predicciones con datos para los cuales conocemos el valor a predecir (label).
- Dividimos el set de datos en dos:
    - Training set
    - Test set
- El trainig set lo usamos para entrenar, el test lo usamos para medir la performance de nuestro modelo.
- Esta medición implica el uso de alguna métrica de performance.

### Métricas

- Accuracy (Porcentaje de aciertos)
- Precisión
- Recall
- RMSE (error cuadrático medio)
- MAE (promedio de los errores absolutos)
- AUC (área bajo al curva)
- Otras…

### Split Train- Test

- En algunos casos podemos hacerlo al azar (ejemplo 80% train, 20% test).
- En otros casos es importante hacerlo por tiempo (evitar time-travelling, ocurre cuando tenemos en el set de entrenamiento cosas que son posteriores al set de testeo).
- Para las métricas es importante que el set de test tenga distribución productiva.

### Sets Desbalanceados

- Si el set de datos está muy desbalanceado puede ser difícil entrena el modelo.
- Posibles soluciones:
    - Oversamplear la clase minoritaria.
    - Subsamplear la clase mayoritaria.
    - Manejar el desbalanceo con hiper-parámetro  del modelo.

### Resumen hasta aquí

- Tenemos un set de datos y necesitamos:
    - Un set de train (que dependiendo del modelo podemos necesitarlo balanceado)
    - Un set de test con distribución productiva.
    - Evitar problemas de time-travelling (jamás tener en train algo que sucedió luego de algo en test).
    - Elegir la métrica con la cual vamos a evaluar nuestro modelo (hay muchas opciones).
    - Es importante que el set de test nunca sea usado para entrenar.