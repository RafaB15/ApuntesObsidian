La virtualización de la memoria le hace creer a un [[Sistemas Operativos/Resumen/Proceso|proceso]] que este tiene toda la memoria disponible para ser reservada y usada como si este fuera siendo ejecutado sólo en la computadora.

Para ejecutarse y ser ejecutado, tanto el proceso como el sistema operativo tienen que estar en memoria.

# Memoria Virtual

La memoria virtual es una abstracción a través de la cual la memoria física puede ser compartida por diversos procesos, dándole a cada uno un [[Sistemas Operativos/Resumen/Address Space|espacio de direcciones]].

Un componente clave de la memoria virtual son las **direcciones virtuales**. Gracias a estas, la memoria de cada proceso empieza en el mismo lugar, la dirección cero, en un espacio de direcciones virtual privado del proceso. Posteriormente la dirección virtual será traducida a una dirección física de memoria.
# Traducción de Direcciones

La traducción de direcciones es el proceso por el cual una **dirección virtual** (emitida por la CPU) es traducida en una **dirección física** de memoria que sea posible usar y no obstruya con ningún otro proceso corriendo. Este mapeo se realiza por hardware, por la Memory Management Unit (MMU), con ayuda del [[Sistemas Operativos/Resumen/Sistema Operativo|Sistema Operativo]] que maneja la memoria.

## Dynamic Relocation

La relocalización dinámica, también conocida como **base and bounds** es una técnica en la cual a cada proceso se le asigna un registro base y otro registro límite.

Cada programa se escribe y compila como si su memoria empezara en la posición cero. Cuando el OS decide cargar el programa en memoria se asigna el valor del registro base a la dirección desde la que se lo va a cargar realmente. 

Con lo cual, cuando se quiera acceder a memoria durante la ejecución del programa, se obtendrá la dirección real de la siguiente manera

$$\text{dirección física} = \text{dirección virtual } + \text{base}$$

La dirección en el registro límite se asegura de que la dirección esté dentro del [[Sistemas Operativos/Resumen/Address Space|espacio de memoria]].

En cuestión de hardware, vamos a necesitar 2 registros que serán parte de la memory management unit (MMU).

Sin embargo, este método tiene la desventaja de que el espacio entre el [[Sistemas Operativos/Resumen/Heap|Heap]] y el [[Sistemas Operativos/Resumen/Stack|Stack]] dentro del espacio de direcciones va a estar vacío, incluso si no se está usando, cuando se traduzca a memoria física, cosa que se arregla con la [[Segmentación]].

![[Sistemas Operativos/Resumen/images/Pasted image 20231003141843.png]]

Mientras que la [[Segmentación|segmentación]] divide la memoria en bloques de tamaño variable, la [[Paging|paginación]] la divide en bloques de igual tamaño.