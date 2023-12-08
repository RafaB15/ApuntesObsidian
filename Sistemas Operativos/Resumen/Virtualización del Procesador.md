También conocida como la virtualización del procesamiento, consiste en dar la ilusión de la existencia de un único procesador para cualquier programa que requiera de su uso. De esta forma se provee:

- Simplicidad en la programación
	- Cada proceso cree que tiene toda la CPU.
	- Cada proceso cree que todos los dispositivos le pertenecen.
	- Distintos dispositivos parecen tener el mismo nivel de interfaces.
	- Las interfaces con los dispositivos son más potentes que el metal solo.
- Aislamiento frente a fallas
	- Los procesos no pueden directamente afectar a otros procesos.
	- Lo errores no colapsan toda la máquina.
El [[Sistemas Operativos/Resumen/Sistema Operativo|sistema operativo]] crea esta ilusión mediante la virtualización de la CPU a través del [[Sistemas Operativos/Resumen/Kernel|kernel]].

![[Sistemas Operativos/Resumen/images/Virtualización del procesador.png]]