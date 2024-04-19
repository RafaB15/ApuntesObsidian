- Es una versión del [[Internet Protocol]]

# Datagrama

- Un [[Datagrama|datagrama]] en IPv6 se ve de la siguiente manera.

![[IPv6 Datagram.png]]

- Las diferencias con [[IPv4]] más importantes
	- **Se expanden las capacidades de addressing**, de 32 a 128 bits.
	- Se introdujo un nuevo tipo de dirección llamado **anycast**, para mandar un mensaje a un grupo de [[End System|hosts]].
	- 40 bytes fijos de longitud.
	- Flow labeling, que puede ser para demandar una calidad de servicio específica o servicio en tiempo real.

- Se definen los siguientes campos
	- **Versión**. IP version.
	- **Traffic Class:** Se puede usar para dar prioridad a ciertos datagramas adentro de un flow o provenientes de ciertas aplicaciones.
	- **Flow label**: Se utiliza para identificar un flow de datagramas.
	- **Payload length**: Longitud del payload.
	- **Next Header**: Identifica el protocolo de la capa de transporte ([[Transmission Control Protocol|TCP]] o [[User Datagram Protocol|UDP]]),
	- **Hop Limit**: Se decrementa este número en uno por cada [[Router|router]] que retransmita el datagrama. Similar al TTL de IPv4.
	- **Source and destination addresses**: El address
	- **Data** El payload.

- Diferencias con el datagrama de IPv4:
	- **Fragmentación:** 
		- IPv6 no permite fragmentación y reensamblado en los routers intermedios, sino que estas operaciones solo se pueden llevar a cabo por los host fuente y destino.
		- Si el datagrama recibido por un router es demasiado grande, este lo droppea, y manda un mensaje "Packet Too Big".
		- El emisor puede entonces volver a enviar los datos pero con un datagrama más pequeño.
	- **Header Checksum**:  No se tiene un checksum, confiando en que los de las capas de más arriba agarrarán esos errores. Ahorra tiempo.
	- **Options field**: Ya no está pero puede ser parte del Next Header.