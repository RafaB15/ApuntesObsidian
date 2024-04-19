- Es un tipo de [[Packet Switches|packet switch]].
- A diferencia de los link layer switches, los routers basan su decisión de redireccionamiento (forwarding) en la información en los headers de los datagramas de red que obtienen.
- Son aparatos de la [[Network Layer|capa de red]].
- **Redireccionar:** Cuando un paquete llega al input link de un router, el router lo tiene que mover al output link apropiado.
- **Rutear**: La capa de red debe determinar la ruta o camino tomado por los paquetes mientras estos fluyen de un emisor a un receptor.
# Forwarding table

- Un router **redirecciona** un [[Paquete|paquete]] examinando su header  y usando algunos valores de este para indexar la tabla.
- El resultado indicará el outgoing link al que se debe redirigir el paquete.
- Estas pueden tener como entradas los primeros bits de las direcciones a las que tienen que llevar a los paquetes, entonces matchean con esas.

![[Routing algorithms.png]]

![[SDN.png]]

# Interior del router

![[Interior de un router.png]]

## Puerto de input

- **Input port**.
- Se encarga de funciones de la capa física para pasar del link al router.
- También conf unciones de la capa física se encarga de comunicar al router con el router del otro lado.
- Aquí se decide el puerto de salida (output port) por el cual el paquete será redirigido, consultando a la forwarding table, para saber a donde se enviará el paquete a través de la Switching Fabric.
- Paquetes de control se redireccionan de un puerto de input a procesador de ruteo.
- Se leen los campos version number, checksum y time to live, rescribiendo los últimos dos.

![[Input port.png]]

## Switching Fabric

- Conecta a los puertos de input con los puertos de output de un router.
- Está contenida completamente adentro del router.
- La consulta a la forwarding table y la decisión de a donde irá el paquete se toma en el **input port**.

## Puertos de output

- **Output port**.
- Guarda los paquetes recibidos de la switching fabric, y transmite estos paquetes en el outgoing link, ejecutando las funciones de la capa de link y capa física necesarias.
- Si un link es bidireccional, se empareja a un output port con un input port en la misma line card para este link.
![[Output port.png]]
## Procesador de ruteo

- **Routing processor**
- Ejecuta funciones del plano de control de la [[Network Layer|capa de red]].
- En routers clásicos, ejecuta los protocolos de ruta, mantiene tablas de ruteo e información de links adjunta, y computa la **forwarding table** para el router.
- En los routers SDN, el procesador de ruteo es responsable de la comunicación con el controlador remoto para poder recibir las entradas en la forwarding table computadas por este, e instalar estas entradas en los input ports del router.
- Ejecuta las funciones de manejo de red.
- Normalmente es un CPU tradicional.


- Las funciones de estos componentes están casi siempre implementadas en hardware.
- **Destination-based forwarding**: En cada router se indica el destino final y se reenvía al router que mejor ayudará a llegar.
- **Generalized forwarding**: Depende de más factores que de solo el destino, como el origen, para redirigir.

# Colas

- En los input port y los output ports se formar colas de paquetes esperando a ser transmitidos por los links.
- Para los ejemplos tomaremos que:
	- $R_{line}$: Transmission rate de los input y output ports. Packets per second.
	- $N$: Cantidad de input ports y output ports (iguales para simplificar)
	- Todos los paquetes de igual longitud.
	- Los paquetes llegan al input port de forma sincrónica.
	- $R_{switch}$: Switch fabric transmission rate.

## Input Queueing

- Si llegan muchos paquetes y estos no se pueden pasar por la switch fabric lo suficientemente rápido, entonces se generan colas.
- Si tenemos un paquetes qeu va a un puerto pero este está ocupado, el paquete se retrasa, pero también retrasa al de atrás, el cual podría tener el puerto de output libre. Esto se conoce como Head Of The Line (HOL) blocking

![[HOL blocking.png]]

## Output Queueing

- Consideramos que $R_{switch} > N\cdot R_{line}$ y todos los paquetes que llegan a los *N* input ports van al mismo output port.
- En este caso el tiempo que lleva mandar un paquete al outgoing link, entran *N* nuevos paquetes al port. Estos tendrán que hacer fila.
- Eventualmente, el número de paquetes en la cola puede exceder la memoria que tiene el output port.

![[Output port queueing.png]]

# Packet Scheduling

## First In First Out

- Se envían los paquetes empezando por los que llegaron primero.
- Si llega otro paquete y no hay más espacio en el buffer, la política de descarte de paquetes decide si lo descarta o descarta algún paquete también en fila.

![[Fifo.png]]

![[Fifo queue.png]]
## Priority Queuing

- Los paquetes que llegan al output link se clasifican en clases de prioridad al llegar a la cola. 
- Los paquetes que tengan información de manejo de la red tienen prioridad sobre el tráfico común, también las cosas en tiempo real suelen recibir prioridad.
- El manejo de paquetes que tengan la misma prioridad se suele hacer en FIFO.
- Si la disciplina es non-preemptive, no se interrumpe el envío de un paquete cuando este ha comenzado.

![[Priority Queue.png]]

![[Priority queue en acción.png]]

## Round Robin y Weighted Fair Queuing

- Los paquetes se ordenan en clases como en la cola con prioridad.
- Sin embargo, en vez de tener una jerarquía de clases, round robin va alternando entre las clases.

![[Round robin.png]]

- Weighted Fair Queuing es como round robin, pero las clases pueden tener diferentes tiempos de servicio antes de pasar al siguiente.

![[WFQ.png]]