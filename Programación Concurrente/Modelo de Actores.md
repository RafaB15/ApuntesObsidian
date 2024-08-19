Similar al modelo de [[Pasaje de mensajes]].
# Actor

- Es una clase
- El actor es la primitiva principal del modelo. 
- Son livianos, se pueden crear miles (en lugar de threads). 
- Encapsulan comportamiento (métodos) y estado interno (memoria propia). 
- Compuesto por:
	- **Dirección**: adonde enviarle mensajes. 
	- **Casilla de correo (mailbox)**: un FIFO de los últimos mensajes recibidos. 
- El actor **supervisor** puede crear otros actores hijo.
	- En Rust también crea el contexto y lo destruye para que todo ande.

![[Pasted image 20240520114653.png]]

- Son aislados de otros actores: no comparten memoria. Esto protege la memoria.
- El estado privado solo puede cambiarse a partir de procesar mensajes.
- Pueden manejar un mensaje por vez.
- En un sistema distribuido, la dirección del actor puede ser una dirección remota.

# Mensajes

- Los actores se comunican entre ellos solamente usando mensajes.
- Los mensajes son procesados por los actores de forma asincrónica. 
- Los mensajes son estructuras simples inmutables
- El procesamiento de mensajes es secuencial

# Actores en Rust

## Framework Actix

- Usa **tokio** y futures como runtime de sustento. Se ejecutan dentro del Sistema de Actores.
- El núcleo es el tipo *Arbitrer*, un thread que crea un event loop por debajo y provee un handler.
- No se puede hacer await en el handler.
- Cada actor se ejecuta dentro de un arbitrer.
- El handler se usa para enviar mensajes al actor.
- Se ejecutan en un contexto de ejecución *Context\<A>*, separado para cada uno.  

## Crear un actor

- Crear un tipo de dato. Debe implementar el trait **Actor**.
- Definir un mensaje e implementar el handler para ese tipo del actor: **Handler\<M>**. Los mensajes pueden ser manejados de forma asincrónica.
- Crear el actor y hacer spawn en uno de los árbitros.

## Ciclo de vida

- **Iniciado (Started)**: con el método started() (implementación default en el trait Actor). El contexto del actor está disponible. No lo implementamos porque ya está implementado por default.
- **En ejecución (Running)**: es el estado siguiente a la ejecución de started(). Puede estar en este estado de forma indefinida. Procesando mensajes.
- **Parando (Stopping)**: puede pasar a este este estado en las siguiente situaciones: 
	- Llamando Context::stop en el mismo actor. 
	- ningún otro actor lo referencia
	- no hay objetos registrados en el contexto 
- **Detenido (Stopped):** desde el estado anterior no modificó su situación. Es el último estado de ejecución.

## Dirección

- Los actores son referenciados únicamente por la **dirección**. 
```Rust
struct MyActor;
impl Actor for MyActor { 
	type Context = Context<Self>; 
} 
let addr = MyActor.start();
```

## Mensaje

Un actor se comunica con otro enviando mensajes. Todos los mensajes son tipados, deben implementar el trait *Message*.

```Rust
impl Message for Ping { 
	type Result = Result<bool, std::io::Error>; 
}
```

## Enviar mensaje

- Varias formas: 
	- **Addr::do_send(M)**: ignora errores en el envío del mensaje. Si la casilla de mensajes está cerrada, se descarta. No retorna el resultado. 
	- **Addr::try_send(M)**: trata de enviar el mensaje inmediatamente. Si la casilla de mensajes está llena o cerrada, retorna *SendError* 
	- **Addr::send(M)**: retorna un objeto future que resultado del proceso de manejo del mensaje.

## Contexto

- Los actores mantienen el contexto interno de ejecución, o estado. 
- Permite al actor determinar su dirección, cambiar los límites de la casilla de mensajes, o detenerse. 
- Los mensajes llegan a la casilla primero, luego el contexto de ejecución llama al handler específico.

## Arbiter

- Provee el contexto de ejecución asincrónica para los actores, funciones y futures. 
- Alojan el entorno donde se ejecuta el actor. 
- Realizan varias tareas: 
	- crear un nuevo Thread del SO
	- ejecutar un event loop
	- crear tareas asincrónicas en ese event loop.


# Práctica Channels y Actores

## Problema del banquero con mensajes

Usamos senders y receivers para que los threads se manden la plata y luego hagan receive bloqueante.

## Actores

- Con channels, el único objetivo en la vida del thread es esperar por mensajes y hacer algo.
- Actores es como un modelo mental, entidad que solo espera por mesajes entrantes y los procesa en orden. Tendrá su propio línea de ejecución permanente. Tenemos que tener una forma de dirigirme hacia ellos.
- Usamos actix y actix_rt
- Definimos un actor definiendo una estructura y definiendo que va a implementar el trait actor. Tendremos que establecer el tipo de **contexto**.
- Un actor se define por el código con el que procesa los diferentes tipos de mensajes que recibe.
- Se hafce implementando el trait Handle
- Lo que usemos como mensaje tiene que implementar el tipo
- Si usamos las macros #[derive(Message)] #[rtype(result="String")]
- Es un sistema de mensajes asincrónicos.
- Te ayuda a evitar el estado mutable compartido.
- Con do_send mandamos el mensaje pero no nos importa si llegó o no.
- Try send devuelve un resutl para saber si llegó
- Send se va a quedar esperando hasta que se libere el actor y pueda recibir el mensaje. Se le pone punto await.
- Los actores corren en un solo thread. Los executors son sobre el thread principal.
- Si metemos un sleep dentro de un message handler que hace multiplexación de tasks, entonces estamos deteniendo todo el actor system.
- Las cosas con sistema operativo y bloqueo lo podemos cambiar por su versión asincrónica.
- Podemos cambiar el context a uno sync para que lo bloqueante sea bloqueante.
- Tenemos que correr el actor con un sync arbiter. Esto lo pondrá a correr en un ambiente dedicado.
- Podemos cambiar la cantidad de instancia indintiguibles entre si. Es como tener un load balancer si se quiere, no sabés cual repsonde tu duda.