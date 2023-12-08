- Costos calculados con la [[Información de Catálogo]]. 
- Existen distintos métodos para calcular el costo de la operación de junta. En estas presentaremos el costo de lectura y cálculo del resultado, no el de almacenamiento.

# Método de loops anidados por bloque

- Dadas dos relaciones *R* y *S*, el método de **loops anidados por bloque** consiste en tomar cada par de bloques de ambas relaciones, y comparar todas sus tuplas entre sí. para ver si la junta de las dos tuplas cumplen la condición para quedar en el resultado final. 
- Si por cada bloque de *R* se leen todos los bloques de *S*, el costo de procesar dicho bloque es $1 + B(S)$, y el total es de $B(R) · (1 + B(S))$. Utilizando las tuplas de *S* como pivotes, el costo total sería de $B(S) · (1 + B(R))$.
- El costo del método es entonces: $$cost(R ∗ S) = min(B(R) + B(R) · B(S), B(S) + B(R) · B(S))$$ 
- Esta estimación es un peor caso, suponiendo que sólo podemos tener un bloque de cada tabla simultáneamente en memoria $(M_i = 2)$ (por lo cual las tendremos que ir sacando y volviendo a poner, teniendo que acceder más veces a memoria). Si pudiéramos cargar una de las tablas completa en memoria y sobrara un bloque, tendríamos el mejor caso: $$cost(R ∗ S) = B(R) + B(S)$$
# Método de único loop
- Si el [[Atributos|atributo]] de junta tiene un [[Índices|índice]] asociado en *R*, por ejemplo, podemos recorrer las tuplas de *S* y para cada una de ellas buscar en el índice la/s tupla/s de *R* en que el atributo coincide. 
- Si el índice es primario, el costo será: $$cost(R ∗ S) = B(S) + n(S) · (Height(I(A, R)) + 1)$$
- Si el índice es de clustering, puede haber más de una coincidencia:
$$cost(R*S) = B(S) + n(S) \cdot \left( Height(I(A,R)) + \frac{n(R)}{V(A,R)\cdot F(R)}\right)$$
- Si el índice es secundario: $$cost(R*S) = B(S) + n(S) \cdot \left( Height(I(A,R)) + \frac{n(R)}{V(A,R)}\right)$$
# Método de sort-merge
- Consiste en ordenar los archivos de cada tabla **por el/los atributo/s de junta**. 
- Si entran en memoria, el ordenamiento puede hacerse con **quicksort**, y el costo de acceso a disco es sólo **B(R) + B(S)**.
- Si los archivos no caben en memoria debe utilizarse un algoritmo de sort externo. El costo de ordenar **R** y volverlo a guardar en disco ordenado es de aproximadamente $2 \cdot B(R) \cdot [\log_{M-1}(B(R))]$ (el log estima la cantidad de etapas del sort externo).
- Una vez ordenados, se hace un merge de ambos archivos que sólo selecciona aquellos pares de tuplas en que coinciden los atributos de junta. El merge recorre una única vez cada archivo, con un costo de **B(R) + B(S)**. 
- El costo total es entonces: $$cost(R*S) = B(R) + B(S) + 2 \cdot B(R) \cdot [\log_{M-1} (B(R))] + 2 \cdot B(S) \cdot [\log_{M-1}(B(S))]$$

# Método de junta hash

- Variante GRACE.
- La idea de este método es particionar las tablas *R* y *S* en **m** grupos utilizando una función de hash $h(X)$ aplicada **sobre los atributos de junta X. 
- **Atención**: Que dos tuplas $r \in R$ y $s \in S$ cumplan que $h(r.X) = h(s.X)$ no implica que $r.X = s.X$! 
- **Costo del particionado**: $2 · (B(R) + B(S))$ 
	- Porque es necesario leer todos los bloques y reescribir sus datos en otro orden. 
- Luego, cada par de grupos $R_i$ y $S_i$ se combina verificando si se cumple la condición de junta con un enfoque de fuerza bruta. 
	- Que los valores de una tabla y de otra tenga el mismo resultado del hash no significa que se tengan que unir, por lo que igualmente habrá que chequearlas, pero será un trabajo menor.
	- Observación: No es necesario combinar $R_i$ y $S_j$ para $i \not= j$ 
	- ¿Por qué? $r.X = s.X \to h(r.X) = h(s.X)$ 
- **Hipótesis**: **m** fue escogido de manera que para cada par de grupos $(R_i , S_i)$ al menos uno entre en memoria ($m \le M$), y sobre un bloque de memoria para hacer desfilar al otro grupo. 
- **Costo de la combinación de $R_i$ y $S_i$ :** $$B(R_i) + B(S_i)$$
	- Esto se deduce de: 
		- Observación 1: $F(R_i) = F(R)$ y $F(S_i) = F(S)$ Observación 2: $\sum_{i=1}^{m}n(R_i) = n(R)$ y $\sum_{i=1}^{m}n(S_i) = n(S)$ 
- El costo total es: $$cost(R ∗ S) = 3 · (B(R) + B(S))$$