- Idea: Codificar las variables categóricas en base a los labels, por ejemplo el promedio de los labels para cada valor posible.
- Peligro: Se filtra información de los labels a los features de entrenamiento.

![[Organización de datos/Feature Engineering/Mean encoding/Untitled.png|Untitled]]

París tiene 0.5 porque aparece dos veces, en una tiene ad 0 y en otra ad 1. Moscu tiene 0.33 porque aparece 3 veces, en 2 tiene ad 0 y en una tiene ad 1.

Se establece un orden entre las variables.

Algunas fórmulas distintas:

![[Organización de datos/Feature Engineering/Mean encoding/Untitled 1.png|Untitled]]

## CV (cross validation) Mean Encoding:

![[Organización de datos/Feature Engineering/Mean encoding/Untitled 2.png|Untitled]]

## Smoothing

![[Organización de datos/Feature Engineering/Mean encoding/Untitled 3.png|Untitled]]

## Adding Noise:

- El ruido degrada la calidad del encoding.
- Es necesario encontrar la cantidad de ruido adecuada (hiper- parámetro).
- En general se usa en conjunto con LOOCV.

# Expanding Mean

![[Organización de datos/Feature Engineering/Mean encoding/Untitled 4.png|Untitled]]

- Es necesario tener el DF ordenado (por tiempo).
- En general minimiza el filtrado del target al set de entrenamiento.
- La calidad del encoding es irregular.
- Es el método usado por CarBoost.