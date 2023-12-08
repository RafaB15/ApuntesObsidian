- Basado en DBSCAN y en clusterin jerárquico.
- Soluciona el problema de densidades diferentes entre los clusters.
- Primero analicemos DBScan y luego veamos qué modifica este versión.

Podemos interpretar a DBScan como que arma un grafo con aristas:

![[Organización de datos/Clustering/HDBScan/Untitled.png|Untitled]]

y los clusters son las componentes conexas.

![[Organización de datos/Clustering/HDBScan/Untitled 1.png|Untitled]]

- Lo que hace HDBScan es evitar el parámetro $\epsilon$ que no permite analizar densidades distintas.
- Para analizar densidades distintas es necesario empujar los outliers fuera de los puntos densos.

![[Organización de datos/Clustering/HDBScan/Untitled 2.png|Untitled]]

Definimos una distancia nueva:

![[Organización de datos/Clustering/HDBScan/Untitled 3.png|Untitled]]

donde core (a) es la distancia al k-vecino más cercano.

K: tamaño mínimo del cluster

Armamos el grafo completo

![[Organización de datos/Clustering/HDBScan/Untitled 4.png|Untitled]]

Armamos el árbol tendido mínimo

![[Organización de datos/Clustering/HDBScan/Untitled 5.png|Untitled]]

![[Organización de datos/Clustering/HDBScan/Untitled 6.png|Untitled]]

![[Organización de datos/Clustering/HDBScan/Untitled 7.png|Untitled]]

![[Organización de datos/Clustering/HDBScan/Untitled 8.png|Untitled]]

![[Organización de datos/Clustering/HDBScan/Untitled 9.png|Untitled]]