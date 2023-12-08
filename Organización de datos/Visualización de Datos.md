Una visualización exitosa tiene 4 elementos:

- Datos: Información usada
- Objetivo o función: ¿Para qué es útil?
- Metáfora visual: Belleza, estructura, apariencia, elementos metafóricos.
- Historia o concepto: ¿Qué tan interesante es? ¿Qué cuenta?

# Plots

Los plots tienen objetivos y datos bien definidos, y pueden o no
contar una historia.

- Sus metáforas visuales son muy simples.
- Son muy útiles en la visualización científica y de análisis
exploratorio.
- Son el esqueleto de las visualizaciones con metáforas
visuales de mayor complejidad.

## Distribución continua:

La variable que se intenta ver tiene que ser lo suficientemente continua para que no pueda ser separadas por partes. No sería posible por ejemplo separarla en barritas para cada número pues se perdería el entendimiento del plot.

 

![[Organización de datos/Visualización de Datos/Untitled.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 1.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 2.png|Untitled]]

Estos dos últimos gráficos se llaman histogramas y el segundo está mal porque se usa una variable discreta abajo y terminás con datos para el mes 1,5 2,4 y así, cuando tendría que ser un gráfico de barras.

Los bins son el numero de barritas de un histograma. Mientras más bins más barritas.

O podemos usar density plots, que son como funciones de densidad de proba. La integral da 1. Arranca en cero a menos que la trunquemos.

![[Organización de datos/Visualización de Datos/Untitled 3.png|Untitled]]

Algunos números útiles:

- **Media:** Es el promedio.
- **Mediana**: Es el valor que está en la mitad de la población.
- **Cuartil:** Son los valores límite que dejan al 25% de la población entre ellos.
- **Rango intercuartílico:** el rango entre el cuartil 1 y el cuartil 3.

### Box Plot

![[Organización de datos/Visualización de Datos/Untitled 4.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 5.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 6.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 7.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 8.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 9.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 10.png|Untitled]]

### Violin Plot:

Es como una combinación entre un density plot y un box plot.

![[Organización de datos/Visualización de Datos/Untitled 11.png|Untitled]]

## Distribución discreta:

Es explícito en la cantidad o proporción

### Pie plot

![[Organización de datos/Visualización de Datos/Untitled 12.png|Untitled]]

### Bar Plot

![[Organización de datos/Visualización de Datos/Untitled 13.png|Untitled]]

### Stacked bar plot

![[Organización de datos/Visualización de Datos/Untitled 14.png|Untitled]]

### Tree map

![[Organización de datos/Visualización de Datos/Untitled 15.png|Untitled]]

## Plots de relación

### Scatter Plot

Ambos ejes o bien son continuos o tienen una buena granularidad (lo que los vuelve indistintos del continuo)

![[Organización de datos/Visualización de Datos/Untitled 16.png|Untitled]]

### Regression plot

![[Organización de datos/Visualización de Datos/Untitled 17.png|Untitled]]

### Heatmap

![[Organización de datos/Visualización de Datos/Untitled 18.png|Untitled]]

![[Organización de datos/Visualización de Datos/Untitled 19.png|Untitled]]

## Series de tiempo

![[Organización de datos/Visualización de Datos/Untitled 20.png|Untitled]]

### Lineplot

![[Organización de datos/Visualización de Datos/Untitled 21.png|Untitled]]

### Lollipop

![[Organización de datos/Visualización de Datos/Untitled 22.png|Untitled]]

## Cosas que se evalúan:

- La visualización se tiene que explicar por sí mismas.
- os tomemos un minuto en pensar con cariño el color que mejor ajusta al concepto que están ploteando.
- Usen ese color para ese concepto a lo largo de las visus.
- No usar colores default.