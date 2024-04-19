- Es un identificador requerido por el [[Internet Protocol|protocolo IP]] para identificar a cualquier **interface** (presente en [[End System|end systems]] y [[Router|routers]]) que sea capaz de enviar y recibir [[Datagrama|datagramas IP]].
- Son únicas a nivel global y manejadas bajo al autoridad de la Internet Corporation of Assigned Names and Numbers (ICANN)
- Tiene una longitud de 32 bits.
- Se suelen escribir en **dotted-decimal notation**, con cada byte escrito en forma decimal y separado por un punto de los otros bytes.
- Se puede usar [[Network Address Translation|NAT]]
- Una porción de la dirección IP dependerá de la subnet a la que esté conectada.
 
![[Direcciones IP y subnets.png]]
- Vemos en la imagen que a la izquierda hay host que compartes los primers 24 bits de su dirección y están conectados por algo que no es un router. Estos hosts conectados a un router forman una **subnet** (también conocida como **IP network**). A la subnet se le da la dirección $223.1.1.0/24$ (conocida como subnet mask), pues la subnet tiene a las 3 direcciones de los host y a una dirección del router.

![[subnets.png]]

- Las subnets también se pueden interconectar por routers, pero habrá una subnet más interconectando los routers.

![[subnets interconactadas.png]]

> To determine the subnets, detach each interface from its host or router, creating islands of isolated networks, with interfaces terminating the end points of the isolated networks. Each of these isolated networks is called a subnet.

# Classless Interdomain Routing

- CIDR (se pronuncia cider).
- Generaliza la noción del addressing the subnets.
- Los *x* bits más significativos de una dirección de la forma $a.b.c.d/x$ se conocen como la **porción de red** de una dirección IP, y se refiere a estos como **prefijos**. Estos son los únicos que se toman en cuenta en la forwarding table de un [[Router|router]].
- Si un host envía un paquete que tiene como destino $255.255.255.255$ entonces quiere que se envíe a todos los hosts en la subnet.

# Dynamic Host Configuration Protocol

- Cuando nos conectamos a una red, se nos da una dirección IP automáticamente. 
- De esto en realidad se encarga un protocolo cliente servidor llamado **DHCP**.
![[DHCP.png]]

- Al entrar se inicia la fase de **DHCP server discovery** en la que se manda un DHCP discover message, mandando el mensaje a la dirección $255.255.255.255$ is el source IP address $0.0.0.0$ (this host).
- El DHCP server responde con un DHCP offer message.
- El cliente manda un DHCP request message al servidor al que se quiera conectar.
- El servidor responde con una DHCP ACK message.
![[DHCP protocol.png]]