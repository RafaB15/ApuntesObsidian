El Kernel es el nivel más bajo de software corriendo en el sistema, que tiene acceso total a todo el hardware de la máquina. El Kernel tiene permiso para hacer cualquier cosa con el hardware. Cualquier otro software corriendo en el sistema es considerado no confiable y se lo corre en un ambiente restringido con menor acceso al poder completo del hardware.
![[Sistemas Operativos/Resumen/images/KernelTrusted.png]]
El Kernel corre directamente en el procesador con derechos ilimitados.

El Kernel también se encarga de la protección en el sistema operativo. Esto es el aislamiento de aplicaciones y usuarios que no se están comportando como se espera para que no corrompan otras aplicaciones o el propio sistema operativo. 

El Kernel en sí también es un [[Sistemas Operativos/Resumen/Proceso|proceso]]. De hecho, es el primer proceso en ejecutarse al iniciar la computadora.
# Tareas específicas del Kernel

- Planificar la ejecución de las aplicaciones
- Gestionar la Memoria
- Proveer un sistema de archivos
- Creación y finalización de procesos
- Acceder a los dispositivos
- Comunicaciones
- Proveer un API

# Modo de Operación Dual

El procesador tiene dos modos que son seleccionados por un bit en el registro de estado del procesador.
## User Mode

En este modo el procesador chequea cada instrucción antes de ejecutarla para cerciorarse de que el proceso corriendo actualmente tiene permiso para hacerlo.

## Kernel Mode

En este modo, el sistema operativo ejecuta comandos con los chequeos apagados.

# Instrucciones Privilegiadas

Estas son instrucciones accesibles en Kernel Mode pero no en User Mode. El Kernel las necesita para poder hacer su trabajo.
- Cambiar niveles de privilegios.
- Ajustar acceso a memoria.
- Habilitar y deshabilitar interrupciones.

# Protección de Memoria

Para prevenir que [[Sistemas Operativos/Resumen/Proceso|procesos]] accedan a memoria que no tienen permiso de acceder los procesadores modernos introducen Virtual Addresses, con las cuales, las direcciones de memoria de cada proceso empiezan en el mismo lugar y cada proceso piensa que tiene toda la máquina para sí mismo, aunque este no sea realmente el caso.

El hardware traduce estas direcciones virtuales a direcciones de memoria física.

# Timer Interrupts

Los sistemas computarizados normalmente incluyen un aparato llamado **hardware timer**, el cual puede configurarse para interrumpir al procesador después de un tiempo especificado o después de que una cantidad de instrucciones específica se han ejecutado. Esto se hace para que el control se pueda devolver al kernel y este chequee que todo está bien y decidir si continuar con este proceso o no.

El que se active un timer y otro método de interrupción no significa siempre que hubo un error. En la mayoría de los casos el sistema operativo resume la ejecución del proceso, configurando el modo, el contador de programa y los registros de vuelta a los valores que tenían previo a la interrupción.

# Tipos de transferencia de modo

## User a Kernel Mode

**Trap**: Cualquier transferencia de control sincrónica de user mode a kernel mode
### Interrupts

Cuando se da la señal de una interrupción el modo pasa de User Mode a Kernel Mode, el hardware del procesador guarda el estado de la ejecución actual y empieza a ejecutarse en un espacio designado para manejar las interrupciones.

Si fue un interrupt por un timer, entonces se chequea si el proceso responde a input del usuario para detectar si entró en un loop infinito.

También se usan interrupciones para informar al Kernel que se completaron I/O requests.

### Excepciones de proceso

Una excepción de proceso es un evento de hardware causado por el comportamiento de un programa usuario, el cual genera un pasaje de control del usuario al kernel.

Ocurre siempre que un proceso intenta ejecutar una instrucción privilegiada o acceder a memoria fuera de la región que a este le corresponde. Puede ocurrir también si un proceso divide un número por cero, intenta escribir a memoria que solo puede leer, entre otras cosas.

En estos casos el Kernel para el programa y devuelve un error al usuario.

### System calls

Una [[Sistemas Operativos/Resumen/System Call| llamada al sistema]] es cualquier procedimiento que el Kernel provee que puede ser llamado desde el nivel de usuario.

Para el programa del usuario, estos se llaman como procedimientos normales, con parámetros y valores que devuelven, a pesar de que por debajo estos en realidad están siendo ejecutados por el Kernel.

Cuando el Kernel completa la llamada al sistema, este resume la ejecución a nivel de usuario inmediatamente después de la trap.

## Kernel a User Mode

### Nuevo Proceso

Para iniciar un nuevo proceso, el kernel copia el programa en memoria, inicializa el contador del programa a la primera instrucción del proceso, inicializa el puntero del stack a la base del stack del usuario y cambia a user mode.

### Resume after an interrupt, processor exception, or system call.

Cuando el kernel termina de manejar el pedido, vuelve a la ejecución del proceso interrumpido.

### Cambiar a un proceso diferente

A veces, después de una interrupción, el kernel va a cambiar a un proceso diferente y luego a user mode, guardando la información necesaria para continuar con el proceso anterior posteriormente.