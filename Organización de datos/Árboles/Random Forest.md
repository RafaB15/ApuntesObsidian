- Uno de los algoritmos más populares en clasificación.
    - Buenos resultados para la mayoría de los sets de datos.
- Bagging sobre árboles de decisión.
- Cada árbol:
    - Usa un subconjunto de los atributos.
    - Usa un bootstrap del set de entrenamiento.
    
    ![[Organización de datos/Árboles/Random Forest/Untitled.png|Untitled]]
    
    Conjunto de árboles de decisión donde cada uno usa un ***bootstrap***  del set de entrenamiento y un cierto conjunto de atributos ***tomados al azar***.
    
- Hiper-parámetros:
    - Cantidad de árboles a crear.
        - Már arboles mejores resultados, pero trade-off de performance.
    - Cantidad de atributos por árbol.
        - Más crítico.
        - Buscarse mediante grid-search usando OOB (out of bounds) precisión.

## Distancia Random Forest:

- Clasificamos dos puntos con cada árbol.
- La distancia es el número de árboles en los cuales la predicción de clase son diferentes.
- Normalizar entre 0 y 1 dividiendo por el total de árboles.