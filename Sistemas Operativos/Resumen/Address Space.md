Es una abstracción de la memoria física, siendo memoria virtual. El espacio de memoria es la manera en la que un [[Sistemas Operativos/Resumen/Proceso|proceso]] ve la memoria en el sistema.

Este espacio contiene toda la información del estado de la memoria del proceso

- El código: Las instrucciones del programa, como tienen que vivir en memoria a la hora de ser ejecutadas, se almacenan aquí. Es estático.
- El [[Sistemas Operativos/Resumen/Stack|stack]]
- El [[Sistemas Operativos/Resumen/Heap|heap]]
![[Sistemas Operativos/Resumen/images/Pasted image 20230929151126.png]]

Estas direcciones de memoria son *virtuales*, pues en la dirección 0 en realidad no encontraremos el código del programa, sino que habrá algo más. Pero para nuestro programa, es aquí donde se almacena el código y al intentar acceder, se traducirá la memoria virtual a memoria física y nos dirigiremos al lugar correcto.

Esto se logra gracias a la [[Sistemas Operativos/Resumen/Virtualización de Memoria|Virtualización de Memoria]]. 