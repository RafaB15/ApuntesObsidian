- **Capa de aplicación**.
- Es una de las capas del [[Protocolo de Capas]].
- Es donde residen las aplicaciones de red y sus protocolos de la capa de aplicación.

# Principios

- Cuando desarrollamos una aplicación, debemos escribir software que pueda ejecutarse en múltiples [[End System|end systems]].
- No tiene que correr en aparatos propios del [[Red#Núcleo de Red|núcleo de la red]] como lo son [[Packet Switches|routers]], pues estos solo pueden ejecutar código de capas más abajo en el protocolo.
- La comunicación de una aplicación de red toma lugar **entre end systems en la capa de aplicación**.

![[Comunicación en application layer.png]]

# Arquitectura

- No hay que confundir la arquitectura de una red ([[Protocolo de Capas#Arquitectura de capas|5 capas]]) con la arquitectura de una aplicación.
- La arquitectura de la aplicación es diseñada por el desarrollador de la aplicación y dictamina como la aplicación está estructurada entre los diferentes [[End System|end systems]].
- Normalmente se decantan por uno de los 2 paradigmas más predominantes, [[Arquitectura Cliente-Servidor]] o [[Arquitectura peer-to-peer]].

# Comunicación entre procesos

- Los diferentes [[Redes/2. Application Layer/Proceso|procesos]] ejecutándose en diferentes hosts se tienen que comunicar a través de la red en esta capa.
- La mayoría de las aplicaciones consisten en pares de [[Redes/2. Application Layer/Proceso|procesos]] comunicándose, con ambos mandándose mensajes.
- Cualquier mensaje mandado desde un proceso a otro debe pasar por la red que está debajo.
- Un proceso manda mensajes a y recibe mensajes de la red a través de una interfaz de software llamada [[Socket|socket]], el cual hace de interfaz entre la capa de aplicación y la [[Transport Layer|capa de transporte]].
- Los desarrolladores de aplicaciones tienen el control de todo lo que pasa del lado de la capa de aplicación en el [[Socket|socket]], sin embargo, se tiene poco o nada de control sobre lo que pasa en el lado de la [[Transport Layer|capa de transporte]]. Como máximo raras veces pueden elegir el protocolo de transporte y setear algunos parámetros.

![[Procesos comunicándose.png]]

- Para poder mandar [[Paquete|paquetes]] de un [[Redes/2. Application Layer/Proceso|proceso]] a otro, el destinatario necesita una dirección. Se tiene que especificar:
	- La dirección del [[End System|host]] del destinatario. En el internet, a un host lo identifica su dirección IP (32 bits, unique identifier).
	- Un identificador que especifique al proceso destino (o más específicamente, socket destino) dentro de su host. Esto se identifica con el **número de puerto**.
- La capa de transporte nos ofrece diferentes protocolos para mandar mensajes que pueden implementar diferentes [[Servicios de transporte|servicios]].
- El internet, o más específicamente las redes TCP/IP, ofrecen dos protocolos de transporte a las aplicaciones: [[User Datagram Protocol|UDP]] y [[Transmission Control Protocol|TCP]]. Estos dos protocolos no ofrecen garantías de tiempo ni rendimiento, pues lidian con su falta de otras maneras.

![[Diferentes aplicaciones y el protocolo que usan.png]]

# Protocolos

- Un protocolo de la capa de aplicación define como los [[Redes/2. Application Layer/Proceso|procesos]] de una aplicación, corriendo en diferentes [[End System|end systems]], se mandar mensajes.
- En particular se define:
	- Los tipos de mensaje intercambiados (request messages, response messages).
	- La sintaxis de los diferentes tipos de mensajes, como los campos en el mensaje y como estos están delimitados.
	- La semántica de los campos, que vendría a ser el significado de la información en los campos.
	- Reglas para determinar cuando y como un proceso manda mensajes y responde mensajes.
- Algunos protocolos de la capa de aplicación están especificados en RFCs y, por ende, en el dominio público.
- No hay que confundir protocolo de la capa de aplicación, con aplicación de red, pues el primero es solo una aprte del segundo.
- Algunos protocolos conocidos son:
	- [[HyperText Transfer Protocol]]
	- [[Simple Mail Transfer Protocol]]
	- [[Domain Name System]]