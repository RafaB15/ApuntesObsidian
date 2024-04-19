- Es un mecanismo para controlar una cantidad descontrolada de datos fluyendo por las red.
- Es implementado por [[Transmission Control Protocol|TCP]].
- Es una de las causas por las que se pierden [[Paquete|paquetes]], pues el [[Socket|socket]] que los recibe (si es TCP e implementa [[Transmisión confiable de datos|transmisión confiable de datos]]), va a tener en un buffer mensajes que todavía no pudo procesar, y si estos llegan demasiado rápido los tendrá que empezar a descartar. 
- Largos atrasos por cola se experimentan a medida que el ratio de arribo de paquetes se aproxima a la capacidad del medio (link capacity).
- **Offered load:** Se refiere a los bytes/sec transmitidos ($\lambda_{in}$) incluyendo los bytes referidos a retransmisiones de paquetes.

# Tipos

En el nivel más alto podemos distinguir entre métodos de control de congestion en donde la [[Network Layer|capa de red]] provee ayuda a la [[Transport Layer|capa de transporte]] para el control de congestión.

## Control de congestión End-to-end

- La capa de red no provee ninguna ayuda explícita a la capa de transporte para el control de la congestión.
- Incluso la presencia de congestión en la red debe ser **inferida** basándose en la cantidad de paquetes perdidos y el delay.
- [[Transmission Control Protocol|TCP]] lo implementa.

## Control de congestión asistido por red

- Los [[Packet Switches|routers]] proveen feedback explícito al sender o receiver acerca del estado de congestión de la red.
- Este feedback puede incluso ser un solo bit que implique congestión.
- Un router también podría informar acerca de el máximo host sending rate que puede soportar en un outgoing link.