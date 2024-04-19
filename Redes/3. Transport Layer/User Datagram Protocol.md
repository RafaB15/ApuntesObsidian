- **UDP**
- Es un [[Transport Layer|protocolo de la capa de transporte]] para ser usado por aplicaciones en la [[Application Layer|capa de aplicaciones]].
- Es un protocolo de transporte sin lujos y ligero, que provee [[Servicios de transporte|servicios]] mínimos.
- No tiene conexión, por lo que no hay un **handshake** antes de empezar a mandar mensajes en la [[Application Layer|capa de aplicación]].
- Es un servicio de transferencia de datos no confiable, por lo que UDP no provee ninguna garantía de que los mensajes que pongas en un socket UDP van a llegar al destinatario. 
- Los mensajes que sí llegan a su destino pueden estar en el orden equivocado.
- No incluye un mecanismo de control de congestión, a diferencia de [[Transmission Control Protocol|TCP]].
- Incluye chequeo de integridad en los headers de los [[Segmento|segmentos]] que envía.
- Este protocolo extiende [[Internet Protocol|el servicio de entregas del IP]] entre dos [[End System|end systems]] para convertirlo en un servicio de entrega entre dos procesos corriendo en los end systems.
- [[Domain Name System|DNS]] es un protocolo de la capa de aplicación que usa UDP.
- En caso de que se le quiera agregar confianza a UDP para no perder información, esa lógica se puede agregar en la capa de aplicación programando diferentes chequeos, para tener sus ventajas y mitigar un poco sus desventajas.
# Multiplexación y desmultiplexación

- En la [[Transport Layer|cada de transporte]] se da la [[Transport Layer#Multiplexación y desmultiplexación|multiplexación y desmultiplexación]].
- Si el protocolo a utilizar es UDP, entonces no se agrega mucho más. Los segmentos en la capa de transporte se convierten en [[Datagrama|datagramas]] en la capa de red con el agregado de headers, y estos son enviados hacia el host destino.
- Los sockets UDP se identifican únicamente con una tupla de dos valores, con el port destino y la dirección IP destino, con lo que si dos de estos mensajes vienen de distintos lugares, pero hacia el mismo port y el mismo host, entonces llegarán por el mismo UDP socket.

# Ventajas

- Más control a nivel aplicación de qué datos se mandan y cuando.
	- Al no haber un sistema de control de congestión como en TCP, los mensajes se pueden llegar a mandar más rápido.
- No hay conexión.
	- A diferencia de TCP que tiene que hacer el three way handshake.
- No hay estado de la conexión.
	- No trackea parámetros acerca de lo que ha pasado en la conexión, pues no hay una conexión continua.
- [[Segmento|Segmentos]] con headers más pequeños.
	- TCP tiene headers de 20 bytes, UDP de 8 bytes.

# Estructura de segmento

- Los [[Segmento|segmentos]] enviados por un [[Socket|socket]] UDP contienen 4 campos: Dirección IP destino, [[Puerto]] destino, Largo (número de bytes) y un checksum, para corroborar que la información no nos llegó corrompida.

![[UDP segment.png]]