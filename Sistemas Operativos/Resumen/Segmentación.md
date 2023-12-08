
La segmentación es una técnica de [[Virtualización de Memoria|virtualización de memoria]].

También llamado **Base and Bounds generalizado**, en esta versión, en vez de tener solo un registro base y otro límite, tendremos dos registros para cada espacio de memoria lógico (en nuestro caso el [[Stack]], el [[Heap]] y el código), con lo cual todo el espacio que esté entre estos registros será el que en realidad se está utilizando, y no tendremos espacio vacío que podría estar utilizando otro proceso.

![[Memoria reservada con segmentación.png]]

En cuestión de hardware, para poder usar **base and bounds generalizado** necesitaremos contar con 3 pares de registros en el MMU.

A la hora de pasar de memoria virtual a memoria física, agarramos la dirección de memoria virtual, le restamos la dirección del inicio del área en la que está ubicada (heap, stack, código) para obtener el *offset*, sumamos el offset al registro base de esa zona y, si es una dirección válida, entonces accedemos a esta.

Para poder soportar que los segmentos puedan crecen de manera descendiente (como lo hace el stack), tenemos que tener un registro más para cada segmento que con un bit nos indique si crece positiva o negativamente.

También, para dar soporte a compartir memoria entre varios procesos, podemos agregar otro registro con **bits de protección** que diga si el código en un [[Address Space]] es Read-Only, Read-Write, etc.

**coarse-grained segmentation:** Nuestros segmentos son relativamente grandes.
**fine-grained segmentation:** Nuestros segmentos son relativamente pequeños.

**External fragmentation:** Cuando tenemos muchos espacios de memoria libre que juntos nos dan la memoria que necesitamos, pero estos no son contiguos, haciendo que no podamos asignarlos a los procesos que nos piden memoria física.

La idea de la segmentación es entonces la de dividir la memoria en trozos de tamaño variable e irlos acomodando. Otro manera de afrontar el problema con pedazos de igual tamaño sería con [[Paging]].