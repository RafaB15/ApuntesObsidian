La regularización altera el entrenamiento de un modelo para evitar que sus parámetros cambien de forma brusca o rápida con los datos, evitando el overfitting.

Vamos a ver tres formas de regularizar:

- L1 (Lasso)
- L2 (Ridge)
- Dropout

# Regularización L1

Agregamos un nuevo componente a las loss.

$$
loss_{L1}(y,\hat y) = loss(y, \hat y) + \alpha \sum_k |w_k|
$$

# Regularización L2

$$
loss_{L2}(y,\hat y) = loss(y, \hat y) + \alpha \sum_k w_k^2
$$

 

# Dropout

![[Organización de datos/Redes Neuronales/Regularización/Untitled.png|Untitled]]

Cancela caminos al azar para obligarlas a no confiar en algunas neuronas. Ayuda a que no todo dependa de una neurona.