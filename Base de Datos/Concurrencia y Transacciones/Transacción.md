- Es una unidad lógica de trabajo en los [[Sistemas de gestión de bases de datos|SGBD]].
- Es una secuencia ordenada de instrucciones que deben ser ejecutadas en su totalidad o bien no ser ejecutadas, al margen de la interferencia con otras transacciones simultáneas. En otras palabras, deben ser **instrucciones atómicas**.
- Una misma transacción puede realizar varias operaciones de consulta/ABM durante su ejecución.
- Antes de existir el [[Concurrencia|multitasking]], las transacciones se serializaban. Hasta tanto no se terminara una, no se iniciaba la siguiente.
- Las instrucciones atómicas básicas de una transacción sobre la base de datos serán: 
	- `leer_item(X)`: Lee el valor del ítem X, cargándolo en una variable en memoria 
	- `escribir_item(X)`: Ordena escribir el valor que está en memoria del ítem X en la base de datos 

# Notación

- $R_T(X)$: La transacción *T* lee el ítem *X*.
- $W_T(X)$: La transacción *T* escribe el ítem *X*.
- $b_t$: Comienzo de la transacción *T*.
- $c_t$: La transacción *T* realiza el commit.
- $a_T$: Se aborta la transacción *T* (*abort*).

Escribimos una transacción general *T* como una lista de instrucciones $\{I_T^{1}, I_T^{2}, \dots, I_T^{m(T)}\}$, siendo $m(T)$ la cantidad de instrucciones de *T*.

# Propiedades ACID

## Atomicidad

**Desde el punto de vista del usuario**, las transacciones deben ejecutarse de manera atómica. Esto quiere decir que, o bien la transacción se realiza por completo, o bien no se realiza.

## Consistencia

Cada ejecución, por sí misma, debe preservar la consistencia de los datos. La consistencia se define a través de reglas de integridad: condiciones que deben verificarse sobre los datos en todo momento.
## Aislamiento

El resultado de la ejecución concurrente de las transacciones debe ser el mismo que si las transacciones se ejecutaran en forma aislada una tras otra, es decir en forma serial. La ejecución concurrente debe entonces ser equivalente a **alguna** ejecución serial.

Ver [[Serializabilidad|serializabilidad]].

## Durabilidad

Una vez que el [[Sistemas de gestión de bases de datos|SGBD]] informa que la transacción se ha completado, debe garantizarse la persistencia de la misma, independientemente de toda falla que pueda ocurrir.

# Recuperación

- Para garantizar las propiedades ACID, los [[Sistemas de gestión de bases de datos|SGBD]] disponen de mecanismos de recuperación que permiten deshacer/rehacer una transacción en caso de que se produzca un error o falla.
- Para ello es necesario agregar a la secuencia de instrucciones de cada transacción algunas instrucciones especiales:
	- **begin**: Indica el comienzo de la transacción.
	- **commit**: Indica que la transacción ha terminado exitosamente, y se espera que su resultado haya sido efectivamente almacenado en forma persistente.
	- **abort**: Indica que se produjo algún error o falla, y que por lo tanto todos los efectos de la transacción deben ser deshechos (rolled back).


