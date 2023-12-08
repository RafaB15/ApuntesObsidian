- KNN (K-Nearest Neighbors)
- ***m*** puntos en ***n*** dimensiones.
- Podemos usar KNN para clasificar o para regresión.
- Es un algoritmo simple pero muy importante.
- Lo vamos a usar durante todo el curso.

# Entrenamiento:

- El entrenamiento de KNN no implica acción alguna.
- Como no hay que hacer nada el tiempo necesario es nulo.
- Y como el tiempo necesario es nulo podemos decir que no hay algoritmo más rápido.

# Clasificación:

- Hay que buscar los puntos más cercanos a un cierto punto dado.
- Esto implica, aparentemente, buscar linealmente entre todos los datos.
- Esto no es bueno, realmente no es bueno.
- No se tiene que entrenar, pero tarda en predecir.
- Cuando los puntos son muchos es necesario contar con algún algoritmo que evite la búsqueda por fuerza bruta.

![[Organización de datos/Machine Learning I/Introducción a KNN/Untitled.png|Untitled]]

# El efecto de K

- Si k es muy chico: Overfitting
- Si k es muy grande: Underfitting
- KNN entre la alucinación y la ceguera.

# Como encontrar k

- Simplemente probar la precisión de KNN para diferentes valores de K.
- Hay que tener en cuenta qué implica un K muy grande o un K muy chico.
- Leave 1 out cross validation.
- K fold cross validation: Separar el set de entrenamiento en k-bloques. Medir la precisión de cada bloque usando los demás como entrenamiento y promediar las k-precisiones.

- Es necesario encontrar una aproximación si los puntos son muchos.
- Es necesario determinar k y la distancia a usar.
- No siempre la distancia euclideana es útil.
- Los atributos tienen que estar normalizados.
- De lo contrario un atributo puede dominar todas las distancias.
- Es muy sensible a dimensiones (features) ruidosas.
- Ej: Predecir la altura de una persona.
- Feature Selection:
    - Forward selection
    - Backward elimination.
- Eliminar un atributo puede ser una medida muy drástica.
- Reducir el peso del atributo.
- Cada atributo aporta un peso diferente en el cálculo de la distancia.
- Hay que aprender los pesos óptimos.

## La teoría

- Teorema de Covert Hart. Si el mejor clasificador posible tiene un error **e** entonces KNN con datos infinitos tiene un error menor a 2e.
- Conclusiones correctas
- Conclusiones incorrectas

## Eliminación de outliers

- Si **m** vecinos de un punto son de otra clase → outlier