- Crear un nuevo thread involucra reservar memoria para este, lo cual puede demandar mucha memoria al tener muchos.
- Se puede usar **Tareas asincrónicas de Rust** para intercalar tareas en un único thread o en un pool de threads. 
- Son mucho más livianas que los threads. 
- Más rápidas de crear, más eficiente de pasarle el control a ellas. 
- Menor overhead de memoria. 
- Se puede tener miles o decenas de miles en un programa. 
- El código asincrónico luce como el de threads, salvo que las operaciones que bloquean, se manejan diferente.
- El scheduler no administra a los **tasks**, sino que se ejecutan en el mismo thread o en una threadpool ya existente.
- Esto logra que se administren mejor los recursos, pues si hay alguna tarea bloqueante el mismo thread en vez de quedarse esperando puede cambiar el contexto y ejecutar algo más.
- Si tenemos un programa que se conecta a un servidor y escribe algo en este, la mayor parte del tiempo el thread está bloqueado.
![[Thread bloqueado async.png]]
- Para evitar esto, un thread debe poder tomar otras tareas mientras espera que la system call se complete.

# Trait Future

- std::future::Future

```rust
trait Future { 
	type Output; 
	// por ahora, interpretar ‘Pin<&mut Self>‘ 
	// como ‘&mut Self‘. 
	fn poll(self: Pin<&mut Self>, cx: &mut Context<’_>) -> Poll; 
	} 
	
enum Poll { 
	Ready(T), 
	Pending, 
}
```

- El poll es ejecutado por el ejecutador, no por nosotros a mano.
- Representa una operación sobre la que se puede testear si se completó. 
- El método *poll* **nunca** bloquea. 
- Si la operación se completó, retorna: *Poll::Ready(output)* (output es el resultado final de la operación). 
- Si no se completó, retorna Pending. 
- Modelo **piñata** de la programación asincrónica: lo único que se puede hacer con un future es golpearlo con poll hasta que caiga el valor. 
- SO proveen system calls como interfaz para hacer poll.
- Las funciones asincrónicas entonces en vez de devolver un valor simple, devuelven un valor que implementa este trait.
- Cada vez que es polleado, avanza todo lo que puede. 
- El Future almacena lo necesario para realizar el pedido hecho por la invocación. 
- Crate async-std: Provee versiones async de las facilidades de I/O de la std (incluyendo un trait Read asincrónico).
- La arquitectura async de Rust está diseñada para ser eficiente. 
- Se llama a poll solamente cuando vale la pena (algo debe retornar Ready, o progresar al objetivo).
- Cuando ponemos la palabra **async** antes de una función, se envuelve el resultado de esta en algo que implemente el trait Future.
- Cada vez que tenemos que usar una función asincrónica tenemos que poner .await? al final.

# Funciones async y expresiones await

- Invocar una función async retorna inmediatamente, antes de que comience a ejecutarse el cuerpo de la función. 
- Se obtiene un Future del valor, que contiene todo lo necesario para que la función pueda ejecutarse (argumentos, espacio para variables locales, etc).
- El tipo específico es generado al momento de compilar. 
- Al ejecutar poll por primera vez sobre el retorno, se ejecuta el cuerpo de la función hasta el primer await. 
- Si no se completó, retorna Pending y toda la función devuelve ese valor/estado. 
- La expresión await toma ownership del future y hace el poll.
- Si está Ready, el valor final del future es el valor devuelto en la expresión await, y continúa. 
- Caso contrario, retorna Pending a su función que lo invocó.
- La siguiente invocación a poll sobre la función cheapo_request, continuará desde el punto donde estaba el future connect. 
- El Future alacena el punto donde debe retomarse en el siguiente poll y el estado local. 
- Las expresiones await tienen la capacidad de continuar, se pueden usar solamente en funciones sync.
- Join te corre concurrentemente dos procesos async
- Join_All te convierte un iterador de futures en un future iterable.
# block on
- block_on es una función sincrónica que produce el valor final de la función asincrónica.
- Es un adaptador del mundo asincrónico al sincrónico. 
- No debe usarse en una función async (bloquea a todo el thread). 
- block_on conoce cuánto hacer sleep hasta hacer poll de nuevo.
# Crear tareas async

- **async_std::task::spawn_local** recibe un future y lo agrega a un pool que realizará polling en el block_on (soportado solamente en unstable del crate). Es análogo a spawn de thread. 
- Los lifetimes de las variables deben ser static, porque debe poder ejecutarse hasta el final del programa. 
- Todas las ejecuciones pueden realizarse en un único thread. 
- Una llamada asincrónica ofrece la apariencia de una única llamada a función que se ejecuta hasta que se completa. Pero es realizada por una serie de llamadas sincrónicas al método poll, que retorna rápidamente, hasta que se completa.
- El cambio de una tarea a otra ocurre solamente en las expresiones **await** → un cómputo grande en una función no daría lugar a la ejecución de otras tareas (diferencia con threads). 
- Existe async_std::task::spawn: crea la tarea y la coloca en el pool de threads dedicado a hacer poll de los futures. 
- No necesita ejecutar block_on para que sea polleada.

# Cómputos de larga ejecución

- *async_std::task::yield_now* favorece el paralelismo. Retorna un future para pasar el control a otra tarea. 
- Se usa: async_std::task::yield_now().await; 
- La primera vez que se hace poll, retorna Pending, la siguiente vez retorna Ready(()). 
- async_std::task::spawn_blocking: coloca la tarea en otro thread del SO (para realizar un cómputo pesado), dedicado a tareas bloqueantes.

# Cuando usar código Async en Rust
- Las tareas asincrónicas usan menos memoria. Los threads de Linux pueden usar desde 20 kb de memoria. 
- Las tareas asincrónicas se crean más rápido. En Linux, threads 15µs, tareas 300 ns. 
- Los cambios de contexto son más rápidos con tareas asincrónicas que con threads.

- En conclusión, usamos async para
	- Consultar servicio externos
	- Leer de un archivo
	- Servir requests HTTP
- No se usa para
	- Calcular un factorial
	- Calcular un producto de matrices
	- Implementar el problema de los filósofos
	- Estado interno compartido


- No usar locks en programación asincrónica