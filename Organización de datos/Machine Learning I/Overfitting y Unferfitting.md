# Underfitting

- Se produce cuando tenemos un error de entrenamiento alto.
- El modelo ajusta mal al set de entrenamiento.
- El modelo tiene “visión borrosa”.
- El modelo no tiene suficiente capacidad expresiva.
- El modelo no tiene suficiente complejidad o grados de libertad.
- Soluciones:
    - En general la solución es cambiar a un modelo más complejo, más expresivo.

# Overfitting

- El modelo tiene muy buen resultado para el set de entrenamiento pero no es tan bueno para el set de test.
- El modelo generaliza mal.
- El modelo “alucina”.
- El modelo es demasiado expresivo.
- Si el modelo es muy complejo puede haber memorizado el set de entrenamiento y es malo prediciendo.
- Un modelo con muchos grados de libertad puede tener demasiadas soluciones posibles al mismo problema de optimización.

![[Organización de datos/Machine Learning I/Overfitting y Unferfitting/Untitled.png|Untitled]]

![[Organización de datos/Machine Learning I/Overfitting y Unferfitting/Untitled 1.png|Untitled]]

- Soluciones:
    - Conseguir más datos.
    - Disminuir la complejidad del modelo.
    - Usar regularización.

## Regularización:

- La regularización es una técnica por la cuál penalizamos a un modelo de machine learning en función de su complejidad.
- Ejemplo: Penalizamos un polinomio mediante lambda * sumatoria de todos los coeficientes al cuadrado.