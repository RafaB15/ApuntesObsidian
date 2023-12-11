# Definición

Scheduling o planificación de tareas se refiere a la manera en la que el [[Sistemas Operativos/Resumen/Kernel|kernel]] del sistema operativo decide qué tareas decide ejecutar en qué orden para intentar optimizar el uso de el o los procesadores.

Hay muchas políticas diferentes para determinar estas prioridades, que también dependerán de los recursos que tengamos a nuestra disposición.

# Terminología

- **Tarea (task)**: Una petición de usuario. A veces se lo llama también un **trabajo**. Un proceso puede contener muchas peticiones de usuario, como cada vez que se quiere escribir una letra en un archivo.
- **Turnaround time:** El tiempo que la tarea tarda en completarse desde que llega al scheduler.
$$\displaystyle \large T_{turnaround} = T_{completion} - T_{arival}$$
- **Tiempo de respuesta (Delay)** Se define al response time como el tiempo desde que se llega una tarea al sistema hasta que este es programado (scheduled). El tiempo que el usuario percibe se tardó en hacer una tarea.
$$\displaystyle \large T_{response} = T_{firstrun} - T_{arival}$$
- **Previsibilidad**: Baja varianza en los tiempos de respuesta de una tarea específica.
- **Rendimiento (Throughput)**: El ratio con el que se completan tareas.
- **Costo del Scheduling (Overhead)**: El tiempo de pasar de una tarea a otra.
- **Fairness**: Igualdad de recursos para las tareas.
- **Starvation**: La falta de progreso en una tarea debido a falta de recursos.
- **Carga de trabajo (Workload)**: Las tareas que un sistema tiene que llevar a cabo, y cuándo estas llegan.
- **Time quantum**: También llamado time slice, es un periodo de tiempo que el [[Sistemas Operativos/Resumen/Kernel|kernel]] le otorga a un proceso para que se ejecute.
- **Preemptive**: Un scheduler se considera preemptive cuando puede parar un trabajo para hacer otro.
# Scheduling con Monoprocesador

## First-In-First-Out (FIFO)

- Se refiere a hacer las tareas en el orden en el que estas llegan.
- Ejecuta una tarea hasta que la termina.
- Minimiza el overhead al cambiar de tarea solo al finalizar una.
- Tiene gran nivel de igualdad (fairness).
- Si una tarea corta llega después de una tarea larga, hace al sistema parecer ineficiente.
- No tiene un buen tiempo de respuesta promedio si las tareas tienen tiempos distintos de ejecución. 
- El tiempo de respuesta promedio es óptimo si todas las tareas tardan lo mismo (no es probable).

## Shortest Job First (SJF)

- Se ejecutan las tareas que se estime van a tardar menos primero.
- Tiene un buen tiempo de respuesta promedio, considerando solo el procesador.
- Los tiempos de ejecución se aproximan porque es imposible saberlos con certeza.
- En caso de que el procesador pueda parar de ejecutar una tarea para empezar otra, estamos ante un caso de **Shortest Time-to-Completion First (STCF)**:

## Shortest Time-to-Completion First (STCF):

- Funciona de la misma manera que SJF, sin embargo una vez que empezó una tarea, a medida que avance con dicha tarea, si el tiempo restante de la tarea es mayor al tiempo que le queda a alguna otra tarea, el procesador pasa a ejecutar esa tarea.
- Si una tarea larga se está ejecutando y llega una corta, se pausa la larga para darle prioridad a la corta y luego sigue con la larga.
- Es malo en la varianza del tiempo de respuesta, pues al hacer las tareas pequeñas tan pronto como pueda, hace las largas tan lento como le sea posible.
- Es propenso a sufrir de starvation cuando siguen llegando procesos pequeños y el grande se queda esperando.
## Round Robin

- Las tareas toman turnos ejecutándose en el procesador por un periodo limitado de tiempo.
- Se tiene una lista de las tareas listas para ser ejecutadas y el primero en la lista recibe un time quantum (tiempo) para realizarse en el procesador. 
	- Si la tarea finalizó en el tiempo asignado se avanza al siguiente en la lista.
	- Si la tarea no finalizó entonces se vuelve a poner en la fila y se avanza con el siguiente.
- No hay posibilidad de que una tarea sufra de starvation, pues eventualmente le tocará su turno.
- Si el time quantum es muy corto, entonces habrá mucho overhead al cambiar tanto de tarea.
- Si el time quantum es muy largo entonces las tareas tendrán que esperar mucho para ejecutarse.
- El tiempo promedio de respuesta no es bueno si tiene muchas tareas que tardan lo mismo, pues lo irá intercalando hasta que todos terminen casi al mismo tiempo, el cual será el más largo.
- Si las tareas varían mucho de tamaño, Round Robin se aproxima a SFJ.
- Tiene buen average response time y mal average turnaround time si en time slice es bajo.

## Max-Min Fairness

- Son políticas para intentar maximizar la igualdad en cuanto a la repartición de recursos para las diferentes tareas.
- Max-Min Fairness iterativamente maximiza la mínima cantidad de recursos dado a un proceso en particular hasta que todos los recursos hayan sido asignados. 
	- Si todos los procesos con compute-bound (dependen solo de la máquina) entonces este método sería como Round Robin.
	- Si los procesos son muy cortos o están ligados a dispositivos I/O entonces se puede decidir si dar sus porciones de tiempo extra a otros procesos.
- Otro método que a veces se usa es darle prioridad a las tareas que menos tiempo han pasado en el procesador hasta ahora.

## Input and Output

- Todos los programas hacen uso del input y el output, pero mientras espera obtenerlo, no hacen uso de la CPU, por lo que los schedulers tienen que tener en consideración que el tiempo que un proceso pase allí puede servir para que otra tarea se ejecute en la CPU.
- Una forma eficiente para que el scheduler organice las tareas es pensar que los momentos en los que se espera que un proceso obtenga input o output dividen ese proceso en diferentes tareas, con lo cual si tenemos un proceso A que cada 10 ms esperará input por otros 10 ms, entonces en vez de pensar a A como un programa de 50 ms, lo pensamos como 5 de 10 ms que empieza cuando se salió del disco. De esa forma lo podemos ajustar mejor con otro programa que pueda que no haga uso de I/O.
	![[Sistemas Operativos/Resumen/images/Scheduler con I-O.png]]

## Multi-Level Feedback Queue (MFQ)

- MFQ está diseñado para realizar muchas tareas en simultaneo.
	- Tiempo de respuesta: Ejecuta tareas cortas rápidamente como en SJF.
	- Overhead bajo: Minimiza el número de tareas evacuadas (se las deja de ejecutar, como en FIFO, y minimiza el tiempo tomando decisiones de ordenamiento.
	- Libre de Starvation: Como en Round Robin, todas las tareas tienen que progresar.
	- Tareas en segundo plano: Las tareas de mantenimiento del sistema no interfieren con las tareas del usuario.
	- Igualdad: Se le asigna a cada proceso su porción fair max-min del procesador.
- Se intenta maximizar estas áreas, pero haciendo los compromisos necesarios dependiendo de la situación.
- MFQ es como una extensión de Round Robin con múltiples filas, cada una con un nivel de prioridad distinto así como diferente time quantum.
- Los niveles de prioridad más altos tienen times quanta más bajos que los de prioridad baja.
- Se mueve a las tareas de prioridad para favorecer a las tareas cortas por sobre las largas.
- Si una tarea está esperando a un dispositivo de I/O, se queda en el mismo nivel de prioridad o se lo sube un nivel.
- Si una tarea es completada deja el sistema.
- Un scheduler MLFQ sigue las siguientes reglas:
1. Si $\text{Prioridad(A)} > \text{Prioridad(B)}$, A se ejecuta y B no.
2. Si $\text{Prioridad(A)} = \text{Prioridad(B)}$, A y B se ejecutan de manera Round Robin utilizando el time slice (quantum time) de la fila en la que están.
3. Cuando una tarea entra al sistema se la coloca en el nivel de prioridad más alto.
4. Cuando una tarea usa su tiempo correspondiente en una fila (independientemente de cuantas veces haya cedido la CPU para fijarse en I/O), su prioridad es reducida (baja a la siguiente fila).
	- Si una tarea utiliza la totalidad de su time slice al momento en el que se le entrega, se la baja de prioridad.
	- Si se fija en operaciones de I/O, cediendo la CPU, entonces se queda en el mismo nivel y al volver continua. Sin embargo, si todo el tiempo que **sí** se estuvo ejecutando en ese nivel supera el time slice de ese nivel, entonces se lo baja de nivel. 
5. Después de un periodo de tiempo *S*, se mueven todas las tareas en el sistema a la fila con la prioridad más alta.
- MLFQ, en vez de demandar conocimiento *a priori* de cuanto va a tardar una tarea, observa la ejecución de una tarea y la prioriza acordemente, al principio tratando a todas las tareas como si fueran a tardar poco, y acomodándolas dependiendo de los tiempos que tardan.
