Una system call es un punto de entrada controlado al kernel, permitiendo a un proceso solicitar que el **kernel** realice alguna operación en su nombre. El kernel expone una gran cantidad de servicios accesibles por un programa vía el application programming interface (API) de system calls.

Algunas características generales de las system calls son:

- Una system call cambia el modo del procesador de user mode a kernel mode, por ende la CPU podrá acceder al área protegida del kernel.
- El conjunto de system calls es fijo. Cada system call esta identificada por un único número, que por supuesto no es visible al programa, este sólo conoce su nombre.
- Cada system call debe tener un conjunto de parámetros que especifican información que debe ser transferida desde el _user space_ al _kernel space_.

# Llamada a una System Call
Desde el punto de vista de un programa llamar a una system call es como invocar a una función de C. Por supuesto, detrás de bambalinas muchas cosas suceden:

1. El programa realiza un llamado a una system call mediante la invocación de una función **wrapper** (envoltorio) en la biblioteca de C.
2. Dicha función **wrapper** tiene que proporcionar todos los argumentos al **system call trap_handling**. La función, internamente, llamará a la sys call con los argumentos adecuados.
3. Dado que todas las system calls son accedidas de la misma forma, el kernel tiene que saber identificarlas de alguna forma. Para poder hacer esto, la función _wrapper_ copia el número de la system call a un determinado registro de la CPU (%eax).
4. La función _wrapper_ ejecuta una instrucción de código maquina llamada **trap machine instruction** (int 0x80), esta causa que el procesador pase de _user mode_ a _kernel mode_ y ejecute el código apuntado por la dirección 0x80 (128) del vector de traps del sistema.
5. En respuesta al trap de la posición 128, el kernel invoca su propia función llamada _syste_call()_ (arch/i386/entry.s) para manejar esa trap.
6. Si el valor de retorno del la rutina de servicio de la system call da error, la función wrapper setea el valor en _errno_.

# Fork

Esta llamada la sistema es utilizada para crear un nuevo proceso. El nuevo proceso es una copia casi idéntica a la del proceso padre, con diferente [[Identificador de Proceso|PID]].

La función fork va a devolver el [[Sistemas Operativos/Resumen/Identificador de Proceso|PID]] del proceso hijo en caso de que seamos el proceso padre y va a devolver cero en caso de que seamos el proceso hijo.

# Wait

Esta llamada al sistema frena la ejecución del proceso que la llama hasta que sus hijos terminen de ejecutarse.

Hay otra versión, waitpid, la cual espera a que termine de ejecutarse el proceso cuyo [[Sistemas Operativos/Resumen/Identificador de Proceso|PID]] se le pase por parámetro.

# Exec

La llamada al sistema exec y sus variaciones se encargan de reemplazar el proceso que está siendo ejecutado actualmente por uno en un binario especificado que se le pasa por parámetro junto con sus argumentos. 

El heap, el stack y el resto de partes del espacio de memoria son re inicializadas.

# Kill

Esta llamada la sistema es utilizada para mandar señales a un proceso, incluyendo directivas para pausar, morir u otras órdenes.