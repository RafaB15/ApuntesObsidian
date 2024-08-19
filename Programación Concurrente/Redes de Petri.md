# Red ordinaria de Petri

- **Grafo bipartito**: Grafo cuyos vértices se pueden separar en dos conjuntos disjuntos, de manera que las aristas no pueden relacionar vértices de un mismo conjunto.
- Es un grafo bipartito que cumple con:
$$PN=(T,P,A)$$
donde:
- $T = t_1, t_2, \dots, t_n$ es un conjunto de nodos llamado **transiciones**.
	- Son eventos que ocasionan cambios de estado
- $P = p_1, p_2, \dots, p_n$ es un conjunto de nodos llamado **lugares**
	- Son los estados del sistema
- $A \subset (T X P) \cup (PXT)$ es un conjunto de **arcos**
- Es bipartito porque no se pueden conectar ds estados/lugares/places entre sí, ni dos transiciones.

![[Red ordinaria de petri.png]]
## Función de Marca
Es un vector que va a contener la cantidad de lo que se conocen como **tokens**, y cuando hay un token en un lugar, la función de marca en ese lugar vale **1**. La función de marca entonces tiene como resultado cuantos tokens hay en un lugar.

$$M: P \to N \cup O$$ 
Cuando el token está en el lugar $p_1$, entonces $M(p_1)=1$ y $M(p_2) = 0$. Por lo tanto $M_0 = (1,0)$ (función de marca para el estado inicial).

# Funciones de Entrada y Salida

Sea $t \in PN = (T,P,A)$ una transición $t$.
Se definen las funciones:
- $I(t) = p / p \in P / (p,t) \in A \subset P$ es la entrada o input de la transición $t$.
	- Es un **lugar/nodo** $(p)$ tal que existe un **arco** $(p,t)$ entre este y la transición $t$ dentro de los nodos $P. 
- $O(t) = p / p \in P / (t, p) \in A \subset P$ es la salida o output de la transición $t$.
	- Es un **lugar/nodo** $(p)$ tal que existe un arco $(t,p)$ entre este y la transición $t$ dentro de los nodos $P$.

![[Pasted image 20240508214543.png]]

- Las transiciones puede tener más de una entrada y más de una salida.
- El nodo con puntito representa que tiene una ficha / token.

## Grafo de Alcance

De los posibles estados del sistema, indicamos la función de marca de ese lugar.

![[Grafo de alcance.png]]

Ejemplito:
![[Pasted image 20240508221633.png]]

![[Pasted image 20240508221643.png]]

Acá vemos que el grafo de alcance es infinito. Porque en el primer estado p1 tiene ficha, p2  y p3 no. Pero si se ejecuta t1 entonces se manda la ficha de p1 a si misma y a p2. Por lo cual si sigue sucediendo t1, siempre se va a regenerar a si misma y se va a sumar una ficha a p2 constantemente.

## Interpretaciones

![[Pasted image 20240508222105.png]]

# Red General de Petri

Es un grafo dirigido bipartito que cumple con
$$PN=(T,P,A, W, M_0)$$

donde
- $T = t_1, t_2, \dots, t_n$ es un conjunto de nodos llamado **transiciones**.
	- Son eventos que ocasionan cambios de estado
- $P = p_1, p_2, \dots, p_n$ es un conjunto de nodos llamado **lugares**
	- Son los estados del sistema
- $A \subset (T X P) \cup (PXT)$ es un conjunto de **arcos**
- $W: A \to N$ es la función de peso
	- Especifica un peso para cada arco que es un número natural.
- $M_0: P \to N \cup \{0\}$ es la función de marca inicial.
	- Es la cantidad de fichas de cada uno de los lugares.

- El peso que tiene el arco es cuantas fichas necesito en el estado del input para que se de esa transición. 
- La transición $t$ está habilitada si y sólo si $M(p) \ge W(p,t): \forall p \in I(t)$
- Cuando $t$ se dispara:
	- $\forall p \in I(t): M(p) \leftarrow M(p) - W(p,t)$
		- Se resta la cantidad en el peso.
	- $\forall p' \in O(t): M(p') \leftarrow M(p') + W(p',t)$

![[Pasted image 20240508223238.png]]

![[Pasted image 20240508224153.png]]

![[Pasted image 20240508224417.png]]

Productor Consumidor con Buffer Infinito:

![[Pasted image 20240508224542.png]]
Productor consumidor con buffer acotado.

![[Pasted image 20240508225606.png]]

- Este ejemplo modela el problema que vimos con semáforos. N sería el tamaño del buffer y en la red de petri sería la cantidad de fichas que hay inicialmente en ese nodo. Al agregar algo al buffer se consume una de esas fichas, y al procesar un elemento del buffer se aumenta una ficha en ese nodo para simbolizar que ahora hay más espacio.
![[Pasted image 20240509222502.png]]

- Las redes de Petri sirven para identificar deadlocks. Si en un grafo de alcance un nodo hoja queda en un estado que no es el estado final del sistema y no puedo salir de él, tengo un deadlock.

# Arco Inhibidor
- En vez de decir que necesita una ficha, dice que necesita que no haya ninguna ficha en el nodo.

![[Pasted image 20240509223418.png]]