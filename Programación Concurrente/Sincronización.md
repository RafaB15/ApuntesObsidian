# Estados de ejecución de un proceso

![[Estados de un proceso.png]]

Nuevo -> Se crea con fork
Listo -> Listo para ser ejecutado
En ejecución -> El scheduler lo ejecuta
En espera -> El proceso está bloqueado y no consume recursos hasta que se termine la operación de entrada y salida que la frenaba, o la espera por un lock.
Finalizado -> Se llama a la system call que solicita finalizar (exit()). 

# Semáforos
- Mecanismos de sincronismo, implementado como una construcción de programación concurrente de más alto nivel.
- Sirven únicamente como sincronización y no como transmisores de información.
- Es un tipo de dato compuesto por dos campos
	- Un entero no negativo llamado V
		- Representa cuantos pueden acceder a la información
	- Un set de procesos llamado L
		- Es un conjunto de procesos que están esperando a que se libere la información (se llame signal)
- Se inicializa con un valor $k \ge 0$ y con el conjunto vacío $\varnothing$ 
- Se definen dos operaciones atómicas sobre un semáforo **S**.
	- *wait(S)* también llamada *p(S)*
		- Reduce V en uno si es mayor a cero. Si es igual a cero, agrega el proceso que quiso acceder a L y este pasa al estado Blocked.
	- *signal(S)* también llamada *v(S)*.
		- Aumenta V en uno. Se saca un proceso de L (arbitrariamente) y se pone en estado Ready.
- Son mecanismos de sincronismo de acceso a un recurso.
- Un semáforo es un contador
	- Si $\text{contador} > 0 \implies \text{recurso disponible}$
	- Si $\text{contador} \le 0 \implies \text{recurso no disponible}$ 
	- El valor del semáforo representa la cantidad de recursos disponibles.
	- Si el valor es menor a cero entonces el valor no está disponible, si es mayor está disponible.
	- Si el valor es cero o uno se llaman semáforos binarios y se comportan igual que los locks de escritura (también conocidos como **Mutex**).
- Operaciones:
	- p(wait) resta 1 al contador
	- v (signal) suma 1 al contador
## Semáforo binario o Mutex

- El valor V sólo puede tomar los valores 0 o 1.
- Se inicializa como (0, $\varnothing$) o (1, $\varnothing$)
- La operación signal(S) se define como
```
if s.v = 1
	// undefined, si es binario la lógica de nuestro programa no debería permitir esto
 else if S.L is empty
	 S.V := 1
 else 
	 sea q un elemento arbitrario del conjunto S.L
	 S.L remove q
	 q.state := ready
```

- wait y signal son instrucciones atómicas.
- Un semáforo debe ser inicializado con un valor entero no negativo.
- La instrucción signal() debe despertar a uno de los procesos suspendidos, pero no está definido cuál de todos los procesos debe despertarse (al azar).
- Invariantes del semáforo -> Propiedades que se ven siempre
	- $S.V \ge O$
	- $S,V = k + \#signal(S) - \#wait(S)$, siendo *k* el valor inicial del semáforo. # = cant de veces que hicimos.
- Tipos de semáforos:
	- System V
	- POSIX
- Un semáforo system V está compuesto por:
	- El valor del semáforo
	- El process id del último proceso que utilizó el semáforo.
	- La cantidad de procesos esperando por el semáforo.
	- La cantidad de procesos esperando por el semáforo.
	- La cantidad de procesos que está esperando que el semáforo sea cero.

# Semáforos en Rust

- Usamos el crate std-semaphore:
- Inicializar el semáforo:
```rust
let sem = Semaphore::new(5);
```
- Obtener el acceso (wait):
```rust
fn acquire(&self)
```
- Liberar el semáforo:
```rust
fn release(&self)
```
- (extra) Obtener el acceso con el patrón RAII (wait):
```rust
fn access(&self)
```

# Barreras en Rust

- Permiten sincronizar varios threads en puntos determinados de un cálculo o algoritmo.
- Están en el módulo std::sync::Barrier
- Bloquea al thread hasta que la barrera internamente valga cero.
- Creación de la barrera
```rust
fn new(n: usize) -> Barrier
```
n son cuantos threads queremos sincronizar.
- Bloquear al thread hasta que todos se encuentren en el punto
```rust
fn wait(&self) -> BarrierWaitResult
```
- Operación interesante **lider**. El último que hace wait. 
- El método BarrierWaitResult::is_leader() devuelve *true* en el thread lider.
- Las barreras son reutilizables automáticamente. Cuando el último hace wait se desbloquean todos.
- El semáforo nunca pide el valor interno del contador.
- Ejercicios conocidos:
![[Ej semáforo 1.png]]![[Ej semáforo 2.png]]
- Básicamente como las barreras solo se liberan si llegan N threads a estas, entonces nos ayuda a sincronizarlas en un punto.