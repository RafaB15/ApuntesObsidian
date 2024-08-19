# Corrección
- Cuando hablamos de corrección nos referimos a que un programa cumpla con su objetivo y lo realice correctamente.
- En procesos (programas secuenciales) es suficiente con debuggear para encontrar errores, ya que ante una misma entrada se obtiene siempre la misma salida. 
- En programas concurrentes, la salida puede depender del escenario que resultó en la ejecución.
- Esto significa que algunos bugs se pueden presentar en unos escenarios y no en otros.
- Definimos propiedades de corrección de los programas concurrentes:
	- Propiedades de tipo **safety**: Debe ser verdadera siempre.
	- Propiedades de tipo **Liveness**: debe volverse verdadera eventualmente

## Safety

- **Exclusión mutua:**
	- Dos procesos no deben intercalar ciertas (sub)secuecnias de instrucciones.
	- Ejemplo: incremento de variable global.
- **Ausencia de deadlock**: 
	- Un sistema que aún no finalizó debe poder continuar realizando su tarea, es decir, avanzar productivamente.

## Liveness

- **Ausencia de starvation:** 
	- Todo proceso que esté listo para utilizar un recurso debe recibir dicho recurso eventualmente.
- **Fairness:**
	- Equidad o justicia.
	- Un escenario es (débilmente) fair, si en algún estado en el escenario, una instrucción que está continuamente habilitada, eventualmente aparece en el escenario.
	- Puede que hayan muchos procesos ejecutándose, pero eventualmente se tendría que ejecutar un proceso que está habilitado.

# Sección Crítica
- **Pregunta de examen: Cómo se modeliza una sección crítica:**
- Cada proceso se ejecuta en un loop infinito cuyo código puede dividirse en una parte crítica y parte no-crítica.
- Especificaciones de corrección:
	- Exclusión mutua: no deben intercalarse instrucciones de la sección crítica.
	- Ausencia de deadlock: Si dos procesos están tratando de entrar a la sección crítica, eventualmente alguno de ellos debe tener éxito.
	- Ausencia de starvation: Si un proceso trata de entrar a la sección crítica, eventualmente debe tener éxito.
- La sección crítica debe progresar (finalizar eventualmente).
- La sección no crítica no requiere progreso (el proceso puede terminar o entrar en un loop infinito)

# Locks

- Sirven para realizar exclusión mutua entre procesos.
- Se implementan mediante variables de tipo *lock*, que contienen el estado del mismo.
- Se utilizan mediante los métodos  *lock()* y *unlock()*.
	- Método *lock()*: El proceso se bloquea (no consume un ciclo del cpu) hasta poder obtener el lock.
	- Método *unlock()*: El proceso libera el lock que tomó previamente con lock.
- Para la implementación se necesita soporte del hardware como del sistema operativo.
- En unix pueden haber varios locks de lectura, pero solo un lock de escritura.
- Para tomar un lock:
	- Si es shared lock (de lectura), se debe esperar a que se liberen todos los exclusive locks.
	- Si es exclusive (write), el proceso debe esperar hasta que sean liberados todos los locks (de ambos tipos)

## Locks en rust

### Traits Send y Sync

- El trait *marker* (no tienen métodos, solo son como labels) **Send** indica que el ownership del tipo que lo implementa puede ser transferido entre threads.
	- Casi todos los tipos de Rust son **Send**.  Hay excepciones como `Rc<T>`
	- Los tipos compuestos que están formados por tipos **Send** automáticamente son Send. Casi todos los tipos primitivos son send, excepto raw pointers (los raw pointers son locales al thread).
- El trait marker **Syn** indica que es seguro para el tipo que implementa Sync ser referenciado desde múltiples threads.
	- Esto es T es Sync if &T (una referencia a T) es Send.
	- Los tipos primitivos son Sync y los tipos compuestos ques están formados por tipos Sync automáticamente son Sync.

### Locks

- Rust provee locks compartidos (de lectura) y locks exclusivos (de escritura) en el módulo: `std::sunc::RxLock`.
- No se provee una política específica sino que es dependiente del sistema operativo.
- Se requiere que T sea Send para ser compartido entre threads y Sync para permitir acceso concurrente entre lectores.
```rust
use std::sync::RwLock
let lock = RwLock::new(5)
```

#### Obtener un lock de lectura

```rust
fn read(&self) -> LockResult<RwLockReadGuard<T>>
```

Bloquea al thread hasta que se pueda obtener el lock con acceso exclusivo.

#### Obtener un lock de escritura

```rust
fn write(&self) -> LockResult<RwLockWriteGuard<T>>
```

Retornan una protección que libera el lock con RAII (Patrón de diseño, que cuando se tiene un recurso tiene que estar inicializado y válido, el destructor se encarga de la liberación de recursos).
Una vez obtenido el lock, se puede acceder al valor protegido.

Un lock queda en estado *envenenado* cuando un thread lo toma de forma exclusiva (write lock) y mientras tiene tomado el lock, ejecuta panic!.
Las llamadas posteriores a read() y write() sobre el mismo lock devolverán Error.