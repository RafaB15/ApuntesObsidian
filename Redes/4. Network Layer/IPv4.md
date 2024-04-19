- Es una versión del [[Internet Protocol]]
# Datagrama

- Un [[Datagrama|datagrama]] en IPv4 se ve de la siguiente manera

![[IPv4 datagram.png]]
- Sus componentes son los siguientes
	- **Version Number:** Versión del datagrama. En este caso será IPv4.
	- **Header Length:** Nos dice donde empieza el payload.
	- **Type of Service:** Distingue los tipos de datagramas, como los que se usan para telefonía y los que se usan para trafico que no es de tiempo real.
	- **Datagram Length:** Largo total del datagrama.
	- **Identifier, flags, fragmentation offset:** Tienen que ver con fragmentación de IP. IPv6 no los tiene.
	- **Time to live:** Se incluye para asegurarse que los datagramas no circulen para siempre. Se reduce en uno cada vez que el datagrama es procesado por el router.
	- **Protocol:** Especifica el protocolo de la capa de transporte. 6 es [[Transmission Control Protocol|TCP]] y 17 es [[User Datagram Protocol|UDP]].
	- **Header Checksum**: Para encontrar errores.
	- **Source and destination IP addresses**: El título.
	- **Options:** Permiten que un header se pueda extender. No están incluidas en IPv6.
	- **Data(Payload)**: Es el payload.
	- El header IP es de 20 bytes. Si tiene un payload TCP entonces son 20 bytes de IP header y 20 bytes de TCP header.

# Fragmentación de datagrama

- Los datagramas de la capa de red están envueltos en un frame de la capa de link, siendo el máximo tamaño que puede llevar conocido como **maximum transmission unit (MTU)**. Este valor puede cambiar de link a link. 
- Debido a esto, a veces se da que te llega un datagrama que es más grande que el MTU del link al que lo tenés que mandar, lo cual genera que lo tengamos que **fragmentar**.
- A las partes en las que separamos el datagrama se los conoce como **fragmentos** y se los encapsula en frames separados y manda por el link.
- La responsabilidad de rearmar los pedazos de los datagramas en el datagrama completo yace en el [[End System|end system]] que lo recibe. Este tiene que discernir si los paquetes que le están llegando de la misma fuente son fragmentos. Para esto se usan el Identifier, flags, fragmentation offset del header.
	- Flag es cero para el último datagrama
	- El offset es para saber el orden.
	- El identifier es para diferenciarlos.

![[Fragmentación de datagrama.png]]

# Addressing

- Un host normalmente tiene un único link hacia la red. El límite entre este link y el host se conoce como [[Interface|interface]].
- Los routers tienen do o más links a los que están conectados. El límite entre el router y cualquiera de sus links también se conoce como interface.
- Debido a que todos los hosts y routers tiene la capacidad de enviar y recibir [[Datagrama|datagramas]] IP, [[Internet Protocol|IP]] requiere que cada uno de estos tenga una [[Dirección IP|dirección IP]]. Por lo que la dirección IP está relacionada en realidad con la interfaz más que con cada dispositivo.