- Conocido en español como conmutación de paquetes.
- Estos toman un [[Paquete|paquete]] que les llega por uno de sus incoming [[Communication Links|communication links]] recibidores y lo redirecciona por alguno de sus outgoing communication links.
- Los dos tipos más comunes de packet switches hoy en día son los **routers** y link-layer switches.
- La mayoría de los packet switches utilizan la transmisión **store-and-forward**, lo cual significa que tienen que recibir el [[Paquete|paquete]] entero antes de poder empezar a transmitir el primer bit del paquete al outgoing communication link.

![[Store and forward.png]]

- Los packet switches tienen muchos links conectados, y cada uno tiene un **output buffer** (también llamado **output queue**) que guardan paquetes que el switch está listo para mandar por ese link. Los paquetes que se necesitan mandar por un link en específico debe esperar en la cola. Esto genera **buffer queuing delays** 
- Si el buffer está lleno entonces al llegar el paquete sucede el **packet loss**, siendo droppeado o el paquete o algún paquete en el buffer.
- Los [[End System|end systems]] al mandar un [[Paquete|paquete]] ponen la dirección IP del destinatario en el header. Cuando a un packet switch le llega uno, este examina una parte de la dirección de destino y redirecciona el paquete a un router adyacente.
- Cada router tiene una **forwarding table** que mapea direcciones de destino (o porciones de estas) a los links de salida para saber a cual mandarlo.
- El internet tiene un número de protocolos de routing que se usan para automáticamente setear las forwarding tables.

# Retrasos

- Cuando un [[Paquete|paquete]] pasa por toda una red de packet switches, suelen haber retrasos ocasionados por diferentes razones.

## Retraso de procesamiento

- **Processing delay**.
- El tiempo que le toma al router examinar el header del [[Paquete|paquete]] y determinar a qué outgoing link redirigirlo.
- También puede incluir chequear errores al nivel de bits recibidos (checksum).
- Sueles ser microsegundos o menos, por lo que es despreciable.

## Retraso de fila

- **Queuing delay**.
- Una vez que se manda el paquete a ser redireccionado a algún link, este es puesto en una fila en donde tiene que esperar a que se libere el link para ser enviado.
- El tiempo que se espere dependerá de la cantidad de paquetes que llegaron antes y que también tienen que ser transmitidos por este link en específico.
- A diferencia del resto de tipos de retraso, el retraso de fila puede varias dependiendo del paquete, pues te puede tocar esperar mucho o poco.
- Siendo $a\frac{paq}{seg}$ el ratio promedio en el que los paquetes llegan, $R\frac{bits}{seg}$ el ratio de transmisión y suponemos que todos los paquetes consisten de $L\ bits$, entonces se conoce como **intensidad de tráfico** a $$\frac{L\cdot a}{R}$$
- Si la **intensidad de tráfico** es mayor a 1, entonces la fila tiende a crecer sin detenerse porque llegan más bits de los que se pueden transmitir.
![[Average queuing delay.png]]
## Retraso de transmisión

- **Transmission delay**.
- Nuestro paquete podrá ser transmitido solo cuando se hayan transmitido todos los paquetes que estaban en la fila.
- Denotamos la longitud del [[Paquete|paquete]] como *L* bits y el ratio de transmisión del [[Communication Links|link actual]] como *R* $\frac{bits}{seg}$.
- El retraso de transmisión será entonces $\frac{L}{R}$
- Este es el tiempo requerido para mover todos los bits del paquete al link.

## Retraso de propagación

- **Propagation delay**.
- Una vez que los bits están en el link estos tienen que llegar hasta el siguiente router.
- El tiempo que toma esto es el retraso de propagación.
- El bit viaja a la velocidad de propagación del link, que normalmente depende del medio físico del que esté hecho.
- Suele ser similar a la velocidad de la luz.
- Es la distancia entre los dos routers dividido por la velocidad de propagación ($\frac{d}{s}$).

## Retraso nodal total

- Es el retraso total y se consigue sumando los 4 tipos de retraso anteriores. 
- $d_{nodal} = d_{proc} + d_{queue} + d_{trans} + d_{prop}$

# Pérdida de paquetes

- **Packet loss**.
- A medida que los [[Paquete|paquetes]] van llegando al router y se tienen que re dirigir a un outgoing [[Communication Links|link]], se lo pone en la fila para se transmitido. 
- Las filas no son infinitas, y si la fila está llena, con ningún lugar para poder guardar el paquete, este se tiene que eliminar (drop) o se elimina uno de los paquetes en la fila.

# Retraso end-to-end

- Se refiere al retraso, no solo tomando en cuenta un solo router, sino todos los routers en la ruta.
- Siendo N el número de routers y asumiendo que no va a haber queuing delays, la fórmula nos quedaría $$dend-end = N(d_{proc} + d_{trans} + d_{prop})$$