**Problema:** Necesidad de procesar grandes volúmenes de datos.

**Map reduce** es un procesamiento distribuido de datos utilizando un **cluster.**

Un **cluster** es un conjunto de computadoras que trabajan juntas y pueden ser vistas como un sistema único. A cada computadora del cluster se le conoce como un nodo.

 

![[Organización de datos/Spark/Map-Reduce/Untitled.png|Untitled]]

![[Organización de datos/Spark/Map-Reduce/Untitled 1.png|Untitled]]

![[Organización de datos/Spark/Map-Reduce/Untitled 2.png|Untitled]]

## Almacenamiento distribuido

- El FileSystem Distribuido es el encargado de gestionar cómo y dónde guarda la información en una computadora y cómo poder consultarla.
- Almacenar grandes volúmenes de datos en múltiples equipos.
- Replicación de datos.
- Tolerante a fallos.
- Alta disponibilidad.
- Relativo bajo costo.
- Implementaciones:
    - GFS (Google)
    - HDFS (Apache Hadoop)

![[Organización de datos/Spark/Map-Reduce/Untitled 3.png|Untitled]]

- CEPH
- S3 (Amazon)

## Map-Reduce:

- Modelo de programación para procesar grandes conjuntos de datos.
- Responde a la necesidad de procesar grandes volúmenes de datos de forma escalable.
- El usuario especifica una función **map** que procesa un par clave/valor para generar un conjunto intermedio de pares clave/valor.
- Se debe especificar también una función **reduce** que combina todos los valores asociados a la misma clave.

## Map

- Transforma nuestros datos.
- Debe ser aplicada a cada dato de nuestro set.
- Puede ser paralelizada y distribuirse entre las distintas máquinas de un cluster para aprovechar todos nuestro poder de procesamiento.
- Algunas diferencias dependientes de la implementación:
    - **Hadoop: $Map(k,v)\to[k_2,v_2]$**
        - Un map convierte un registro clave/valor a otro registro clave/valor.
    - **Spark:     $Map(r) \to [r']$**
        - Un map no diferencia entre clave y valor sino que toma todos los registros como uno.

## Reduce:

- Combina los resultados del map.
- Es necesario procesar los datos de todas las máquinas del cluster.
- Reduce locales en paralelo y reduce entre máquinas mediante etapa de shufflle & sort.
- Algunas diferencias funcionales en el reduce:
    - **Reduce Hadoop:**
        - $ReduceByKey((k,v),f)\to[(k,v)]$
        - El sistema agrupa todos los registros para los cuales la clave es la misma.
        - Requiere que todos los registros de igual clave estén en el mismo equipo que ejecute el reduce: Shuffle & Sort.
    - **Reduce Spark:**
        - ReduceByKey: Combina los elementos para una misma clave.
        - Reduce: da un único resultado para todo el set de datos.
        - La función reduce toma dos valores para dar como resultado la combinación de ambos.
        - El resultado de un reduce entre dos registros es el input del siguiente reduce.
        - Ejemplo:
            - (fecha,cliente,importe)
            - Map(a):
                - a[importe]
            - Reduce(a,b):
                - a + b
        - Operaciones conmutativas y asociativas de modo de poder ejecutarse distribuidas.
- **Shuffle & Sort:**
    - Mueve la salida de un proceso map a un cierto equipo de tal forma que un reducer pueda procesar sus registros.
    - Fase más costosa del proceso Map-Reduce.
    - Optimización para reducir la cantidad de datos a transmitir por la red.
- Framework Map-Reduce:
    - Abstracción para el procesamiento distribuido.
    - API de distintos niveles para ejecutar Map-Reduce
    - Manejo del framework de los trabajos a ejecutar en cada máquina del cluster.
    - División de los trabajos entre los nodos del cluster.
    - Manejo de errores en los trabajos.
    - El framework nos soluciona varios de estos inconvenientes.
    - Nos da opciones de cómo manejarlos.