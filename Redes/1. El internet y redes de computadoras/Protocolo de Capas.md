# Arquitectura de capas

- Se divide el protocolo para que funcionen sistemas complejos como el [[Internet]] en diferentes capas.
- Una capa puede utilizar **servicios** de la capa de abajo y provee servicios a la capa de arriba.
- Una arquitectura de capas nos permite discutir una parte específica y bien definida de un sistema largo y complejo. 
- Esta simplificación tiene mucho valor, pues nos provee modularidad, lo que hace mucho más fácil cambiar la implementación de un servicio proveído por una capa.
- Mientras la capa provea el mismo servicio a la capa de arriba y utilice los mismos servicios de la capa de abajo.

![[Horizontal layering of airline functionality.png]]

# Protocolo de Capas

- Los diseñadores de [[Red|redes]] organizan protocolos, y el hardware y software que los implementa, en **capas**.
- Cada protocolo le pertenece a una de las capas.
- Cada capa en un **modelo de servicio** va a 
	- Realizar acciones adentro de la capa
	- Usar los servicios de la capa directamente abajo.
- Un protocolo de capa puede ser implementados en software, hardware o en una combinación de ambos.
- Cuando se los toma juntos, los protocolos de las distintas capas se conocen como **protocol stack**. 
- El protocol stack del [[Internet]] consiste de cinco capas:
	- [[Application Layer]]: Es donde residen las aplicaciones de red y sus protocolos de la capa de aplicación (HTTP, SMTP, FTP).
	- [[Transport Layer]]: Transporta mensajes de la capa de aplicación entre endpoints de las aplicaciones.
	- [[Network Layer]]: Es responsable de mover paquetes de la capa de red conocidos como *datagrams* de un host a otro.
	- [[Link Layer]]: Provee servicios para mover un paquete de un nodo (host o router) a otro.
	- [[Physical Layer]]: Se encarga de mover los bits individuales en un frame de un nodo al siguiente.

![[Protocolos en capas.png]]

- Un paquete que viaja a través de las capas normalmente tiene dos campos, los heders y el payload. El payload normalmente es un paquete en la capa de arriba, y al bajar se le agregaron headers.
- Al principio se había desarrollado el modelo OSI, que tenía dos capas adicionales.