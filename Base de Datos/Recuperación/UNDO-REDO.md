
En el algoritmo UNOD/REDO es necesario cumplir con las reglas de [[UNDO|UNDO]] y [[REDO|REDO]] al mismo tiempo.

# Procedimiento

- Cuando una transacción $Ti$ modifica el item $X$ remplazando un valor $v_{old}$ por $v$, se escribe $(WRITE, T_i , X, v_{old} , v)$ en el log. 
- El registro $(WRITE, T_i , X, v_{old} , v)$ debe ser escrito en el log en disco (flushed) antes de escribir (flush) el nuevo valor de $X$ en disco.
- Cuando $T_i$ hace commit, se escribe $(COMMIT, T_i)$ en el log y se hace flush del log a disco.
- Los ítems modificados pueden ser guardados en disco antes o después de hacer commit.

# Reinicio

- Cuando el sistema reinicia se siguen los siguientes pasos: 
	- Se recorre el log de adelante hacia atrás, y por cada transacción de la que no se encuentra el $COMMIT$ se aplica cada uno de los $WRITE$ para restaurar el valor anterior a la misma en disco. 
	- Luego se recorre de atrás hacia adelante volviendo a aplicar cada uno de los $WRITE$ de las transacciones que commitearon, para asegurar que quede asignado el nuevo valor de cada ítem.
	- Finalmente, por cada transacción de la que no se encontró el $COMMIT$ se escribe $(ABORT, T)$ en el log y se hace flush del log a disco.

# Checkpoint Activo

- El [[Log#Checkpoints Activos|checkpoint activo]] del algoritmo UNDO/REDO.
- El **procedimiento** es el siguiente:
	- Escribir un registro $(BEGIN\ CKPT, t_{act})$ con el listado de todas las transacciones activas hasta el momento y volcar el log a disco. 
	- Hacer el volcado a disco de todos los ítems que hayan sido modificados antes del $(BEGIN\ CKPT)$. 
	- Escribir $(END\ CKPT)$ en el log y volcarlo a disco.
- En la **recuperación** es posible que debamos retroceder hasta el inicio de la transacción más antigua en el listado de transacciones, para deshacerla en caso de que no haya commiteado, o para rehacer sus operaciones posteriores al $BEGIN\ CKPT$, en caso de que haya commiteado.