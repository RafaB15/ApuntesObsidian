- Density Based Spatial Clustering of Applications with Noise.
- Concepto distinto de cluster — grupo denso.
- Permite tener puntos que no son parte de algún cluster (noise).
- Tenemos que definir densidad.
- Un punto está en una región densa $\iff$ hay más de k puntos con distancia menor a $\epsilon$ del punto (incluimos al punto).
    - Tenemos dos hiperparámetros k y $\epsilon$.
- No se tiene que definir la cantidad de clusters.

### Problemas:

- Es muy sensible a los parámetros.
- Es particularmente sensible a $\epsilon$.
- Como la densidad se define a priori, no maneja bien clusters con densidades muy distintas.
- Como es “plano”, no puede encontrar clusters más densos dentro de otros más grandes.