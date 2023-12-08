# Definición:

Tengo una serie de n datos con n features, la pasamos por una caja y nos da n datos, n filas y k features nuevos. No pedimos alguna relación en particular entre las features viejas y las nuevas, pero sí pedimos una relación entre los puntos nuevos y los viejos. Dependerá del algoritmo.

![[Organización de datos/Reducción de Dimensiones/Reducción de dimensiones/Untitled.png|Untitled]]

![[Organización de datos/Reducción de Dimensiones/Reducción de dimensiones/Untitled 1.png|Untitled]]

# Motivaciones para reducir dimensiones:

- Visualización.
    - Buscar agrupamientos y relaciones con variables categóricas.
- Reducir tiempo de cómputo.
    - Ej: algoritmos que no escalan bien en dimensiones
- Obtener los features importantes del dataset.
    - Manifold theory

## Manifold theory + manifold learning

- Las dimensiones ***reales*** de los datos generalmente no son iguales a las dimensiones ***aparentes***.
    - i.e. non es posible cualquier combinación de las columnas (no existe una casa con 15 baños y una habitación).
- Concepto de grados de libertad y restricciones.

# ¿Cómo funciona la “caja”?

- ¿Es importante?
    - Si
- Fundamental en visualización
    - Según el método hay relaciones y patrones que agregan significado o nos pueden llevar a la ruina.
- Es importante tener alguna intuición de los parámetros.