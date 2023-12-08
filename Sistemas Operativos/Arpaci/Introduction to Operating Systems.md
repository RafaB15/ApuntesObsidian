# Ejecución de un programa

Ciclo continuo de FETCH → DECODE → EXECUTE

El procesador busca (***fetch)*** una instrucción en la memoria, la decodifica (***decode***) (averigua qué instrucción es) y la ejecuta (***execute***) (sumar números, saltar a una función acceder a memoria).

Al terminar, el ***procesador*** pasa a la siguiente instrucción hasta que finalice el programa.

Esta es la base del modelo de computación de Von Neumann.

# Sistema Operativo

Hace que los programas sean fáciles de utilizar, incluso al mismo tiempo, dejándolos compartir memoria e interactuar con dispositivos.

Esto lo hace a partir de una técnica llamada ***Virtualización***

## Virtualización

El OS toma un recurso físico, como un procesador, una memoria o un disco, y lo transforma en una versión **virtual** más general, poderosa y fácil de usar. Por eso a veces nos referimos al SO  como una Virtual Machine.

El OS también provee interfaces (APIs) que se pueden llamar para decirle qué hacer. Estas se llaman ***System Calls***. Decimos que el OS provee una ***standard library*** a las aplicaciones.

Al tener que administrar los recursos de los diferentes programas corriendo, al OS también se lo conoce como un ***resource manager.***

A veces llamamos a un procesador CPU.

Un programa guarda todas sus estructuras de datos en memoria, por lo que mientras un programa corre este accede a memoria muchas veces. También se accede a memoria cada vez que se hace un ***fetch*** para buscar la siguiente instrucción.

Si tenemos dos programas que están ejecutándose al mismo tiempo y dentro de ese programa se utiliza la misma dirección de memoria, el OS al virtualizar la memoria se encarga de que cada proceso acceda espacio de direcciones virtual privado, el cual luego el OS mapea a un espacio de la memoria física de la máquina.

El software en un sistema operativo que normalmente se encarga de manejar el disco de memoria se conoce como ***File System***, el cual se encarga de guardar cualquier archivo que el usuario crea de forma confiable y eficiente en los discos del sistema. Los archivos se comparten a través de diferentes procesos (No se hace una versión virtualizada local para cada uno, pues se sabe que los programas querrán acceder a alguno de los que ya existen).