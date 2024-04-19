- **Capa de transporte**.
- Es una de las capas del [[Protocolo de Capas]].
- Reside entre la [[Application Layer|capa de aplicación]] y la [[Network Layer|capa de red]].
- Es la capa que provee servicios de comunicación a los [[End System|hosts]] en la capa de aplicación.

# Protocolos

- Los protocolos de la capa de transporte proveen **comunicación lógica** entre [[Application Layer|procesos de aplicación]] corriendo en hosts distintos.
- Los protocolos más conocidos son [[Transmission Control Protocol|TCP]] y [[User Datagram Protocol|UDP]].

![[Protocolo de transporte.png]]

- Los protocolos de la capa de transporte se implementan en los [[End System|end systems]], pero no en los [[Packet Switches|routers de red]]. 
- En el lado que envía un mensaje, la capa de transporte recibe un mensaje de la capa de aplicación para ser enviado. Este los transforma en paquetes de la capa de transporte, mejor conocidos como [[Segmento|segmentos de la capa de transporte]]. 
- La capa de transporte le pasa los segmentos a la [[Network Layer|capa de red]], donde se lo encapsula en un network-layer packet (datagrama) y se manda al destino. Como los routers de red actúan en la red, podrán leer la información añadida por la capa de red para llegar a su destino.
- Entonces los protocolos de la capa de transporte **viven en el host** y se encargan de al recibir mensajes de la red, hacer que lleguen al **proceso** correcto. Cuando mandamos un mensaje lo llevan hasta el filo de la red, en donde se lo delegan a la capa de red para que lo mande al host.

# Relación con la capa de red

- Mientras que los protocolos de la capa de transporte proveen comunicación lógica entre **procesos corriendo en diferentes hosts**, los protocolos de la [[Network Layer|capa de red]] proveen comunicación lógica entre **hosts**.
- En un [[End System|end system]], la capa de transporte se encarga de mover los mensajes de los procesos a la capa de red y viceversa, pero no tiene un decir en como los mensajes se mueven en el núcleo de la red.
- El servicio de transporte proveído por la [[Network Layer|capa de red]] es el [[Internet Protocol|IP]].

# Multiplexación y desmultiplexación

- **Multiplexing and Demultiplexing**.
- Es el proceso a través del cual se extiende el modelo de transporte de datos [[End System|host]]-to-host a uno [[Redes/2. Application Layer/Proceso|process]]-to-process para las aplicaciones que corren en los hosts.
- Cuando la capa de transporte recibe un segmento de la capa de red, esta tiene que mandarlo al proceso adecuado, o más bien, al [[Socket|socket]] adecuado dentro de ese proceso.

![[Multiplexing y demultiplexing.png]]

- Los [[Segmento|segmentos]] tienen información que ayuda a identificar el socket específico al que van dirigidos, pues los sockets tienen identificadores únicos dentro de un host.
- **Demultiplexación:** Entregar datos en un segmento de la capa de transporte al socket correcto.
- **Multiplexación:** Encapsular los conjuntos datos de diferentes sockets en el host fuente, encapsular cada conjunto de datos con información en el header para crear segmentos y pasar los segmentos a la capa de red.

![[Diferentes tipos de sockets.png]]