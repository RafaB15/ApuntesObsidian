- Un socket es la interfaz entre la [[Application Layer|capa de aplicación]] y la [[Transport Layer|capa de transporte]].
- También se le refiere como **Application Programming Interface (API)** entre la aplicación y la [[Red|red]], dado que el socket es la interfaz de programación con el cual se construyen aplicaciones en la red.
- Los [[Redes/2. Application Layer/Proceso|procesos]] tienen uno o varios sockets disponible y, cuando quieren mandar un mensaje por la red, lo ponen en el socket en la capa de aplicación, el cual hace uso de los servicios disponibles en la capa de transporte para hacerlo llegar hasta el socket del proceso destino.

![[Procesos comunicándose.png]]

- Se identifican de distintas formas dependiendo de si el protocolo de la [[Transport Layer|capa de transporte]] siendo usado es [[Transmission Control Protocol|TCP]] o [[User Datagram Protocol|UDP]].
	- **UDP**: El socket es identificado por una tupla de dos valores.
		- (Dirección IP destino, Número de [[Puerto|puerto]] destino).
	- **TCP:** El socket es identificado por una tupla de cuatro valores.
		- (Dirección IP emisor, Número de [[Puerto|puerto]] emisor, Dirección IP destino, Número de puerto destino).
- Con lo cual si se usa UDP, cualquier mensajes que nos llegue para un puerto específico llega a ese socket independientemente de quien lo envíe, pero en el caso de TCP, como los sockets se identifican también por quién lo envía, se usan diferentes socket por cada emisor.
![[Diferentes tipos de sockets.png]]

- En python por ejemplo, un socket tcp tiene un método accept(). a través del cual se acepta una conexión en un puerto. Este método devuelve a su vez un socket, que es el que está conectado con el cliente. Por lo que este socket que se devuelve está identificado por la ip y puerto del socket donde estaba escuchando y la ip y puerto del cliente que hizo la conexión.
- En udp no hay un método accept, sino que simplemente tenemos el rcvfrom, que también nos devuelve información acerca del que emisor, pero que lo mande quien lo mande siempre cae en el mismo lugar.
- 