Una neurona artificial es una función, que tiene otra función como hiperparámetro y dos parámetros ***b*** y **w**. Entonces su salida es $f(wx+b)$

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled.png|Untitled]]

# Neurona lineal:

Es una neurona en la que la función es $f(x) = x$

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 1.png|Untitled]]

 

## Red neuronal de neuronas lineales

$w_i = \text{Weight}_i$

$b_i = \text{Bias}_i$

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 2.png|Untitled]]

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 3.png|Untitled]]

Si factorizamos esta expresión nos damos cuenta que nos queda algo multiplicando a $x$ más una constante, lo que termina siendo una función lineal.

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 4.png|Untitled]]

Por lo tanto no se puede sacar mucho provecho de una red neuronal de neuronas lineales, pues podríamos usar simplemente una sola neurona lineal que haga lo mismo.

# Neurona no lineal

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 5.png|Untitled]]

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 6.png|Untitled]]

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 7.png|Untitled]]

Con estas neuronas escalonadas podemos armar redes neuronales que nos son más útiles

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 8.png|Untitled]]

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 9.png|Untitled]]

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 10.png|Untitled]]

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 11.png|Untitled]]

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 12.png|Untitled]]

A medida que vayamos agregando neuronas no lineales vemos que podemos moldear la función

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 13.png|Untitled]]

## Teorema de aproximación universal

Con ciertas funciones y una capa de neurona infinitas podemos aproximar absolutamente cualquier función

![[Organización de datos/Redes Neuronales/Neuronas Artificiales/Untitled 14.png|Untitled]]