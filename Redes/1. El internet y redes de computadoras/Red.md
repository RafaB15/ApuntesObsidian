- Network
- Una red vendría a ser un conjunto de [[End System|end systems]] conectados a través de [[Communication Links|links de comunicación]] transmitiéndose información a través de [[Protocolo|protocolos]].
- El internet es una red de muchos [[End System|end systems]].
- Al borde de la red de encuentran los [[End System|end systems]], que envía y reciben información.
- Las redes se implementan siguiendo la [[Protocolo de Capas|arquitectura de capas]].

# Red de acceso

- Se refiere a la red que conecta físicamente un [[End System|end system]] con el primer [[Packet Switches|router]] (también conocido como *edge router*) en una [[Ruta|ruta]] desde el end system a alguno remoto. 

![[Ruta.png]]
- En la casas, las dos redes de acceso más prevalentes son el **cable** y **Digital Subscriber Line (DSL)**. 
- Normalmente se puede conseguir DSL por el mismo servicio que te da telefonía, con lo que el *telco* pasa a ser también to *ISP* (internet service provider).
- La línea telefónica residencial lleva entonces datos y señales telefónicas tradicionales simultaneamente, las cuales se encodean en frecuencias diferentes para no confundirlas.
- Esto hace que un único DSL link actúe como 3 links por separado, con lo que una llamada telefónica y la conexión a internet pueden compartir el DSL link al mismo tiempo.
![[DSL internet access.png]]

- Por otra parte, también se puede obtener acceso a internet a través de **cable**, con lo que pasamos a usar la infraestructura de televisión por cable de la compañía de televisión por cable para obtener acceso a internet.
- Se requieren modem especiales llamados **cable modems**. Para DSL se requieren **DSL modems**.

![[Internet por cable.png]]

- Hoy en día, en las casas, campuses y compañías se usa una **local area network (LAN)** para conectarse al [[End System|end system]] al final del router. Esto se suele hacer con **ethernet**.

![[Ethernet internet access.png]]

- Normalmente nos conectamos sin cables en una **Wireless LAN Setting** mandando y recibiendo [[Paquete|paquetes]] desde un punto de acceso que está conectado a la red que está conectada al [[Internet|internet]].
- Wireless LAN access based on IEEE 802.11 technology $\to$ WiFi 

![[Home network.png]]

- Los celulares se conectan a redes 3G y 4G, que usan el mismo servicio de telefonía para transmitir [[Paquete|paquetes]].

# Núcleo de Red

- Network core.
- Dentro de la red los [[End System|end systems]] intercambian mensajes. 
- Para mandar los mensajes, la fuente parte el mensaje en [[Paquete|paquetes]]. Cada paquete va a viajar por [[Communication Links]] y [[Packet Switches]] hasta llegar al destino en lo que se conoce como [[Ruta|ruta]].
- Otra forma de redirigir paquetes se da con el [[Circuit Switches]]

# Red de redes

- Para conectarse a internet, un end system se conecta a un access ISP (internet service provider). Pero los ISP a su vez deben estar conectados, lo cual se logra creando un **red de redes**.
- Los ISPs también deben ser capaces de conectarse entre ellos, con lo cual se conectan a ISPs de mayor nivel que tiene como objetivo conectar ISPs. Hay varios de estos, con lo que a su vez estos se conectan a ISPs de niveles aún mayores, hasta que las más grandes se conectan entre ellas sin costo adicional.

![[ISPs network.png]]

# Rendimiento en redes

- **Throughput**
- Si nosotros queremos mandar un archivo de host ([[End System|end system]]) A a host B, el **rendimiento instantáneo** vendría a ser el ratio ($\frac{bits}{seg}$) al que el host B está recibiendo el archivo.
- Si el archivo tiene *F* bits, y le toma *T* segundos al host B recibir todos los bits, entonces el **rendimiento promedio** vendría a ser $\frac{F}{T}\frac{bits}{seg}$.
- En una red, el ratio de transmisión que se elegirá para la ecuación de rendimiento será el menor de los involucrados, actuando como cuello de botella.