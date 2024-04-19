- Es una arquitectura usada en la [[Application Layer|capa de aplicación]].
- **Servidor:** [[End System|Host]] que está prendido constantemente.
- **Cliente:** [[End System|Host]] que hace requests al servidor.
- En esta arquitectura los clientes no se comunican directamente entre ellos.
- El servidor tiene una **dirección IP** fija y conocida.
- Como el servidor siempre está encendido y su dirección IP es conocida y no cambia, un cliente siempre se puede contactar con el servidor enviándole [[Paquete|paquetes]] a su dirección IP.
- Muchas veces se usan data centers para, usando un gran número de hosts, crear un **servidor virtual**, que por debajo sean muchos servidores, de manera de poder responder más requests sin sobrecargarse.

![[Arquitectura cliente-servidor.png]]