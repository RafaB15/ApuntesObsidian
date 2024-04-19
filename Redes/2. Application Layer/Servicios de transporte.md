- Al desarrollar una aplicación en al [[Application Layer|capa de aplicación]], se debe elegir uno de los protocolos de la [[Transport Layer|capa de transporte]] disponibles.
- Cada protocolo disponible en la capa de transporte nos provee de diferentes servicios

## Transferencia confiable de datos

- Un protocolo provee esto si se asegura que los datos enviados desde un lado de la aplicación serán entregados correcta y completamente al otro lado de la aplicación.
- Si se provee el servicio de transferencia de datos confiables proceso-a-proceso, significa que un [[Redes/2. Application Layer/Proceso|proceso]] puede mandar sus datos por el [[Socket|socket]] sabiendo con certeza que estos llegarán sin errores al destinatario.
- Si no se provee este servicio, algunos paquetes que se envían se podrían perder, lo cual solo sirve para **loss-tolerant applications**.

## Rendimiento

- [[Red#Rendimiento en redes|Throughput]]
- Es el ratio con el que el proceso que envía datos puede entregar bits al proceso que los recibe.
- Un protocolo puede proveer como servicio **rendimiento disponible garantizado a un ratio específico**.
- Se garantiza una cota inferior de $r\frac{bits}{seg}$.
- Las aplicaciones que necesitan un rendimiento específico se suelen conocer como **bandwith-sensitive applications**.
- Las aplicaciones que no necesitan un rendimiento específico se conocen como **elastic applications**.

## Timing

- Un protocolo de transporte también puede ofrecer garantías de tiempo.
- Estas garantías son de la forma "Cada bit que se manda por el socket, llega a su destino en no más de 100 mseg".

## Seguridad

- Un protocolo de transporte puede proveer a una aplicación con servicios de seguridad.
- Se puede encriptar todos los datos enviados por el proceso emisor y desencriptar en el proceso destinatario.
- También se puede proveer integridad de los datos o autentificación en el end-point.

![[Requerimientos de diferentes servicios.png]]
