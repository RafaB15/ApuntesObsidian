- [[Sistemas de gestión de bases de datos]] [[No SQL|no SQL]] de tipo [[Bases de datos basadas en grafos|basadas en grafos]].
- Es una de las bases de datos orientadas a grafos más conocidas.
- Incluye soporte para [[Transacción#Propiedades ACID|transacciones ACID]] y para bases de datos distribuidas.
- Utiliza un lenguaje de consulta declarativo denominado **Cypher**.
# Nodos

- Una base de datos Neo4j está formada por **nodos**.
- Un nodo puede tener distintos **labels**. Dentro de cada **label**, el nodo tendrá un conjunto de **propiedades** con determinados **valores**.
- En **Cypher** los nodos se crean con el comando **CREATE**.
```Cypher
CREATE (pepe:Persona {nombre: 'Pepe', color: 'Azul', prof: 'Estudiante'})
```
- Pepe tendrá el **label** *persona* y las **propiedades** *nombre, color* y *prof*.
- No existe una estructura rígida respecto a qué propiedades deben tener los nodos con determinado label. Podemos no especificar algunas propiedades.
- pepe será como un *alias*, no queda almacenado en la base, pero nos sirve para referenciar al nodo.

# Consultas Básicas

- Para buscar un nodo o conjunto de nodos utilizamos el comando **MATCH**
```Cypher
MATCH (p:Persona {nombre: 'María'}) RETURN p.nombre, p.prof
```
- El resultado de la consulta es un conjunto de **records**, que podemos representar con una tabla.
- También se pueden aplicar condiciones de selección sobre las búsquedas con el comando **WHERE**.
```Cypher
MATCH (m:Persona) WHERE m.color = 'Verde' RETURN m.nombre, m.prof
```

# Interrelaciones

- Podemos utilizar el comando **CREATE** para definir interrelaciones entre los nodos
```Cypher
MATCH 
	(juan:Persona {nombre:‘Juan’}),
	(lucas:Persona {nombre:‘Lucas’}),
	(edith:Persona {nombre:‘Edith’}),
	(maria:Persona {nombre:‘María’}),
	(tom:Persona {nombre:‘Tomás’}),
	(luis:Persona {nombre:‘Luis’})
CREATE 
	(juan)−[:AMIGO_DE]−>(lucas),
	(edith)−[:AMIGO_DE]−>(maria),
	(maria)−[:AMIGO_DE]−>(lucas),
	(lucas)−[:AMIGO_DE]−>(tom),
	(luis)−[:AMIGO_DE]−>(edith),
	(lucas)−[:ENEMIGO_DE]−>(edith),
	(tom)−[:ENEMIGO_DE]−>(edith),
	(tom)−[:ENEMIGO_DE]−>(luis)
```

![[Grafo Neo4j.png]]

- En Neo4j, los ejes son siempre direccionales. (Los grafos son dirigidos) a la hora de crearlos.
- Sin embargo, para trabajar con grafos no dirigidos no es necesario crear las interrelaciones en los dos sentidos. 
- Es posible indicar en la **consulta** Cypher si queremos prestar atención a la dirección de los ejes en la navegación, o no.
	- ->: Requiere que se respete la dirección del eje. 
	- -: Pasa por alto la dirección del eje en la interrelación.
- Si queremos consultar por los enemigos que tienen un amigo en común, podemos hacer

```Cypher
MATCH 
	(p1:Persona) - [:ENEMIGO_DE] - (p2:Persona) - [:AMIGO_DE] - (p3:Persona),
	(p1) - [:AMIGO_DE] - (p3)
RETURN DISTINCT p1.nombre, p2.nombre
```

- Si queremos que nos de solo un resultado por par y no los dos agregamos `->` a una de las condiciones.

```Cypher
MATCH 
	(p1:Persona) - [:ENEMIGO_DE] -> (p2:Persona) - [:AMIGO_DE] - (p3:Persona),
	(p1) - [:AMIGO_DE] - (p3)
RETURN DISTINCT p1.nombre, p2.nombre
```

- Si hubieran muchos triángulos de amigos y queremos solo un par, podemos usar distinct

```Cypher
MATCH 
	(p1:Persona) - [:ENEMIGO_DE] -> (p2:Persona) - [:AMIGO_DE] - (p3:Persona),
	(p1) - [:AMIGO_DE] - (p3)
RETURN DISTINCT p1.nombre, p2.nombre
```

- También lo podemos escribir en varias líneas

```Cypher
MATCH 
	(n:Persona) - [:ENEMIGO_DE] -> (o:Persona), 
	(n:Persona) - [:AMIGO_DE] - (m:Persona),
	(o:Persona) - [:AMIGO_DE] - (m:Persona)
RETURN DISTINCT n.nombre, o.nombre
```

- Con un `*` en la interrelación podemos indicar una cantidad indeterminada de saltos.
	- *¿A cuantos **amigos** de distancia están Juan y Luis?*
```Cypher
MATCH 
	(juan:Persona {nombre:‘Juan’}),
	(luis:Persona {nombre:‘Luis’}),
	p=( juan:Persona)−[:AMIGO_DE * ]−(luis:Persona)
RETURN length(p)
ORDER BY length(p) 
LIMIT 1
```

# Esquema general de consulta

```Cypher
MATCH p1 = pattern1, p2 = pattern2, ..., pn = patternn 
WHERE cond1, cond2, ..., condm 
RETURN pi1 , ..., agg(pj1 ), ... 
ORDER BY pik , agg(pj k 0 ), ... 
LIMIT N;
```

- Un patrón (pattern) puede especificarse a través de un nodo y sus propiedades, una interrelación y sus propiedades, o un camino y sus propiedades. A cada patrón podemos darle un nombre. 
- La cláusula WHERE dá aún más flexibilidad para filtrar los resultados basados en alguna condición. 
- Las operaciones de agregación se realizan siempre en el RETURN, aplicando funciones como count(), sum() ó max(), sin la necesidad de utilizar group by.
- También podemos usar **WITH** para tener otro pattern matcheado del que sacar datos.
- Si queremos contar la cantidad de amigos de cada persona usamos
```Cypher
MATCH p=(a:Persona) - [:AMIGO_DE] - (b:Persona) RETURN a.nombre, COUNT(p)
```