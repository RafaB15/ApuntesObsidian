- Es un sistema de procesamiento distribuido que posee una abstracción y un framework para ejecutar trabajos de map reduce de forma distribuida y paralela en un cluster.
- Nos soluciona todos los trabajos de bajo nivel.
- APIs en:
    - Java
    - Scala
    - Python
    - R
- Apis de alto nivel:
- RDD API
- Dataframe API
- Spark SQL
- MLib
- GraphX
- GraphFrames
- Spark Streaming

## Arquitectura:

- Comunicación entre un drive y una serie de ejecutores (executors).
- Tareas (jobs) del driver se convierten en tareas para los executors.
- Los resultados de esas tareas vuelven al driver.

## Resilent Distributed Datasets (RDDs)

- Colecciones particionadas en un cluster.
- Guardados en memoria o disco.
- Reconstruidos automáticamente frente a fallos de máquinas o demoras en un job.
- Creados a partir de datos externos.

### Operaciones sobre RDD

- Transformaciones:
    - Crea un nuevo RDD a partir de otro existente.
    - Lazy (solo se va a ejecutar hasta que se le defina una acción). Por ejemplo, si usamos filter nos va a correr en un segundo y recién al usar una acción se va a filtrar. Va a tal extremo que si hacemos take(5) no es que nos filtrará todo el rdd y luego tomará los primeros 5, sino que solo filtrará lo necesario para tener los primeros 5 valores filtrados.
    - Cache (ram o disco).
    - Transformaciones disponibles:
        - Map
        - Filter
        - FlatMap
        - ReduceByKey
        - GroupByKey
        - Join
- Acciones:
    - Devuelven un valor al driver luego de procesar los datos.
    - Acciones disponibles:
        - Reduce
        - Collect
        - Count
        - Take
        - TakeOrdered
        - First