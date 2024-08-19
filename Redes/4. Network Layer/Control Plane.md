- Es el plano de la [[Network Layer|cada de red]] que se encarga de la lógica de toda la red que controla como un [[Datagrama|datagrama]] se traslada del [[End System|host]] a otros [[Router|routers]] al destinatario.
- **Per router control:** Un algoritmo de ruteo corre en cada router, con una función de redireccionamiento y ruteo contenida en cada uno. Los componentes de ruteo de cada router se comunican entre sí en el plano de control.

![[Per router data plane.png]]

- **Control centralizado lógicamente**: Un controlador lógicamente centralizado computa y distribuye las tablas de ruteo a usar por cada router. El controlador se comunica con un control agent (CA) en cada router.

![[Logically centralized routing controller.png]]

# Algoritmos de ruteo

- $G = (N, E)$ es un set de *N* nodos y una colección de *E* vértices.
![[Grafo de routers.png]]

- Para cualquier par de nodos $(x,y)$ en *E*, $c(x,y)$ es el costo del vértice entre los nodos *x* e *y*.
- Si no pertenecen a *E* este costo es infinito. 
- **Algoritmos de ruteo centralizados:** Computa un camino de menor costo entre una fuente y un destino teniendo conocimiento completo acerca de la red. Si tienen información acerca de los links entre los routers se los conoce como **Link-state (LS) algorithms**.
- **Algoritmo de ruteo descentralizado:** El cálculo del camino de menor costo se lleva a cabo de una manera iterativa y distribuida por los routers.
- **Static routing algorithms**: Los costos varían lentamente con el tiempo.
- **Dynamic Routing Algorithms:** Cambian los caminos cuando cambia la topología o carga el tráfico.
- **Sensibles a la carga o no:** Varían con la congestión. Si uno tiene mucho costo por congestión se lo rodea. Hoy la mayoría son load insensitive.

## Link-State (LS) Routing Algorithm

- Se conoce la topología de la red y todos los costos. Se los da de input al algoritmo.
- El algoritmo de Dijkstra es uno.
![[Dijkstra.png]]

![[Dijkstra algorithm.png]]
## Distance Vector Routing Algorithm

- Algoritmo iterativo, asincrónico y distribuido.
- Es distribuido porque cada nodo recibe información de uno o más de sus vecinos directamente conectados,  hace un cálculo, y distribuye los resultados del cálculo de vuelta a sus vecinos (nodos conectados).
- Es iterativo porque el proceso continúa hasta que ya no haya más información para compartir entre nodos.
- Es asincrónico debido a que no requiere que todos los nodos estén fijados los unos con los otros.
- Es self_terminating, no requiere de una señal para terminar, simplemente lo hace.
- Algoritmo de Bellman Ford.

![[Distance Vector Algorithm.png]]

![[DV algorithm.png]]

# Intra-AS Routing

- Se refiere a organizar los routers en **autonomous systems (ASs)**, cada uno consistiendo en u grupo de routers que están bajo el mismo control administrativo.
- Se identifican por su autonomous system number, el cual es globalmente único.
- En un AS pueden haber **routers internos** que solo se comunican con otros routers dentro del AS, o **gateway routers** que se comunican con routers dentro de otros ASs.
- Los routers dentro del mismo AS corren el mismo algoritmo de ruteo y tienen información de los otros. A estos algoritmos de ruteo se los conoce como **intra-autonomous system routing protocol**
## Open Shortest Path First (OSPF)

- Es un protocolo de link-state que usa un flooding de link-state information y un algoritmo de camino menos costoso de Dijkstra.
- Con este algoritmo cada router construye un grafo del AS completo.
- Cada router corre Dijkstra localmente para saber el camino más corto a cada nodo desde él.
- El administrador de red se encarga de asignar los pesos.

# Ruteo entre ISP

- Para rutear un paquete entre muchos sistemas autónomos necesitamos un **Inter-autonomous system routing protocol**.
- Como se comunican muchos AS, estos tiene que estar corriendo el mismo protocolo de inter AS (no confundir con el intra que vimos antes). Este protocolo es el BGP

## Border Gateway Protocol

- Es el protocolo que une los diferentes [[Internet Service Provider|ISPs]].
- En la tabla de redirecciones de un [[Router|router]], las entradas en la tabla para direcciones dentro de la misma AS se determinan con los protocolos de Intra-AS, pero para los destinos afuera del AS, se encarga BGP.
- Se usan prefijos de la forma $138.16.68/22$ para mapear conjuntos de sub redes.
- BGP le provee a cada router una manera de:
	- Obtener información acerca del prefijo de alcance de los ASs vecinos. 
		- En otras palabras, lo deja publicar el suyo propio para no estar aislado.
	- Determina la mejor ruta a estos prefijos.
		- Corre una BGP route selection procedure localmente.
- BGP también es usado para implementar el servicio anycast de IP.

### Advertising BGP Route Information

- Los gateway routers de una AS tienen conexiones BGP externas (eBGP) mientras que los routers internos tienen conexiones BGP internas (iBGP).
- En estas conexiones van publicitando que existen y se retransmite por todas las AS, quienes transmiten también que para llegar a esta nueva red tienen que pasar por ellos, creando así una ruta.

![[BGP connections.png]]

## Eligiendo la mejor ruta

- Al publicitar prefijos, con estos también se tiene la información de los AS por los que hay que pasar para llegar a una subnet llamado **AS-PATH**. Esto ayuda a prevenir loops al poder descartar todas las rutas que te lleguen en donde esté tu propio AS.
- Otra variable que se manda es el **NEXT-HOP**, que es la dirección IP de la interfaz de router que empieza el **AS-PATH**.
- Cada **ruta BGP** se escribe como una lista con tres componentes: **NEXT-HOP, AS-PATH, destination prefix**.

### Hot Potato Routing

1. Aprende de tu protocolo inter-AS que la subnet **x** es alcanzable a través de múltiples gateways.
2. Usar la información de ruteo del protocolo intra-AS para determinar los costos del camino con menor costo a cada uno de los gateways
3. Hot Potato Routing -> Elegimos el gateway con el menor costo mínimo.
4. Determinamos por la forwarding table la interfaz **I** que lleva a la gateway de menor costo. Entramos en **(x,I)** en la forwarding table.