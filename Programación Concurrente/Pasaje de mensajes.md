# Modelos de Comunicación

- Comunicación entre entidades (procesos o computadores)
	- Sincrónica: Ambas partes están sincronizadas. Comunicación y respuesta. Llamada telefónica ponele
	- Asincrónica - Buffer: No hay una sincronicidad, pero nadie está esperando una respuesta. Se pone en un buffer. Es como el correo electrónico. Cada tanto vemos si tenemos una respuesta.
- Direccionamiento ¿Cómo se determina a quién dirigir un mensaje? 
	- Simétrico: Tenemos una comunicación de 1 a 1.
	- Asimétrico: No hay comunicación 1 a 1. Hay una multidfusión, un broadcast. Es como un mensaje en twitter. Publicás algo y te leen todos los que te siguen. 
	- Sin direccionamiento (matcheo por estructura del mensaje): El mensaje se recibe dependiendo de la estructura del mensaje. Una app que procesa solamente los mensajes que son de meteorología.
- Flujo de datos
	- Unidireccional: Un canal que conecta al emisor con el receptor. Logger.
	- Bidireccional: Se envían y reciben mensajes en ambos sentidos.

# Canales

- Conectan un proceso emisor con un proceso receptor 
- Tienen un nombre 
- Son tipados -> Son para leer tipos de datos.
- Sincrónicos o asincrónicos
- Unidireccionales

## Productores y Consumidores

![[Pasted image 20240519224825.png]]
Si el canal está lleno, entonces mandar se bloquea tal parece. No es común. Hay un problema.

# Selective Input

- Es una sintaxis permitida por los lenguajes que soportan canales.
- Permite escuchar en varios canales de forma bloqueante y desbloquearse con el primero que recibe un mensaje. (Rust no lo implementa)
- Esto ayuda con el busy wait, pues de otra forma tendrías que chequear continuamente si hay información en algún canal de forma no bloqueante continuamente.

## Filósofos Comensales

![[Pasted image 20240519230324.png]]
No nos interesa lo que se manda, solo que se manda algo.
Cada filósofo tiene una variables dummy.
Eat debería estar indentado.
Extrae dos palitos de los canales i e i + 1.

# Remote Procedure Calls

- Permiten al cliente ejecutar funciones en un servidor localizado en otro procesador.
	- Se requiere la implementación de stubs en ambos extremos
	- Los stubs conforman interfaces remotas utilizadas para compilar cliente y servidor
	- Localización de servicios
	- Parameter marshalling

# Canales en Unix
- Unix provee Pipes y FIFOs para conectar dos procesos independientes, orientado a bytes.
	- Los fifos poseen una representación en el file system. Podemos crear un fifo en unix y los veremos si hacemos ls en el directorio en el que está.
- Unix también provee colas de mensajes (Message Queues) orientados a mensajes como unidades independientes. No los podés leer a la mitad.

# Canales en Rust
- Do not communicate by sharing memory; instead share memory by communicating.
- Un canal tiene dos extremos: un emisor y un receptor.
- Una parte del código invoca métodos sobre el transmisor, con los datos que se quiere enviar.
- Otra parte chequea el extremo de recepción por la existencia de mensajes.
- Múltiples productores, un consumidor.
- Transfieren el ownership del elemento enviado.
- Para crear múltiples productores, se clona el extremo de envío.