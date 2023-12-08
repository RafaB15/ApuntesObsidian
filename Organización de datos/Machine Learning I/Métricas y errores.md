# Métricas

Vamos a llamar “métrica” a toda forma de medir qué tan bien le va a un modelo.

Vamos a diferenciar métricas para dos situaciones aunque hay más:

- Clasificación
- Regresión

Un modelo recibe un punto que puede ser cualquier cosa que usará para predecir y devolverá una predicción, pero nosotros tendremos también la respuesta correcta para ver si hizo las cosas bien.

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled.png|Untitled]]

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 1.png|Untitled]]

La métrica nos ayudará a medir la calidad de nuestro modelo

## Clasificación binaria

El problema de clasificación binaria es tal que sus $y$ son unos o ceros e $\hat{y}$ es un número entre 0 y 1 que representa la probabilidad de que $x$ sea de la clase 1.

Ejemplos:

- Detección de fraude
- Filtro de spam
- Predicción de compra

Las 4 métricas de clasificación binaria que vamos a ver son:

- Accuracy
- Precisión
- Recall (ó “recuperados”)
- AUC-ROC

### Accuracy:

Vamos a querer decir qué tantas veces nuestro modelo acierta en su predicción. Primero tenemos que transformar nuestras predicciones en binario. Luego definimos accuracy como la cantidad de predicciones correctas sobre el total. Depende del corte que elijamos para saber si algo fue acertado.

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 2.png|Untitled]]

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 3.png|Untitled]]

### Precisión:

¿Cuántos de los que dije que son de una clase lo son realmente?

Me fijo cuantos de los unos que predije resultaron ser verdaderamente unos, entonces sé que si digo que algo es uno tiene cierta precisión.

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 4.png|Untitled]]

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 5.png|Untitled]]

### Recall:

Es análogo a la precisión. ¿Cuántos de los que son de una clase predije como de esa clase? Mientras más precisión tenga, más difícil va a ser el recall y viceversa. 

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 6.png|Untitled]]

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 7.png|Untitled]]

***Ejemplo:*** Predicción de cáncer en imágenes médicas. La clase 1 es “tiene cáncer”.

Precisión: ¿Cuántos de los que dije que son de una clase lo son realmente?

Buenas precisión: Cuando yo digo que alguien tiene cáncer, tiene cáncer.

Consecuencia de una mala precisión: Alguien se lleva un susto y con estudios posteriores se ve que no tenía cáncer.

Recall: ¿Cuántos de los que son de una clase predije como de esa clase?

Buen recall: Para todos los que tenían cáncer yo dije que tenía cáncer.

Consecuencias de un mal recall: Que se nos pase alguien que tenía cáncer.

Es mucho más costoso tener un recall bajo que una precisión baja.

### AUC-ROC:

AUC → Area under the curve.

ROC → Es una curva.

La probabilidad de que dados dos puntos de la clase 0 y 1 cualesquiera, sus probabilidades predichas estén bien ordenadas, es decir, la probabilidad del punto 0 sea menor a la del 1.

 

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 8.png|Untitled]]

### Regresión:

Las 2 métricas de regresión que vamos a ver son:

- MAE: Mean Absolute Error, promedio del error absoluto

$$
MAE = \frac{\sum_{i=1}^n|y_i - \hat{y}_i|}{n} \\ y=[10,20,30] \\ \hat{y} = [11,19,25] \\ MAE = \frac{1+1+5}{3} = 2.333
$$

- MSE: Mean Squared Error
    
    $$
    MSE = \frac{\sum_{i=1}^n(y_i - \hat{y}_i)^2}{n} \\ y=[10,20,30] \\ \hat{y} = [11,19,25] \\ MAE = \frac{1+1+25}{3} = 9
    $$
    

# Error, pérdida u objetivo:

El error, pérdida u objetivo entre otros nombres, es una métrica que es parte de la construcción de un modelo.

En general el modelo intenta mejorar (optimizar) esa métrica por medio del entrenamiento.

No cualquier métrica puede ser un error de cualquier tipo de modelo.

El error de una regresión lineal por cuadrados mínimos es el MSE.

![[Organización de datos/Machine Learning I/Métricas y errores/Untitled 9.png|Untitled]]

Errores muy comunes en clasificación son distintas métricas de teoría de la información: entropía, entropía cruzada, divergencia de Kullback-Leiber.

Para regresión el error más común a usar es MSE, cuya ventaja respecto de MAE es que es diferenciable.