# Regla de Undo

Antes de que una modificación sobre un ítem $X \leftarrow v_{new}$ por parte de una transacción no commiteada sea guardada en disco (flushed), se debe salvaguardar en el log en disco el último valor commiteado $v_{old}$ de ese ítem.

# Procedimiento

- Cuando una transacción $T_i$ modifica el ítem $X$ remplazando un valor $v_{old}$ por $v$, se escribe $(WRITE, T_i , X, v_{old})$ en el log, y se hace flush del log a disco.
- El registro $(WRITE, Ti , X, v_{old})$ debe ser escrito en el log en disco (flushed) antes de escribir (flush) el nuevo valor de $X$ en disco ([[Log#WAL|WAL]]).
- Todo ítem modificado debe ser guardado en disco antes de hacer commit. 
- Cuando $T_i$ hace commit, se escribe $(COMMIT, T_i)$ en el log y se hace flush del log a disco ([[Log#FLC|FLC]]).

## Observaciones

- Los tres primeros puntos aseguran que todas las modificaciones realizadas sean escritas a disco antes de que la transacción termine. 
- De esta forma, una vez cumplimentado el paso 4, ya nunca será necesario hacer REDO. Si la transacción falla antes ó durante el punto 4, será deshecha (UNDO) al reiniciar.
- Se considera que la transacción commiteó cuando el registro $(COMMIT, T_i)$ queda escrito en el log, en disco.

# Reinicio

- Cuando el sistema reinicia se siguen los siguientes pasos: 
	- Se recorre el log de adelante hacia atrás, y por cada transacción de la que no se encuentra el $COMMIT$ se aplica cada uno de los $WRITE$ para restaurar el valor anterior a la misma en disco. 
	- Luego, por cada transacción de la que no se encontró el $COMMIT$ se escribe $(ABORT, T)$ en el log y se hace flush del log a disco.

# Checkpoint Activo

- El [[Log#Checkpoints Activos|checkpoint activo]] del algoritmo UNDO.
- El **procedimiento** es el siguiente:
	- Escribir un registro $(BEGIN\ CKPT, t_{act})$ con el listado de todas las transacciones activas hasta el momento.
	- Esperar a que todas esas transacciones activas hagan su commit (sin dejar por eso de recibir nuevas transacciones) 
	- Escribir $(END\ CKPT)$ en el log y volcarlo a disco.
- En la **recuperación**, al hacer el rollback se dan dos situaciones:
	- Que encontremos primero un registro $(END\ CKPT)$. En ese caso, sólo debemos retroceder hasta el $(BEGIN\ CKPT)$ durante el rollback, porque ninguna transacción incompleta puede haber comenzado antes). 
	- Que encontremos primero un registro $(BEGIN\ CKPT)$. Esto implica que el sistema cayó sin asegurar los commits del listado de transacciones. Deberemos volver hacia atrás, pero sólo hasta el inicio de la más antigua del listado.