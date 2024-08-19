# Condition variable
- Una condición variable C
- Tiene asociado un FIFO
- Consta de tres operaciones atómicas
	- waitC(cond)
		- cond.append (p) 
		  p.state := blocked 
		  monitor.releaseLock ()
		  - El proceso espera por una condición, se queda bloqueado sin consumir uso del cpu, libera el lock del monitor de esa variable de condición.
	- signalC(cond)
		- if ( cond <> empty ) 
		  begin 
		  q := cond.remove () 
		  q.state := ready 
		  end
		  - Verifica si la condición no está vacía, saca al proceso de la fila y su estado de blocked, y termina.
	- empty(cond)
		- return cond = empty
		- Nos retorna si la condición está vacía.

# Monitores

- Herramientas de sincronización que permite a los hilos tener exclusión mutua y la posibilidad de esperar (block) por que una condición se vuelva falsa. 
- Tienen un mecanismo para señalizar otros hilos cuando su condición se cumple.
- Consta de:
	- Nombre 
	- Variables internas 
	- Procedimientos del monitor: rutinas que acceden directamente a las variables internas 
	- Una interfaz pública para que los procesos puedan acceder a las variables internas 
	- Inicialización de las variables internas 
	- Un conjunto de condition variables que incorporan **sincronismo** al monitor
- Los procesos pueden tomar distintos estados: 
	- Esperando para entrar al monitor 
	- Ejecutando el monitor (sólo un proceso a la vez - exclusión mutua) 
	- Bloqueado en FIFO de variable de condición 
	- Recién liberado de la wait condition I Recién completó una operación signalC.

![[Semáforo vs Monitor.png]]


- Cuando se usan los waits en rust se les pasa un mutexguard. Lo que pasa es que primero tenés que hacer lock y esperás hasta conseguir el elemento, luego se fija en la condición, si no da lo que queremos entonces liberamos el lock y esperamos a que nos despierten la condition variable con un notify_one o notify_all, al despertarnos volvemos a intentar tomar el lock y tenemos otro mutex guard nuevo.