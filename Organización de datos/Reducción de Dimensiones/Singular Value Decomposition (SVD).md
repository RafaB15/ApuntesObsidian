***Revisar Guía 5 álgebra***

# Usos

## Compresión de imágenes:

Si consideramos a la imagen como una matriz de píxeles, podemos aplicarle la SVD y quedarnos con los **r** valores singulares más grandes (aproximación de rango r), mientras más chico **r** mayor será la compresión.

Almacenar estas matrices truncadas $U_r, \sum_r \text{ y } V_r$ nos puede resultar menos pesado en disco que almacenar la matriz original.

Sin embargo, es una compresión con pérdida , estamos descartando información importante para la imagen, ¿qué pasa si ahora intentamos reconstruir la imagen?

![[Organización de datos/Reducción de Dimensiones/Singular Value Decomposition (SVD)/Untitled.png|Untitled]]

## Otras aplicaciones:

- Reducción de dimensiones de un dataset.
- Information retrieval, Análisis Semántico Latente (LSA).
- Sistemas de recomendación.
- Procesamiento de señales.
- Motores de búsqueda (ver CubeSVD p.ej)

Y muchas más