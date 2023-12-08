- Es un [[Sistemas de gestión de bases de datos|SGBD]] que corre como sistema distribuido en distintas computadoras (nodos) que se encuentran sobre una red (ya sea local, a través de Internet, o como un servicio de cloud computing), aprovechando las ventajas de la computación distribuida y brindando a las aplicaciones la abstracción de ser un único sistema coherente.

# Fragmentación

- Es la tarea de dividir un conjunto de [[Agregado|agregados]] entre un conjunto de nodos.
- Se realiza con dos objetivos: 
	- Almacenar conjuntos muy grandes de datos que de lo contrario no podrían caber en un único nodo. 
	- Paralelizar el procesamiento, permitiendo que cada nodo ejecute una parte de las consultas para luego integrar los resultados. 
- Según la manera de fragmentar, podemos distinguir entre fragmentación horizontal o vertical.  Muchas veces se utiliza una combinación de ambas.
## Fragmentación Horizontal

- Los agregados se reparten entre los nodos, de manera que cada nodo almacena un subconjunto de agregados. 
- Generalmente se asigna el nodo a partir del valor de alguno de los atributos del agregado. 
## Fragmentación Vertical

- Distintos nodos guardan un subconjunto de atributos de cada agregado. 
- Todos suelen compartir los atributos que conforman la clave. 

# Replicación

- La replicación es el proceso por el cual se almacenan múltiples copias de un mismo dato en distintos nodos del sistema. 
- Nos brinda varias ventajas: 
	- Es un mecanismo de backup: permite recuperar el sistema en caso de fallas de disco o catastróficas. 
	- Permite repartir la carga de procesamiento si permitimos que las réplicas respondan consultas o actualizaciones. 
	- Garantiza cierta disponibilidad del sistema aún si se caen algunos nodos. 
- Cuando las réplicas sólo funcionan como mecanismo de backup se denominan **réplicas secundarias**. Cuando también pueden hacer procesamiento, se las conoce como **réplicas primarias**. 
- La replicación nos genera un nuevo problema a resolver: la consistencia de los datos. 
	- Puede darse la situación de que distintas réplicas almacenen (al menos, temporalmente) distintos valores para un mismo dato.