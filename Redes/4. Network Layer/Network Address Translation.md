- **NAT**
- Es un sistema a través del cual, en una red privada, podemos hacer uso de la misma [[Dirección IP|dirección IP]] para muchos [[End System|end systems]] distintos.

![[NAT.png]]

- En una sub red privada que usa NAT las interfaces en la red tienen la dirección $10.0.0.0/24$, la cual está reservada para redes privadas. Estas direcciones solo tienen significado para aparatos dentro de nuestra misma red.
- En el exterior, ven al NAT-enabled [[Router|router]] como algo con una única dirección IP.
- NAT sabe a donde mandar la información que le llega  a través de la NAT translation table.
- Al la NAT recibir un [[Datagrama|datagrama]] a través de la LAN, le cambia la dirección IP privada por la suya, genera un nuevo puerto de fuente y lo reemplaza por el elegido por el host.
- Cuando nos llega un mensaje, la tabla se indexa con la dirección IP de destino y el puerto de destino para poder obtener el host al que verdaderamente le están enviando algo.
- Reescribe el datagrama entrante y lo redirige a la red local.