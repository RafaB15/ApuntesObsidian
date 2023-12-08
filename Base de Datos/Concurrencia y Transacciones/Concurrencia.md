- Es la posibilidad de ejecutar múltiples [[Transacción|transacciones]] o tareas en forma simultánea.

- **Sistemas monoprocesador**
	- Permiten hacer multitasking, en donde varios hilos o procesos pueden estar corriendo simultáneamente.
- **Sistemas multiprocesador y sistemas distribuidos**
	- Disponen de varias unidades de procesamiento que funcionan en forma simultánea.
	- Suelen replicar la base de datos, disponiendo de varias copias de algunas tablas (o fragmentos) en distintas unidades de procesamiento.

- En sistemas multiprocesador o distribuidos vamos a querer aprovechar toda la capacidad de cómputo
	- Si dos [[Transacción|transacciones]] utilizan sets de datos distintos deberían poder ejecutarse concurrentemente en distintos procesadores.
- En sistemas monoprocesador, serializar no es una opción
	- No es deseable que la ejecución de una transacción lenta demore a otras de ejecución rápida. 
	- Mientras una transacción espera que el SO escriba una página en disco, otra transacción podría realizar una operación en memoria.

# Modelo de procesamiento concurrente

- El modelo de procesamiento que usaremos será el de **Concurrencia Solapada (interleaved concurrency)**, que considera las siguientes hipótesis
	1. Disponemos de un único procesador que puede ejecutar múltiples [[Transacción|transacciones]] simultáneamente.
	2. Cada transacción está formada por una secuencia de instrucciones atómicas, que el procesador ejecuta de a una a la vez.
	3. En cualquier momento el scheduler puede suspender la ejecución de una transacción, e iniciar o retomar la ejecución de otra.
- Ver [[Solapamiento]].

![[Concurrencia solapada.png]]

# Modelo de datos

- Consideraremos que nuestra base de datos está formada por ítems. 
- Un ítem puede representar: 
	- El valor de un atributo en una fila determinada de una tabla. 
	- Una fila de una tabla. 
	- Un bloque del disco. 
	- Una tabla. 
- Las instrucciones atómicas básicas de una transacción sobre la base de datos serán: 
	- `leer_item(X)`: Lee el valor del ítem X, cargándolo en una variable en memoria 
	- `escribir_item(X)`: Ordena escribir el valor que está en memoria del ítem X en la base de datos 
- Nota: El tamaño de ítem escogido se conoce como granularidad, y afecta sustancialmente al control de concurrencia

# Anomalías

- Al ejecutarse transacciones en forma concurrente se da lugar a distintas situaciones anómalas que pueden violar las [[Transacción#Propiedades ACID|propiedades ACID]].

## Lectura Sucia

- Dirty Read
- Se presenta cuando una transacción $T_2$ lee un ítem que ha sido modificado por otra transacción $T_1$.
- Si luego $T_1$ se deshace, la lectura que hizo $T_2$ no es válida en el sentido de que la ejecución resultante puede no ser equivalente a una ejecución serial de las transacciones.
- Es un conflicto de tipo WR: $W_{T_1}(X) \dots R_{T_2}(X) \dots (a_{T_1} \ ó \ c_{T_1})$ . (a de abort y c de commit).

![[Ejemplo lectura sucia.png]]
## Actualización Perdida

- Lost update
- Ocurre cuando una transacción modifica un ítem que fue leído anteriormente por una primera transacción que aún no terminó.
- En este caso, si la primera transacción luego modifica y escribe el ítem que leyó, el valor escrito por la segunda se perderá. 
- Si en cambio la primera transacción volviera a leer el ítem luego de que la segunda lo escribiera, se encontraría con un valor distinto. En este caso se lo conoce como lectura no repetible (unrepeatable read). 
- Ambas situaciones presentan un conflicto de tipo RW (read-write), seguido por otro de tipo WW ó WR, respectivamente.
- Caracterización: $R_{T_1}(X) \dots W_{T_2}(X) \dots (a_{T_1} \ ó \ c_{T_1})$

![[Ejemplo actualización perdida.png]]

## Escritura Sucia

- Dirty read.
- Ocurre cuando una transacción $T_2$ escribe un ítem que ya había sido escrito por otra transacción $T_1$ que luego se deshace.
- El problema se dará si los mecanismos de recuperación vuelven al ítem a su valor inicial, deshaciendo la modificación realizada por $T_2$.
- Es un conflicto de tipo WW: $W_{T_1}(X) \dots W_{T_2}(X) \dots (a_{T_1} \ ó \ c_{T_1}).$

![[Ejemplo escritura sucia.png]]

## Fantasma

- Phantom.
- Se produce cuando una transacción $T_1$ observa un conjunto de ítems que cumplen determinada condición, y luego dicho conjunto cambia porque algunos de sus items son modificados/creados/eliminados por otra transacción $T_2$. 
- Si está modificación se hace mientras $T_1$ aún se está ejecutando, $T_1$ podría encontrarse con que el conjunto de ítems que cumplen la condición cambió. 
- Esta anomalía atenta contra la serializabilidad. 
- Caracterización: $R_{T_1}(\{X_{cond}\}) \dots W_{T_2}(X_{cond}) \dots (a_{T_1} \ ó \ c_{T_1})$, en donde el ítem $X_{cond}$ cumple con la condición con que fueron seleccionado los *X* en la lectura.

![[Ejemplo fantasma.png]]

