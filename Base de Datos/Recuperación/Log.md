- Para hacer posible la [[Recuperación|recuperación]] antes fallas, el [[Sistemas de gestión de bases de datos|SGBD]] guarda una serie de información en un log (bitácora).
- El log almacena generalmente los siguientes registros:
	- $(BEGIN, T_{id})$: Indica que la transacción $T_{id}$ comenzó.  
	- $(WRITE, T_{id}, X, x_{old}, x_{new})$:  Indica que la transacción $T_{id}$ escribió el ítem $X$, cambiando su viejo valor $X_{old}$ por $x_{new}$.
	- $(READ, T_{id}, X)$:  Indica que la transacción $T_{id}$ leyó el ítem $X$.
	- $(COMMIT, T_{id})$:   Indica que la transacción $T_{id}$ commiteó.
	- $(ABORT, T_{id})$:  Indica que la transacción $T_{id}$ abortó.
- La información que se guarda puede varias dependiendo del algoritmo de recuperación utilizado.

# Reglas

El gestor de logs se guía por dos relgas básicas

## WAL

- WAL $\to$ Write Ahead Log
- Indica que antes de guardar un ítem modificado en disco, se debe escribir el registro de log correspondiente en disco.

## FLC

- FLC $\to$ Force Log at Commit.
- Indica que antes de realizar el commit el log debe ser volcado a disco.

# Checkpoints

- Puntos de control.
- Se usa para evitar retroceder más de lo debido en el archivo de log al ejecutar alguno de los algoritmos de recuperación después de un reinicio.
- Es un registro especial en el archivo de log que indica que todos los ítems modificados hasta ese punto han sido almacenados en disco.
- La presencia de un checkpoint en el log implica que todas las transacciones cuyo registro de commit aparece con anterioridad tienen todos sus ítems guardados en forma persistente, y por lo tanto ya no deberán ser deshechas ni rehechas.

## Checkpoints Inactivos

- Tienen un único tipo de registro , **CKPT**.
- La creación de un checkpoint inactivo en el log implica la suspensión momentánea de todas las transacciones para hacer el volcado (flush) de todos los buffers en memoria al disco.

## Checkpoints Activos

- Utiliza dos tipos de registros de checkpoint: $(BEGIN\ CKPT, t_{act})$ y $(END\ CKPT)$, en donde *tact* es un listado de todas las transacciones que se encuentran activas (es decir, que aún no hicieron commit). El procedimiento varía según cada algoritmo de recuperación.

