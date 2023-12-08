# Un modelo

- Planteamos una hipótesis.
- Definimos qué es un buen modelo.
- Intentamos llegas a uno.

- Planteamos una función predictora
    - Tendremos parámetros e hiperparámetros.
- Definimos una función de error o de costo.
    - Según si es un problema de clasificación o regresión tenemos varias opciones.
- Minimizamos el costo con métodos numéricos.
    - Esto nos encuentra los mejores parámetros. Los hiperparámetros los buscamos de otra manera.

# Primer modelo: Regresión Lineal

Una regresión lineal es un modelo que intenta ajustar una línea a un conjunto de datos.

Es decir, queremos hallar el conjunto **m** y **b** que más se acerque a nuestros datos, según la ecuación de la recta.

![[Organización de datos/Machine Learning I/Introducción a Redes Neuronales/Untitled.png|Untitled]]

Planteamos las hipótesis de la regresión lineal:

$$
h_{\theta}(\hat{x})=\theta^t \hat{x}
$$

x es una muestra o evidencia y $\theta$ es el parámetro que queremos aprender.

## Idea de optimización: descenso de gradiente

- El gradiente me dice para dónde aumenta más la función.
- Si voy en sentido contrario, para dónde disminuye más.
- Es la mejor opción local → Greedy.
- Error, minimizar esta función significa que se predice algo muy cercano al valor real.

$$
J(\theta) = \frac{1}{2}\sum_i(h_{\theta}(x^{(i)}) - y^{(i)})^2
$$

## Optimización:

- Podemos utilizar descenso por gradiente. Definimos la sucesión:
    
    Aquí $\gamma$ es un parámetro no aprendido y por lo tanto debemos definirlo nosotros. Se denomina ritmo de aprendizaje (learning rate) y puede ser constante, o dependiente del número de iteraciones.
    

$$
\theta_{n+1} = \theta_n - \gamma \nabla J(\theta_n)
$$