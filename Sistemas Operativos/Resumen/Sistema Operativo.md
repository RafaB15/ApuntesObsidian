Un **Sistema Operativo (OS):** 

-  Se ejecuta como la capa de software de más bajo nivel en la computadora.
- Es la **capa de software** que **maneja** los **recursos de una computadora** para sus **usuarios** y sus **aplicaciones**.
- Un **sistema operativo** está diseñado para **ocultar** detalles de **hardware de bajo nivel** y para crear una **máquina abstracta** que le proporcione a las **aplicaciones** servicios de **alto nivel**.
- **Interactúa directamente con el hardware**, proporcionando **servicios comunes** a los programas y **aislándolos** de idiosincrasia de hardware.
- Es el **software** que **controla** los **recursos de hardware** de una **computadora** y **provee** un **ambiente** bajo el cual los **programas pueden ejecutarse**.
- Al tener que administrar los recursos de los diferentes programas corriendo, al OS también se lo conoce como un ***resource manager.***
- El SO hace uso de la [[Sistemas Operativos/Resumen/Virtualización|virtualización]] para hacer que la ejecución de los programas parezca algo fácil, virtualizando:
	- El procesador
	- La memoria
	- La persistencia (dispositivos de almacenamiento)

# Roles
Un sistema operativo tiene que cumplir 3 roles:
## Referee

Un OS gestiona recursos compartidos entre diferentes aplicaciones que se encuentran ejecutándose en la misma máquina física. 

- Un OS puede frenar la ejecución de una aplicación e iniciar la ejecución de otra.
- Los OS aíslan a cada aplicación de las demás que se encuentran corriendo en la misma computadora.
- Por ende un OS tiene que protegerse a sí mismo y a las demás aplicaciones que se están ejecutando en la misma computadora.
- Dado que todas estas aplicaciones comparten los ***mismos recursos físicos*** el OS decide qué aplicación usa un determinado recurso y cuando

## Ilusionista

Un OS debe proveer una abstracción del hardware para simplificar el diseño de aplicaciones.
El sistema operativo provee la ilusión de que se dispone de toda la memoria para almacenar al programa, cuando realmente se sabe que la memoria real de la computadora es finita.

## Pegamento

Un OS debe proveer una serie de ***servicios comunes*** que faciliten un mecanismo que permita compartir, por ejemplo, información entre las aplicaciones (ej. Cut and paste, look and feel, acceso a los dispositivos de entrada y salida del sistema)

# Kernel

El nivel más bajo de software corriendo en el sistema operativo se conoce como [[Sistemas Operativos/Resumen/Kernel|Kernel]], el cual tiene permisos para hacer cualquier cosa dentro del sistema operativo.

Cuando un programa está corriendo, este alterna entre user mode y kernel mode, dependiendo de los permisos necesarios para ejecutar ciertas acciones.

# Procesos

Una vez que un programa se convierte en un ejecutable a través del [[Sistemas Operativos/Resumen/Proceso de Compilación|proceso de compilación]], para correr el programa, el SO copia las instrucciones y datos de la imagen ejecutable a la memoria física. El SO reserva las parte de la memoria llamadas el stack de ejecución y el heap.

Una vez que el programa es cargado en memoria, el SO puede empezar a correrlo seteando el stack pointer y saltando a la primera instrucción del programa.

El sistema operativo lleva la contabilidad de todos los [[Sistemas Operativos/Resumen/Proceso|procesos]] que se están ejecutando en la computadora mediante la utilización de una estructura llamada Process Control Block o PCB. La PCB almacena toda la información que un sistema operativo debe conocer sobre un proceso en particular:

- Donde se encuentra almacenado en memoria.
- Donde la imagen ejecutable esta en el disco.
- Que usuario solicito su ejecución.
- Que privilegios tiene ese proceso.

Además el S.O. crea la ilusión de la existencia de varios cientos o miles de procesadores, cuando en realidad tiene uno solo, mediante la [[Sistemas Operativos/Resumen/Virtualización#Virtualización del Procesador|virtualización de la CPU]].