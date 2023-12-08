El proceso es la ejecución de un programa con permisos restringidos. Es la abstracción de una ejecución protegida brindada por el [[Kernel]] del [[Sistema Operativo|sistema operativo]].

Se pasa de un archivo de código escrito en algún lenguaje de alto nivel a un archivo que se puede ejecutar mediante el [[Sistemas Operativos/Resumen/Proceso de Compilación|proceso de compilación]].

Un proceso es una instancia de un programa. Cada programa puede tener cero, uno o más procesos ejecutándolo. Por cada instancia de un programa, hay un proceso con su propia copia del programa en memoria.

Un proceso necesita permisos del [[Sistemas Operativos/Resumen/Kernel|kernel]] del sistema operativo antes de acceder a la memoria de cualquier otro proceso, antes de leer o escribir en disco, cambiar las configuraciones del hardware, entre otras cosas. En otras palabras, el kernel del sistema operativo hace de intermediario y chequea el acceso al hardware de cada proceso.

Un proceso incluye:
- Los archivos abiertos
- Las señales (signals) pendientes.
- Datos internos del kernel.
- El estado completo del procesador.
- Un espacio de direcciones de memoria.
- Uno o más hilos de Ejecución. Cada thread contiene
	- Un único contador de programa
	- Un stack
	- Un conjunto de registros.
- Una sección de datos globales.

Mientras existe un proceso, el sistema operativo se encarga de dos tipos muy importantes de virtualización. 
1. La [[Sistemas Operativos/Resumen/Virtualización de Memoria|Virtualización de Memoria]],  a través de la cual el SO se asegura que los distintos procesos puedan hacer uso de la memoria física sin pisarse entre sí.
2. La [[Sistemas Operativos/Resumen/Virtualización del Procesador|Virtualización del Procesador]], a través de la cual el SO se encarga de que cada proceso piense que tiene un procesador entero para sí mismo.

# Contexto

Cada **proceso** tiene un **contexto** bien definido que comprende toda la información necesaria para describir completamente al mismo.

El contexto de un proceso consiste en:

- [[Address Space|User Address Space]]: normalmente está dividido en varias áreas: text, data, stack y heap,
- **Control Information**: el kernel utiliza dos estructuras principales para mantener información de control de un proceso- la **user area** y la estructura _proc_. Cada proceso además tiene su propio **kernel stack** y **mapas de traducción de direcciones**.
- **Credentials**: Las credenciales del proceso incluyen los groups IDs y user id, asociados con él.
- **Variables de entorno**: son un conjunto de strings del formato variable=valor que son heredadas del proceso padre.
- **Hardware Context**: Esto contiene el contenido de los registros de propósito general, y de un conjunto especial de registros del sistema:
	- El Program Counter (_PC_)  
	- El Stack Pointer (_SP_)
	- El Processor Status Word (PWD)
	- Memory Management Registers
	- Los Registros de la Unidad de Punto Flotante.