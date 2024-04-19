- Es un estilo de paralelización donde el cómputo (*task*) es partido en sub-cómputos (*subtasks*). Los resultados de estos se unen (*join*) para construir la solución al cómputo inicial. 
- Partir el cómputo se realiza en general de forma recursiva (las subtareas pueden a su vez subdividirse): 
	- los sub-cómputos son independientes → el cómputo se puede realizar en paralelo.
- Las sub-tareas se pueden crear en cualquier momento de la ejecución de la tarea.
- Las tareas **no deben bloquearse**, excepto para esperar el final de las subtareas.
![[Fork Join.png]]

- Modelo de concurrencia sin condiciones de carrera. 
- Los programas fork-join son determinísticos, los threads están aislados. El programa produce el mismo resultado independientemente de las diferencias de velocidad de los threads (determinístico).
- **Performance**: en el caso ideal $t_{secuencial}/N_{threads}$ . Puede variar por diferencias en el tamaño de una tareas, y porque se debe realizar procesamiento para hacer la **combinación** de los resultados individuales. 
- **Desventaja**: requiere que las unidades de trabajo (tareas) sean aisladas.

![[Fork Join Program.png]]

# Work Stealing

- Algoritmo usado para hacer scheduling de tareas entre threads.
- **Work stealing** (Robo de trabajo): worker threads inactivos roban trabajo a threads ocupados, para realizar balanceo de carga. 
	- Cada thread tiene su propia cola de dos extremos (en los que se puede agregar y sacar) (*deque*) donde almacena las tareas listas por ejecutar. 
	- Cuando un thread termina la ejecución de una tarea, coloca las subtareas creadas al final de la cola. 
	- Luego, toma la siguiente tarea para ser ejecutada del final de la cola. 
	- Si la cola está vacía, y el thread no tiene más trabajo, tratar de robar tareas del inicio de una cola de otro thread (random).
- Se hace con una cola de doble entrada para disminuir los casos en donde hay un bloqueo al dos threads querer tomar el mismo trabajo.
- También para que los threads que terminaron saquen las tareas más viejas, las cuales seguro son más grandes. De esa forma también pasa más tiempo entre cada obtención de trabajo.

- **Ventajas:**
	- Los worker threads se comunican solamente cuando lo necesitas $\to$ menos necesidad de sincronización.
	- La implementación de la cola deque agrega bajo overhead de sincronización.
# Rayon
Rayon es una biblioteca muy popular, creada por Niko Matsakis, que implementa el modelo fork join de 2 formas. 
- Realizar dos tareas en paralelo: 
	
```rust
let (v1, v2) = rayon::join(fn1, fn2);
```
- invoca a fn1 y fn2 y retorna una tupla con ambos resultados.
- Realizar **N** tareas en paralelo:
```rust
giant_vector.par_iter().for_each(|value| {
	do_thing_with_value(value); 
});
``` 
El método .par_iter() crear un iterador Parallel Iterator similar a los iteradores de Rust, pero que se ejecutan en apralelo. Rayon maneja los threads y ditribuye el trabajo.

![[Rayon.png]]

- Desde afuera, Rayon parece crear una tarea por elemento del vector. 
- Internamente, crea un worker thread por núcleo de CPU. 
- Implementa: Work stealing. Los métodos .reduce() y .reduce_with() se usan para combinar los resultados.