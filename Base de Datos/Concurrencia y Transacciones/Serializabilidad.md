- Decimos que un [[Solapamiento|solapamiento]] de un conjunto de transacciones $T_1, T_2, \dots, T_n$ es serializable cuando la ejecución de sus instrucciones en dicho orden deja a la base de datos en un estado equivalente a aquél en que la hubiera dejado **alguna** [[Ejecución serial|ejecución serial]] de $T_1, T_2, \dots, T_n$.
- El que los solapamientos sean serializables garantizan la propiedad de aislamiento de las [[Transacción|transacciones]].
# Serializabilidad por conflictos

- Sabiendo que todo par de instrucciones consecutivas $(I_1, I_2)$ de un solapamiento que no constituye un [[Conflicto|conflicto]] puede ser invertido en su ejecución para obtener un [[Solapamiento#Equivalencia de conflictos|solapamiento equivalente por conflictos]], si logramos hacer esto y dejar de un lado todas las instrucciones de un transacción y del otro las de la otra, entonces habremos obtenido una [[Ejecución serial|ejecución serial]] equivalente por conflictos al solapamiento inicial, lo que nos dice que el solapamiento es serializable por conflictos. 
## Grafo de precedencias

- Sirve para evaluar la serializabilidad por conflictos. 
- Dado un conjunto de transacciones $T_1, T_2, \dots, T_n$ que acceden a determinados ítems $X_1, X_2, \dots, X_p$, el grafo de precedencias es un grafo dirigido simple que se construye de la siguiente forma: 
	1. Se crea un nodo por cada transacción $T_1, T_2, \dots, T_n$. 
	2. Se agrega un arco entre los nodos $T_i$ y $T_j$ (con $i \not = j$) si y sólo si existe algún conflicto de la forma ($R_{T_i} (X_k), W_{T_j} (X_k)$), ($W_{T_i} (X_k), R_{T_j} (X_k)$) ó ($W_{T_i} (X_k), W_{T_j}(X_k)$). 
- Cada arco ($T_i , T_j$) en el grafo representa una precedencia entre $T_i$ y $T_j$ , e indica que para que el resultado sea equivalente por conflictos a una ejecución serial, entonces en dicha ejecución serial $T_i$ debe preceder a (es decir, “ejecutarse antes que”) $T_j$.

![[Cuadro grafo de precedencia ejemplo.png]]

![[Grafo de precedencia ejemplo.png]]

- Un orden de ejecución es serializable por conflictos si y sólo si su grafo de precedencias no tiene ciclos.
- Si un orden de ejecución es serializable por conflictos, el orden de ejecución serial equivalente puede ser calculado a partir del grafo de precedencias, utilizando el algoritmo de ordenamiento topológico. Podemos ir sacando de a uno los nodos que no tienen aristas entrantes y en ese orden ejecutamos.