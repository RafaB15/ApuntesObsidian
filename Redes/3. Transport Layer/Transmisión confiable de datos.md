- **Reliable data transfer**
- La transmisión de datos confiable es una característica que puede estar presente en los protocolos de la [[Transport Layer|capa de transporte]]  hacia abajo.
- Se refiere a la garantía de entregar todos los datos enviados sin ningún error, en el orden correcto, sin ningún bit duplicado o perdido.

![[Servicio de transmisión confiable visto desde la aplicación.png]]

- Está presente en [[Transmission Control Protocol|TCP]], la cual al estar construida en la capa de transporte se posiciona por arriba de otro protocolo, [[Internet Protocol|IP]], el cual no es confiable.

![[Vista de como ve TCP a IP.png]]

# Estructura de un protocolo de transmisión confiable

- El protocolo en la capa de transporte va a hacer uso del protocolo en la capa de red, el cual no es confiable. Será necesario entonces que implementemos ciertos mecanismos en la capa de transporte para cerciorarnos de que los mensajes hayan llegado bien y lidiar con los casos en que no.

## Errores de bits

- Cuando los bits son transmitidos, almacenados y propagados pueden ocurrir errores por los que un 0 pasa a ser 1 o viceversa.
- Para lidiar con eso se implementa un **protocolo ARQ (Automatic Repeat reQUest)**.
- Este protocolo necesita de 3 capacidades:
	- **Detección de errores:** Se necesita un mecanismo para saber cuando han ocurrido errores (checksum).
	- **Feedback del receptor:** Se manda un mensaje positivo (ACK) o negativo (NAK) dependiendo de si el mensaje llegó correctamente o no.
	- **Retransmisión:** Un paquete que fue recibido con errores será retransmitido por el emisor. Solo se empezarán a mandar nuevos paquetes cuando el último paquete haya sido recibido correctamente (**stop-and-wait protocol**).
	![[stop and wait.png]]
- Para lidiar todavía más con los errores, podemos agregar un sequence number y hacer operaciones con él. Si usamos el protocolo stop-and-wait entonces podemos representarlo con un bit e ir intercalando entre 0 y 1 (**alternating-bit protocol**). Si nos llegan dos 0 o 1 seguidos entonces nos **reenviaron** el paquete, el cual puede que ya tengamos bien guardado (paquete duplicado) y nos lo reenviaron por precaución (les llegó corrompido el ACK), entonces sabemos que no lo tenemos que guardar pero igual mandamos un ACK.

## Pérdida de paquetes

- De parte del emisor, si no se recibe un **ACK** después de un tiempo estimativo de cuanto tuvo que haberse tardado (es un tiempo probable pero no certero), el emisor retransmite el mensaje.
- Se necesitará un timer para esto.

# Protocolo de pipeline

- Pipelined protocol.
- El hecho de que el protocolo sea **stop-and-wait** genera que sea algo lento.
![[Pipelined protocol.png]]

- Con **stop-and-wait** el emisor suele estar desutilizado, pues tiene que esperar mucho tiempo entre mandar un paquete y recibir un ACK. 
- Stop and wait:
![[Stop and wait computers.png]]

- Pipilining:

![[Pipelining computers.png]]

- En pipelining, el emisor tiene permitido mandar varios paquetes consecutivamente, sin esperar por confirmación de que fueron recibidos bien.
- Para que se de esto, se tienen que dar también las siguientes cosas:
	- Se tiene que aumentar el rango de sequence numbers, pues ahora pueden haber muchos paquetes en tránsito.
	- El sender y el receiver tendrán que tener paquetes en buffers por si todavía no se confirmó que fueron recibidos bien
	- A veces se necesitará que el receptor guarde en un buffer paquetes bien recibidos para su uso en recuperación de errores (Selective-repeat).

## Go-Back-N (GBN)

- En este protocolo, el emisor puede mandar múltiples paquetes sin esperar por confirmaciones, pero solo puede tener un número máximo *N* de paquetes sin confirmar en el pipeline en un debido momento.

![[GBN sequence numbers.png]]

- Al *N* ser como una ventana, este tipo de protocolos se conocen como **Sliding Window**.
- Si se pierde un paquete, entonces se reenvían todos los paquetes que se habían enviado desde el paquete que se perdió.
- De parte del transmisor, si recibe un paquete bien (sequence number es n siendo el último n - 1), devuelve un ACK. Sino, lo descarta y manda un ACK para n - 1.

![[GBN.png]]

## Selective Repeat (SR)

- Se intenta evitar las retransmisiones excesivas de GBN, retransmitiendo únicamente los paquetes que se sospecha fueron transmitidos mal.
- Cuando el emisor recibe un paquete fuera de orden, en vez de descartarlo como en GBN, lo pone en un buffer y espera a que le llegue el siguiente mensaje.
- Otra vez habrá una ventana *N*, sin embargo esta vez algunos de los paquetes ya estarán confirmados.

![[SR window.png]]

![[SR.png]]