- **Capa de red**
- Es una de las capas del [[Protocolo de Capas]].
- Reside entre la [[Transport Layer|capa de transporte]] y la capa de enlace.
- Provee servicios de comunicación lógica [[End System|host]] to host.
- El protocolo más famoso que existe en esta capa es el [[Internet Protocol]].
- Para comprenderla mejor la dividimos en **data plane** y **control plane**.
	- **Data Plane:** Las funciones por [[Router|router]] par saber como se reenvía un datagrama a otro.
	- **Control Plane:** Lógica de toda la red que controla como un datagrama se traslada del host a otros routers al destinatario. 

![[Capa de red.png]]

# Redireccionar y routing

-  **Redireccionar**
	- Forwarding
	- Se implementa en el data plane.
	- Cuando un paquete llega al input link de un router, el router lo tiene que mover al output link apropiado.
	-  Se refiere a lo que sucede localmente dentro de un router al mover un paquete de un link a otro.
	- Sucede en nanosegundos
	- Se puede implementar en el hardware.
- **Rutear**
	- Routing
	- Se implementa en el control plane.
	- La capa de red debe determinar la ruta o camino tomado por los paquetes mientras estos fluyen de un emisor a un receptor.
	- Los algoritmos que los determinan se conocen como routing algorithms.
	- Se refiere a los caminos end-to-end que toman los paquetes al ser enviados 
	- Dura segundos
	- Se lo implementa en software.
![[Routing algorithms.png]]
- Para este proceso el [[Router|router]] usa su **forwarding table**.
- Los contenidos de la forwarding table del router se obtienen a través de los routing algorithms. Estos algoritmos se almacenan en cada router y se comunican con los de otros routers para generar los valores de sus forwarding tables.
- Usando Software Defined Networking (SDN), se puede tener un software conectado a cada router y que este ejecute el algoritmo de routing y les de la información necesaria para generar sus forwarding tables.
![[SDN.png]]

# Modelo de Servicios

- Los posibles servicios que la capa de red puede proveer son los siguientes.
	- **Guaranteed delivery**: Eventualmente llega al destino
	- **Guaranteed delivery with bounded delay**: El paquete llega y le podés especificar un delay.
	- **In order packet delivery:** Llegan en orden
	- **Guaranteed minimal bandwith:** Envía paquetes por debajo del bit rate del link
	- **Security;** Encriptar todos los datagramas.
- La capa de red del internet provee únicamente un servicio, **best-effort service**. Con este, no se garantiza que los paquetes sean recibidos en orden ni que siquiera sean recibidos. Tampoco se garantiza delay o bandwith. Pareciera ser un eufemismo para decir que este servicio no ofrece servicios.