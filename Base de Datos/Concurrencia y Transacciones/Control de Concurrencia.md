Enfoques para controlar la [[Concurrencia|concurrencia]].
- **Enfoque pesimista:** Busca garantizar que no se produzcan [[Conflicto|conflictos]].
	- Basado en locks.
- **Enfoque optimista**: Consiste en "dejar hacer" a las [[Transacción|transacciones]], y deshacer (*rollback*) una de ellas si en *fase de validación* se descubre un conflicto. Conveniente cuando la probabilidad de conflicto es baja.
	- Control de concurrencia basado en *timestamps*.
	- Snapshot Isolation.
	- Control de concurrencia multiversión (MVCC).

# Control de concurrencia basado en locks

- En este método, el [[Sistemas de gestión de bases de datos|SGBD]] utiliza locks para bloquear a los recursos (los ítems) y no permitir que más de una transacción los use en forma simultánea. 
- Los *locks* son insertados por el SGBD como instrucciones especiales en medio de la transacción. 
- Una vez insertados, las transacciones compiten entre ellas por su ejecución. 
### Locks
- Son variables asociadas a determinados recursos, y que permiten regular el acceso a los mismos en los sistemas concurrentes. 
- Son una herramienta para resolver el problema de la exclusión mutua. 
- Un lock debe disponer de dos primitivas de uso, que permiten tomar y liberar el recurso *X* asociado al mismo: 
	- `Acquire(X)` ó `Lock(X) (L(X))`. 
	- ``Release(X)`` ó ``Unlock(X) (U(X))``. 
- Tienen carácter bloqueante: Cuando una transacción *tiene* un lock sobre un ítem *X*, ninguna otra transacción puede adquirir un lock sobre el mismo ítem hasta tanto la primera no lo libere. 
- Es fundamental que dichas primitivas sean atómicas. Es decir, la ejecución de la primitiva ``Lock(X)`` sobre un recurso *X* no puede estar solapada con una ejecución semejante en otra transacción. 
	- Lock(X) requiere leer y escribir una variable.

![[Cuadro ejemplo locks.png]]

# Protocolo de Lock de 2 fases (2PL)

- Una transacción no puede adquirir un *lock* luego de haber liberado un *lock* que había adquirido.
- La regla divide naturalmente en dos fases a la ejecución de la transacción:
	- Una fase de adquisición de locks, en la que la cantidad de locks adquiridos crece. 
	- Una fase de liberación de locks, en que la cantidad de locks adquiridos decrece.
- El cumplimiento de este protocolo es condición suficiente para garantizar que cualquier orden de ejecución de un conjunto de transacciones sea serializable

# Problemas

### Bloqueo o Deadlock

- Un deadlock es una condición en que un conjunto de transacciones quedan cada una de ellas bloqueada a la espera de recursos que otra de ellas posee.
![[Ejemplo deadlock.png]]

- **Mecanismos de prevención de deadlocks:** 
	1. Que cada transacción adquiera todos los locks que necesita antes de comenzar su primera instrucción, y en forma simultánea. ($Lock(X_1, X_2, \dots, X_n)$). 
	2. Definir un ordenamiento de los recursos, y obligar a que luego todas las transacciones respeten dicho ordenamiento en la adquisición de locks. 
	3. Métodos basados en timestamps. 
- La limitación del enfoque preventivo es que será necesario saber qué recursos serán necesarios de antemano.

- **Mecanismos de detección de deadlocks:** 
	1. Analizar el grafo de alocación de recursos: un grafo dirigido que posee a las transacciones y los recursos como nodos, y en el cual se coloca un arco de una transacción a un recurso cada vez que una transacción espera por un recurso, y un arco de un recurso a una transacción cada vez que la transacción posee el lock de dicho recurso. 
		- Cuando se detecta un ciclo en este grafo, se aborta (rollback) una de las transacciones involucradas. 
		- El concepto es muy similar al del grafo de precedencias para un solapamiento.
	2. Definir un *timeout* para la adquisición del *Lock(X)*, después del cual se aborta la transacción.

### Inanición

- La inanición es una condición vinculada con el deadlock, y ocurre cuando una transacción no logra ejecutarse por un periodo de tiempo indefinido.
- Puede suceder por ejemplo, si ante la detección de un deadlock se elije siempre a la misma transacción para ser abortada. 
- La solución más común consiste en encolar los pedidos de locks, de manera que las transacciones que esperan desde hace más tiempo por un recurso tengan prioridad en la adquisición de su lock

# Control de concurrencia basado en timestamps

- Se asigna a cada transacción $T_i$ un timestamp $TS(T_i)$ (p.ej, un número de secuencia, o la fecha actual del reloj). 
- Los *timestamps* deben ser únicos, y determinarán el orden serial respecto al cual el solapamiento deberá ser equivalente. 
- Se permite la ocurrencia de conflictos, pero siempre que las transacciones de cada conflicto aparezcan de acuerdo al orden serial equivalente: 
$$(W_{T_i} (X), R_{T_j} (X)) → TS(T_i) < TS(T_j)$$
- Al no emplear locks, este método está exento de deadlocks.

# Protocolo de lock de 2 fases estricto (S2PL)

Una transacción no puede adquirir un lock luego de haber liberado un lock que había adquirido, y además los locks de escritura sólo pueden ser liberados después de haber commiteado la transacción.

# Protocolo de lock de 2 fases riguroso (R2PL)

Los locks sólo pueden ser liberados después del commit. No diferencia los tipos de lock.
# Snapshot Isolation

- Cada transacción ve una snapshot de la base de datos correspondiente al instante de su inicio. 
- **Ventaja**: 
	- Permite un mayor solapamiento, ya que lecturas que hubieran sido bloqueadas utilizando locks, ahora siempre pueden realizarse. 
- **Desventajas**: 
	- Requiere de mayor espacio en disco o memoria, al tener que mantener múltiples versiones de los mismos ítems. 
	- Cuando ocurren confictos de tipo WW entre transacciones, obliga a deshacer una de ellas.
- Cuando dos transacciones intentan modificar un mismo ítem de datos, generalmente gana aquella que hace primero su commit, mientras que la otra deberá ser abortada (first-committer-wins).
- Esto por sí solo no alcanza para garantizar la serializabilidad. Debe combinarse con dos elementos más: 
	- Validación permanente con el grafo de precedencias buscando ciclos de conflictos RW. 
	- Locks de predicados en el proceso de detección de conflictos, para detectar precedencias.
- No pueden ocurrir anomalías del fantasma, porque la transacción ve la misma snapshot a lo largo de su vida.

