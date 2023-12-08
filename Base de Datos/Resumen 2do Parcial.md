# 1. Concurrencia

## 1.1. Anomalías

- **Lectura Sucia (Dirty Read):** Se presenta cuando una transacción $T_2$ lee un ítem que ha sido modificado por otra transacción $T_1$. Si $T_1$ aborta la ejecución resultante puede no ser equivalente a una ejecución serial de las transacciones.
- **Actualización Perdida (Lost Update):** Ocurre cuando una transacción modifica un ítem que fue leído anteriormente por una primera transacción que aún no terminó. Si la primera transacción volviera a leer el ítem luego de que la segunda lo escribiera, se encontraría con un valor distinto. En este caso se lo conoce como *lectura no repetible (unrepeatable read)* .
- **Escritura Sucia (Dirty Read):** Ocurre cuando una transacción $T_2$ escribe un ítem que ya había sido escrito por otra transacción $T_1$ que luego se deshace.
- **Fantasma (Phantom):** Se produce cuando una transacción $T_1$ observa un conjunto de ítems que cumplen determinada condición, y luego dicho conjunto cambia porque algunos de sus items son modificados/creados/eliminados por otra transacción $T_2$. 

## 1.2. Conflicto

- Dado un [[Serializabilidad#Solapamiento|orden de ejecución]], un conflicto es un par de instrucciones $(I_1, I_2)$ ejecutadas por dos [[Transacción|transacciones]] distintas $T_i$ y $T_j$ , tales que $I_2$ se encuentra más tarde que $I_1$ en el orden, y que responde a alguno de los siguientes esquemas: 
	- $(R_{T_i} (X), W_{T_j} (X))$: Una transacción escribe un ítem que otra leyó. 
	- $(W_{T_i} (X), R_{T_j} (X))$: Una transacción lee un ítem que otra escribió. 
	- $(W_{T_i} (X), W_{T_j} (X))$: Dos transacciones escriben un mismo ítem. 
- Todo par de instrucciones consecutivas $(I_1, I_2)$ de un [[Solapamiento|solapamiento]] que no constituye un conflicto puede ser invertido en su ejecución (es decir, reemplazado por el par ($I_2, I_1$)) obteniendo un solapamiento equivalente por conflictos al inicial.

## 1.3. Serializabilidad por conflictos: Grafo de precedencias

- Dado un conjunto de transacciones $T_1, T_2, \dots, T_n$ que acceden a determinados ítems $X_1, X_2, \dots, X_p$, el grafo de precedencias es un grafo dirigido simple que se construye de la siguiente forma: 
	1. Se crea un nodo por cada transacción $T_1, T_2, \dots, T_n$. 
	2. Se agrega un arco entre los nodos $T_i$ y $T_j$ (con $i \not = j$) si y sólo si existe algún conflicto de la forma ($R_{T_i} (X_k), W_{T_j} (X_k)$), ($W_{T_i} (X_k), R_{T_j} (X_k)$) ó ($W_{T_i} (X_k), W_{T_j}(X_k)$). 
- Cada arco ($T_i , T_j$) en el grafo representa una precedencia entre $T_i$ y $T_j$ , e indica que para que el resultado sea equivalente por conflictos a una ejecución serial, entonces en dicha ejecución serial $T_i$ debe preceder a (es decir, “ejecutarse antes que”) $T_j$.

![[Cuadro grafo de precedencia ejemplo.png]]

![[Grafo de precedencia ejemplo.png]]

## 1.4. Control de Concurrencia

- **Protocolo de Lock de 2 fases:** Una transacción no puede adquirir un *lock* luego de haber liberado un *lock* que había adquirido. Todas las que lo cumplen son serializables. ![[Cuadro ejemplo locks.png]]
- **Timestamps:** Se asigna a cada transacción $T_i$ un timestamp $TS(T_i)$, los cuales determinarán el orden serial respecto al cual el solapamiento deberá ser equivalente.
- **Snapshot Isolation:** Cada transacción ve una snapshot de la base de datos correspondiente al instante de su inicio. Cuando dos transacciones intentan modificar un mismo ítem de datos (conflicto Write Write), generalmente gana aquella que hace primero su commit, mientras que la otra deberá ser abortada (first-committer-wins).
- 
## 1.5. Recuperabilidad

- Un [[Solapamiento|solapamiento]] es **recuperable** si y sólo si ninguna [[Transacción|transacción]] *T* realiza el *commit* hasta tanto todas las transacciones que escribieron datos antes de que *T* los leyera hayan commiteado.
- Recuperable no implica [[Serializabilidad|serializable]] y viceversa.
- Rollback $\to$ Procesar el log de una transacción $T$ en forma inversa para deshacer sus efectos.  
- Recuperable $\to$ Nunca será necesario deshacer transacciones que ya hayan commiteado.
- Recuperable no implica que no sea necesario tener que hacer rollbacks en cascada de transacciones que aún no commitearon.

## 1.6. Niveles de Aislamiento

- **Read Uncommitted:** Es la carencia total de aislamiento: No se emplean locks, y se accede a los ítems sin tomar ninguna precaución. 
- **Read Committed:** Evita la anomalía de lectura sucia. 
- **Repeatable Read:** Evita la lectura no repetible y la lectura sucia. 
- **Serializable:** Evita todas las anomalías, y asegura que el resultado de la ejecución

![[Cuadro Niveles de Aislamiento.png]]

# 2. Recuperación

## 2.1. Undo

- Cuando una transacción $T_i$ modifica el ítem $X$ remplazando un valor $v_{old}$ por $v$, se escribe $(WRITE, T_i , X, v_{old})$ en el log, y se hace flush del log a disco.
- El registro $(WRITE, Ti , X, v_{old})$ debe ser escrito en el log en disco (flushed) antes de escribir (flush) el nuevo valor de $X$ en disco ([[Log#WAL|WAL]]).
- Todo ítem modificado debe ser guardado en disco antes de hacer commit. 
- Cuando $T_i$ hace commit, se escribe $(COMMIT, T_i)$ en el log y se hace flush del log a disco ([[Log#FLC|FLC]]).
- Cuando el sistema reinicia se siguen los siguientes pasos: 
	- Se recorre el log de adelante hacia atrás, y por cada transacción de la que no se encuentra el $COMMIT$ se aplica cada uno de los $WRITE$ para restaurar el valor anterior a la misma en disco. 
	- Luego, por cada transacción de la que no se encontró el $COMMIT$ se escribe $(ABORT, T)$ en el log y se hace flush del log a disco.
- **Checkpoint Activo:**
	- Escribir un registro $(BEGIN\ CKPT, t_{act})$ con el listado de todas las transacciones activas hasta el momento.
	- Esperar a que todas esas transacciones activas hagan su commit (sin dejar por eso de recibir nuevas transacciones) 
	- Escribir $(END\ CKPT)$ en el log y volcarlo a disco.
- **Recuperación CKPT activo:**
	- Si encontramos primero un registro $(END\ CKPT)$ sólo debemos retroceder hasta el $(BEGIN\ CKPT)$ durante el rollback, porque ninguna transacción incompleta puede haber comenzado antes). 
	- Si encontramos primero un registro $(BEGIN\ CKPT)$ implica que el sistema cayó sin asegurar los commits del listado de transacciones. Deberemos volver hacia atrás, pero sólo hasta el inicio de la más antigua del listado.

## 2.2. Redo

- Cuando una transacción $T_i$ modifica el ítem $X$ remplazando un valor $v_{old}$ por $v$, se escribe $(WRITE, T_i , X, v)$ en el log. 
- Cuando $T_i$ hace commit, se escribe $(COMMIT, T_i)$ en el log y se hace flush del log a disco ([[Log#FLC|FLC]]). Recién entonces se escribe el nuevo valor en disco. 
- Cuando el sistema reinicia se siguen los siguientes pasos: 
	- Se analiza cuáles son las transacciones de las que está registrado el $COMMIT$. 
	- Se recorre el log de atrás hacia adelante volviendo a aplicar cada uno de los $WRITE$ de las transacciones que commitearon, para asegurar que quede actualizado el valor de cada ítem. 
	- Luego, por cada transacción de la que no se encontró el $COMMIT$ se escribe $(ABORT, T)$ en el log y se hace flush del log a disco.
- **Checkpoint Activo:**
	- Escribir un registro $(BEGIN\ CKPT, t_{act})$ con el listado de todas las transacciones activas hasta el momento y volcar el log a disco. 
	- Hacer el volcado a disco de todos los ítems que hayan sido modificados por transacciones que ya commitearon. 
	- Escribir $(END\ CKPT)$ en el log y volcarlo a disco.
- **Recuperación CKPT activo:**
	- Si encontramos primero un registro $(END\ CKPT)$ deberemos retroceder hasta el $(BEGIN , T_x )$ más antiguo del listado que figure en el $(BEGIN\ CKPT)$ para rehacer todas las transacciones que commitearon. Escribir $(ABORT, T_y )$ para aquellas que no hayan commiteado. 
	- Si encontramos primero un registro $(BEGIN\ CKPT)$. Si el checkpoint llego sólo hasta este punto no nos sirve, y entonces deberemos ir a buscar un checkpoint anterior en el log.

## 2.3. Undo-Redo

- Cuando una transacción $Ti$ modifica el item $X$ remplazando un valor $v_{old}$ por $v$, se escribe $(WRITE, T_i , X, v_{old} , v)$ en el log. 
- El registro $(WRITE, T_i , X, v_{old} , v)$ debe ser escrito en el log en disco (flushed) antes de escribir (flush) el nuevo valor de $X$ en disco.
- Cuando $T_i$ hace commit, se escribe $(COMMIT, T_i)$ en el log y se hace flush del log a disco.
- Los ítems modificados pueden ser guardados en disco antes o después de hacer commit.
- Cuando el sistema reinicia se siguen los siguientes pasos: 
	- Se recorre el log de adelante hacia atrás, y por cada transacción de la que no se encuentra el $COMMIT$ se aplica cada uno de los $WRITE$ para restaurar el valor anterior a la misma en disco. 
	- Luego se recorre de atrás hacia adelante volviendo a aplicar cada uno de los $WRITE$ de las transacciones que commitearon, para asegurar que quede asignado el nuevo valor de cada ítem.
	- Finalmente, por cada transacción de la que no se encontró el $COMMIT$ se escribe $(ABORT, T)$ en el log y se hace flush del log a disco.
- **Checkpoint Activo:**
	- Escribir un registro $(BEGIN\ CKPT, t_{act})$ con el listado de todas las transacciones activas hasta el momento y volcar el log a disco. 
	- Hacer el volcado a disco de todos los ítems que hayan sido modificados antes del $(BEGIN\ CKPT)$. 
	- Escribir $(END\ CKPT)$ en el log y volcarlo a disco.
- En la **recuperación** es posible que debamos retroceder hasta el inicio de la transacción más antigua en el listado de transacciones, para deshacerla en caso de que no haya commiteado, o para rehacer sus operaciones posteriores al $BEGIN\ CKPT$, en caso de que haya commiteado.

# 3. Procesamiento y Optimización de Consultas

## 3.1. Información de catálogo

- `n(R)`: Cantidad de tuplas de la relación *R*.
- `B(R)`: Cantidad de bloques de almacenamiento que ocupa *R*. Normalmente se guardan las filas de a bloques y un acceso a memoria recupera un bloque entero.
- `V(A,R)`: Cantidad de valores distintos que adopta el atributo *A* en *R* (variabilidad).
- `F(R)`: Cantidad de tuplas de *R* que entran en un bloque (factor de bloque). $F(R) = \frac{n(R)}{B(R)} \implies B(R) = \frac{n(R)}{F(R)}$

## 3.2. Selección

### 3.2.1. Costo de la Selección

#### Búsqueda lineal

- Consiste en explorar cada registro, analizando si se verifica la condición.
$$cost(S_1) = B(R)$$
#### Búsqueda con índice primario
- Solo una tupla puede satisfacer la condición (si es que la consulta compara por =).
- Si utilizamos un árbol de búsqueda:	$cost(S_{3a}) = Height(I(A_i, R)) + 1$
- Si utilizamos una clave de hash: $cost(S_{3b}) = 1$
#### Búsqueda con índice clustering
- Las tuplas se encuentran contiguas en los bloques, los cuales estarán disjuntos.
$$cost(S_5) = Height(I(A_i, R)) + \frac{n(R)}{V(A_i,R) . F(R)}$$
#### Búsqueda con índice secundario
- Cuando $A_i$ no tiene un índice de clustering, pero existe un índice secundario asociado a él.
 $$cost(S_6) = Height(I(A_i, R)) + \frac{n(R)}{V(A_i,R)}$$
### 3.2.2 Cardinalidad de la Selección

- Realizaremos la siguiente estimación: $$n(\sigma_{A_i=c}(R)) = \frac{n(R)}{V(A_i , R)}$$
## 3.3. Proyección

### 3.3.1 Costo de la Proyección

- Proyección del tipo $\pi_{X}(R)$.
- X **es** superclave $cost(\pi_{X}(R)) = B(R)$
-  X **no es** superclave.
	- $\hat \pi_X(R) \to$ Proyección de multisets (sin eliminar duplicados).
	- **Ordenar** la tabla: Si $B(\hat \pi_X)(R)) \le M$ (memoria total) podemos ordenar en memoria. De lo contrario, el costo usando sort externo será: $$cost(\pi_X(R)) = cost(Ord_M(R)) = 2.B(R).[\log_{M-1}(B(R))] - B(R)$$
	- Utilizar una estructura de **hash**: Si $B(\hat \pi_X)(R)) \le M$ también podemos hacer el hashing en memoria, con costo $B(R)$. Utilizando hashing externo el costo es de $B(R) + 2.B(\hat \pi_X)(R))$ .

- Si la consulta [[SQL]] no incluye **DISTINCT** no hay que eliminar duplicados, por lo que el costo es siempre $B(R)$.

### 3.3.2 Cardinalidad de la Proyección

- Si proyectamos por una superclave entonces $$n(\pi_{X}(R)) = n(R)$$
- Esta siempre será una cota superior, pues si no es superclave entonces nos dará menos tuplas.

## 3.4 Junta

### 3.4.1 Costo de la Junta

#### Loops anidados por bloque

- Se toman cada par de bloques de ambas relaciones, y comparamos todas sus tuplas entre sí. para ver si la junta de las dos tuplas cumple la condición para quedar en el resultado final.
- El costo del método es (dependiendo de la tabla que usemos como pivote y usando solo dos bloques de memoria) entonces: $$cost(R ∗ S) = min(B(R) + B(R) · B(S), B(S) + B(R) · B(S))$$
- Si pudiéramos cargar una de las tablas completa en memoria y sobrara un bloque, tendríamos el mejor caso: $$cost(R ∗ S) = B(R) + B(S)$$
#### Único Loop

- Si el [[Atributos|atributo]] de junta tiene un [[Índices|índice]] asociado en *R*, por ejemplo, podemos recorrer las tuplas de *S* y para cada una de ellas buscar en el índice la/s tupla/s de *R* en que el atributo coincide. 
- Si el índice es primario, el costo será: $$cost(R ∗ S) = B(S) + n(S) · (Height(I(A, R)) + 1)$$
- Si el índice es de clustering, puede haber más de una coincidencia:
$$cost(R*S) = B(S) + n(S) \cdot \left( Height(I(A,R)) + \frac{n(R)}{V(A,R)\cdot F(R)}\right)$$
- Si el índice es secundario: $$cost(R*S) = B(S) + n(S) \cdot \left( Height(I(A,R)) + \frac{n(R)}{V(A,R)}\right)$$
#### Sort-merge

- Consiste en ordenar los archivos de cada tabla **por el/los atributo/s de junta**. 
- Si entran en memoria, el ordenamiento puede hacerse con **quicksort**, y el costo de acceso a disco es sólo **B(R) + B(S)**.
- Si los archivos no caben en memoria debe utilizarse un algoritmo de sort externo. 
- Una vez ordenados, se hace un merge de ambos archivos que sólo selecciona aquellos pares de tuplas en que coinciden los atributos de junta. 
- El costo total es entonces: $$cost(R*S) = B(R) + B(S) + 2 \cdot B(R) \cdot [\log_{M-1} (B(R))] + 2 \cdot B(S) \cdot [\log_{M-1}(B(S))]$$
#### Junta Hash

- Variante GRACE.
- La idea de este método es particionar las tablas *R* y *S* en **m** grupos utilizando una función de hash $h(X)$ aplicada **sobre los atributos de junta X. 
- **Costo del particionado**: $2 · (B(R) + B(S))$
- Luego, cada par de grupos $R_i$ y $S_i$ se combina verificando si se cumple la condición de junta con un enfoque de fuerza bruta. 
- **Hipótesis**: **m** fue escogido de manera que para cada par de grupos $(R_i , S_i)$ al menos uno entre en memoria ($m \le M$), y sobre un bloque de memoria para hacer desfilar al otro grupo. 
- **Costo de la combinación** de $R_i$ y $S_i$ : $B(R_i) + B(S_i)$
- **Costo total**: $$cost(R ∗ S) = 3 · (B(R) + B(S))$$
- ¿Cómo escoger **m**?
	- Mientras hacemos la partición, guardaremos los elementos de cada grupo en un bloque de memoria.
	- La cantidad de bloques que *suponemos* tendrá una partición de *R* es $\frac{B(R)}{m}$. 
	- **Fórmulas:**
		- $m \le M$ 
		- $min\left(\frac{B(R)}{m}, \frac{B(S)}{m}\right) \le M$  
		- $m \le min(Var(A,R), Var(A,S))$

### 3.4.2 Cardinalidad de la Junta

- **Selectividad de la Junta (js):** $$\frac{1}{max(V(R,B), V(S,B))}$$
- La cardinalidad de la junta se calcula entonces: $$n(R *S) = js \cdot n(R) \cdot n(S) = \frac{n(R) \cdot n(S)}{max(V(R,B), V(S,B))}$$

- Factor de bloque del resultado: $$F(R*S) = \left(\frac{1}{F(R)} + \frac{1}{F(S)}\right)^{-1}$$
- La cantidad de bloques se calcula como: $$B(R*S) = \frac{js \cdot n(R) \cdot n(S)}{F(R*S)} = js \cdot B(R) \cdot B(S) \cdot (F(R) + F(S))$$
## 3.5 Cardinalidad con histograma

- El histograma nos muestra la distribución de los atributos más frecuentes
- $n(Pelicula) = 728$
- $V(género, Película) = 9$
![[Histograma simple.png]]

- $n(\sigma_{género = comedia}(Películas))=140$
- $n(\sigma_{género = terror}(Películas))=\frac{n(Pelicula) - 418}{V(genero, Pelicula) -3} = 52$

- En una junta serían de la siguiente manera
	- $R(A,B)$ con $V(B,R) = 18$
	- $S(B,C)$ con $V(B,S) = 15$
![[Pasted image 20231205235522.png]]
- Conociendo $f_R(x_i)$ y $f_S(x_i)$ sabemos que la cantidad de tuplas en el resultado será $f_R(x_i) \cdot f_S(x_i)$.
![[Pasted image 20231205235556.png]]
- Si solo conocemos uno, estimamos el otro (siendo k la cantidad de otros atributos conocidos de esa tabla) $$f_S(x_i) = \frac{f_S(otros)}{V(B,S) - k}$$
![[Pasted image 20231205235858.png]]
- Actualizamos el valor de otros y k a k'.

$$f_{R*S}(otros) = \frac{f_R(otros) \cdot f_S(otros)}{max(V(R,B) - k', V(S,B) - k')}$$

- Finalmente, para estimar la cardinalidad hacemos $$n(R* S) = \sum_{i}f_{R*S}(x_i) = 121635$$

## 3.6. Heurísticas de Optimización

1. Realizar las selecciones lo más temprano posible. 
2. Remplazar productos cartesianos por juntas siempre que sea posible. 
3. Proyectar para descartar los atributos no utilizados lo antes posible. Entre la selección y la proyección, priorizar la selección.
4. En caso de que hayan varias juntas, realizar aquella más restrictiva primero. Optar por árboles **left-deep** ó right-deep para acotar las posibilidades.