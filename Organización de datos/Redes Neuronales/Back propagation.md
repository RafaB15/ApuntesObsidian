# Hiper-parámetros

![[Organización de datos/Redes Neuronales/Back propagation/Untitled.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 1.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 2.png|Untitled]]

# Parámetros

Los w y los b

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 3.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 4.png|Untitled]]

Cambian a medida entrenemos

## Error

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 5.png|Untitled]]

Queremos encontrar el error mínimo

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 6.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 7.png|Untitled]]

Esta última ecuación no funciona muy bien porque:

- La función de pérdida es no convexa.
- Se necesita tener todas las predicciones computadas al mismo tiempo para poder derivar.
- No todas las funciones de activación y pérdida se derivan fácil o son derivables, la expresión final puede ser muy compleja.
- Entrenar con todos los datos empeora el entrenamiento respecto de su alternativa (Stochastic Gradient Descent - SGD).
    - 
        
        ***epochs*** veces se mezclan todos los datos al azar t:
        
        1. Se toman ***batch size*** datos en orden y para cada uno:
            1. Se calcula el gradiente $\vec\nabla loss(y,\hat y)(\theta)$ por medio de ***back propagation***.
            2. Se mueven los parámetros en la dirección contraria al gradiente en una magnitud de módulo ***learning rate.***
            
            ![[Organización de datos/Redes Neuronales/Back propagation/Untitled 8.png|Untitled]]
            
- Igualar eso a 0 no es sencillo.

### Error cuadrático medio

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 9.png|Untitled]]

### Error absoluto medio

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 10.png|Untitled]]

### Entropía cruzada categórica

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 11.png|Untitled]]

### ***StochasticGradient Descent:***

***epochs*** veces se mezclan todos los datos al azar t:

1. Se toman ***batch size*** datos en orden y para cada uno:
    1. Se calcula el gradiente $\vec\nabla loss(y,\hat y)(\theta)$ por medio de ***back propagation***.
    2. Se mueven los parámetros en la dirección contraria al gradiente en una magnitud de módulo ***learning rate.***

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 8.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 12.png|Untitled]]

## Back propagation

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 13.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 14.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 15.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 16.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 17.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 18.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 19.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 20.png|Untitled]]

![[Organización de datos/Redes Neuronales/Back propagation/Untitled 21.png|Untitled]]