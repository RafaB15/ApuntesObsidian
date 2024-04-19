- Es una arquitectura usada en la [[Application Layer|capa de aplicación]].
- No se depende (o se depende muy poco) de **servidores**.
- Las aplicaciones que implementan esta arquitectura hacen uso de la comunicación directa entre [[End System|hosts]] conectados momentáneamente, llamados **peers**.
- Los peers son normalmente computadoras de escritorio o laptops controlados por usuarios.
- Una característica muy importante de esta arquitectura es su **auto-escalabilidad**, pues mientras que al haber más hosts hay también más requests, la presencia de estos nuevos hosts significan que hay más capacidad de servicio en el sistema, pues también responden requests.
- No son caras, pues normalmente no requieren mucha infraestructura de servidores.
- Tienen problemas de seguridad, eficiencia y confianza por su estructura tan descentralizada.
- Si quisiéramos definir a los diferentes peers como cliente o servidor, el peer que está recibiendo información sería el cliente, mientras que el que la transmite es el servidor en un momento específico. El que un peer sea 

![[Arquitectura peer-to-peer.png]]