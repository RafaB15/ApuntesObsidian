- **TCP**.
- Es un [[Transport Layer|protocolo de la capa de transporte]] para ser usado por aplicaciones en la [[Application Layer|capa de aplicaciones]].
- Este modelo de servicio incluye un servicio orientado a la conexión y [[Transmisión confiable de datos|transmisión confiable de datos]].
- TCP también implementa un mecanismo de [[Control de Congestión|control de congestión]]. Cuando hay mucha congestión en la conexión entre cliente y servidor esta se controla.
- TCP no provee ninguna encriptación. Para eso se creo una mejora llamada **Secure Sockets Layer (SSL)** en la capa de aplicación. Para usar un SSL socket API hay que incluir las bibliotecas pertinentes en el cliente y el servidor.
- Este protocolo extiende [[Internet Protocol|el servicio de entregas del IP]] entre dos [[End System|end systems]] para convertirlo en un servicio de entrega entre dos procesos corriendo en los end systems.
- TCP convierte el servicio de transporte de datos entre hosts **no confiable** de [[Internet Protocol|IP]] en un servicio de transporte de datos entre procesos **confiable**.
# Características
## Servicio orientado a la conexión

- TCP hace que el cliente y el servidor intercambien información de control de la [[Transport Layer|capa de transporte]] antes de mandarse mensajes de la [[Application Layer|capa de aplicación]].
- Es un **handshake** que alerta al cliente y al servidor, para prepararlos para recibir mensajes.
- Después del handshake es que se dice que existe una conexión TCP entre los [[Socket|sockets]] de los dos [[Redes/2. Application Layer/Proceso|procesos]].
- Esta es una **full-duplex connection** debido a que los dos procesos pueden mandar mensajes al otro al mismo tiempo mientras la conexión siga activa.
- Cuando se termina de mandar mensajes, se destruye la conexión.
- No se permite el multicasting (un sender, muchos receivers).

## Transferencia confiable de datos

- Se confía en TCP para entregar toda la data sin ningún error y en el orden correcto, sin ningún byte duplicado o perdido.

## Conexión persistente

- Dependiendo del programa, se puede decidir mantener una única conexión TCP activa y mandar mensajes en esta, o abrir una nueva conexión para cada request.
- Si se usa una misma conexión TCP, se dice que es una **persistent connection**. De lo contrario, sería una **non-persistent connection**.

# Multiplexación y desmultiplexación

- En la [[Transport Layer|capa de transporte]] se da la [[Transport Layer#Multiplexación y desmultiplexación|multiplexación y desmultiplexación]].
- A diferencia de [[User Datagram Protocol|UDP]], los [[Socket|sockets]] de TCP se identifican con una tupla de 4 valores: Dirección IP fuente, [[Puerto]] Fuente, Dirección IP destino, Puerto Destino.
- Con lo cual, si dos mensajes vienen de distintos lugares, pero van al mismo destino, cada uno llegará por un socket distinto.

# Funcionamiento
- Primero se hace el three way handshake. El cliente le mando un mensaje sin payload al servidor y este le responde con uno de la misma forma. Luego el cliente le manda un mensaje que sí puede tener payload y eso concluye el 3 way handshake.
- Cuando se quiere mandar un mensaje, este se manda primero a un **send buffer** (se reserva durante el 3-way handshake), y eventualmente TCP agarrará pedazos de ese buffer y los mandará a la [[Network Layer|capa de red]].
- Cuantos datos se pueden poner en un [[Segmento|segmento]] depende del MSS, maximum segment size.
- Se forman **segmentos TCP** emparejando un pedazo de client data con un header. Luego se mandan a la capa de red que los encapsula en datagramas IP de la network layer. Al llegar a su destino, el segmento se pone en el **buffer de recibidos** de la conexión TCP.

![[TCP process.png]]

## Segmentos TCP

![[TCP segment structure.png]]

- Los **secuence number field** y **acknowledgement number field** se usan para hacer un servicio de transporte confiable.
- La **receive window** es para control de flujo (la cantidad de bytes que el receiver está dispuesto a aceptar).

### Sequence Number y Acknowledgment Numbers

![[Seq numer y Ack number TCP.png]]

- Los números de secuencia tienen que ver con el stream de bytes transmitidos, y no con el número de segmento.
- El **número de secuencia de un segmento** es el número del stream de bytes del primer byte en el segmento. El primer número de secuencia se elige al azar.
- El **acknowledgment number** de un segmento es el número de secuencia del próximo byte que el host está esperando del host con el que está conectado.
- Como TCP reconoce (ack) los bytes hasta el primer byte faltante en el stream, se dice que TCP provee **cumulative acknowledgments**.
- Al mandar mensajes estos dos parámetros se van cambiando para saber si se perdió algún paquete. Al mandar un mensaje con un número de secuencia te pueden devolver paquetes con un campo ACK (no acknowledgment number) válido, lo cual te indica que le llegó bien o no. También se pone un timer, y si no te llegó en el tiempo estipulado lo mandás de vuelta. EL timer aumenta con cada retransmisión.
- Fast retransmit: Retransmitir el código rápidamente cuando se sospecha que se perdió, aunque no pasara en tiempo necesario para confirmalo.
- TCP se parece a [[Transmisión confiable de datos#Go-Back-N (GBN)|GBN]], pero tiene diferencia, como a veces guardar buffers y pedir la retransmisión de un solo paquete.
- Mientras se mandan mensajes, se van dando información acerca de los buffers para que frenen un poco si es que están por llenarlos.


## Manejo de conexión

- Al empezar una conexión TCP se tiene que hacer el three way handshake
	- Primero el cliente TCP manda un segmento especial al servidor TCP. Este no contiene datos de la capa de aplicación, sino que tiene uno de sus flag bits conocido como **SYN** seteado en 1. Por eso se refiere a este segmento como **segmento SYN**. El cliente también elige al azar un sequence number inicial y lo pone en este mensaje.
	- Cuando este segmento llega al servidor, el servidor reserva espacio para los buffers y variables correspondientes a la conexión y manda un segmento que simboliza que acepta la conexión al cliente. Este segmento tampoco tiene payload, pero tiene 3 cosas importantes en su header. El SYN bit está en 1, el acknowledgment field está seteado a "num_de_secuencia_cliente" + 1 (lo cual significa que el servidor confirma haber recibido bien el número), además el servidor también setea su propio sequence number inicial random y lo pone en su campo correspondiente en el header. Se conoce a este segmento como **segmento SYNACK**
	- Al recibir el SYNACK, el cliente reserva memoria para los buffers y variables correspondientes a la conexión. Luego mando un nuevo mensaje al servidor, el cual reconoce que se recibió la información de conexión del servidor (ponemos el número de secuencia que nos mandaron + 1 en el acknowledgment field), se pone el SYN bit en cero, ya que la conexión está establecida. Este mensaje ya puede cargar con payload si quiere.

![[Three way handshake.png]]

- Para terminar una conexión TCP se manda un segmento por parte del cliente con el bit FIN puesto en 1. Luego el servidor hace lo mismo y el cliente le vuelve a mandar un mensaje de acknowledgment. Para este punto los buffers y variables deben estar deallocados.

![[Cerrar conexión TCP.png]]

- Ciclo de una conexión TCP:

![[TCP lifecycle client.png]]

![[TCP lifecycle server.png]]

- Si nos mandan un mensaje dirigido a un puerto que no tenemos aceptando conexiones, devolvemos un mensaje con la flag RST puesta en 1 para que no nos vuelvan a mandar ese mensaje.

# Control de congestión

- Este protocolo implementa [[Control de Congestión|control de congestión]].
- Hace uso de **End-to-end congestion control**.
- TCP hace que cada emisor limite el ratio al que encía tráfico a su conexión en función de la congestión de red percibida.
	- Si ve que hay poca congestión, incrementa su ratio de envío.
	- Si ve que hay mucha congestión, decrementa su ratio de envío.
- El lado que envía información tiene una variable que es la **ventana de congestión** (congestion window), denotada **cwnd**. 
- La congestion window impone una restricción en cómo puede mandar tráfico a la red la conexión TCP.
- La cantidad de datos sin reconocer no puede superar a la ventana.
$$\text{LastByteSent} - \text{LastByteAcked} \le \min(\text{cwnd}, \text{rwnd})$$
- **rwnd:** Es el espacio faltante receive buffer que obtenemos de la otra parte de la conexión tcp. Nos indica cuantos bytes más puede recibir y guardar. Si nos pasamos probablemente los desechen.
## Principios
- TCP utiliza los siguientes principios para saber cómo comportarse
- **Un segmento perdido implica congestión, y por ello, el ratio en envío del TCP se debería reducir cuando se pierde un segmento**
	- Si nos mandan 4 ACKS iguales (uno original y 3 duplicados) u ocurre un timeout es interpretado como una pérdida que genera la retransmisión del segmento. Se tiene que decrementar la congestion window size.
- **Un segmento ACK indica que la red está entregando los segmentos del emisor al receptor, y por ello, el ratio del emisor puede ser incrementado cuando un ACK llega para un segmento previamente no reconocido**
	- La llegada de ACKS se toma como un indicativo de que todo está bien y que la red no está congestionada. Se puede aumentar la congestion window size.
- **Bandwith probing**
	- TCP incrementa su ratio de transmisión en respuesta a los ACKS hasta que ocurre un evento de pérdida, en el que el ratio de transmisión decrece.
	- TCP entonces va aumentando su ratio de transmisión nuevamente de a poco hasta que se genere la congestion nuevamente, para ver si puede llegar a un ratio más grande.

## Algoritmo de controld e congestión

### Slow Start

- Al empezar la conexión se inicializa el valor de **cwnd** a 1 **MSS** (minimum size segment). El sending rate incial es entonces $\frac{MSS}{RTT}$.
- En slow start, el valor de **cwnd** va a aumentar en un MSS por cada ACK que recibamos para un segmento sin reconocer.

![[Slow start.png]]
- Hay una variable llamada **ssthresh** (slow start thresshold), la cual **cwnd** no puede superar mientras crece. Al principio esta variable se setea en el valor más grande que puede tener (16 bits, 65535).
- El crecimiento exponencial de slow start termina en dos casos
	- Si hay un evento de pérdida por un timeout se setea el **cwnd** a 1 MSS y se empieza con el slow start de nuevo, pero setteando el valor de **ssthresh** a $\frac{cwnd}{2}$, la mitad de la ventana al encontrar detectar la congestión.
	- Si **cwnd** aumenta hasta alcanzar el valor de **ssthresh**. Cuando esto sucede pasamos de slow start a **congestion avoidance**.
	- Si recibimos 3 ACKS duplicados, TCP hace un fast retransmit y entra en el fast reovery state.

### Congestion Avoidance

- Al entrar en este modo, **cwnd** es aproximadamente la mitad de su valor cuando se encontró una congestión por última vez.
- Como se encontró congestión no muy lejos de este valor la última vez, avanzamos más despacio.
- Ahora el valor de cwnd se va a aumentar de a 1 MSS por cada RTT. Esto se puede hacer aumentando cwnd en MSS (MSS/cwnd), cada vez que llegue un paquete.
- Si ocurre un timeout, congestion avoidance hace lo misom que se hacía en Slow Start.
- Si se reciben 3 ACKS, TCP divide el valor de **cwnd** a la mitad y se actualiza ssthresh a la mitad del valor viejo de cwnd. Luego se entra en Fast Recovery.

### Fast Recovery

- Se incrementa el valor de **cwnd** en 1 MSS por cada ACK duplicado recibido por el segmento perdido que causó que TCP entrara en este estado. 
- Cuando lega un ACK por el segmento perdido, se vuelve al congestion avoidance state después de desinflar cwnd.
- Si sucede un timeout, se pasa al slow start después de cortar cwnd y actualizar ssthresh.

![[Cognestion control.png]]

- A este algoritmo se lo conoce como **additive-increase, multiplicative-decrease (AIMD)**.