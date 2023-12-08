# Regla de REDO

Antes de realizar el commit, todo nuevo valor $v$ asignado por la transacción debe ser salvaguardado en el log, en disco.

# Procedimiento

- Cuando una transacción $T_i$ modifica el ítem $X$ remplazando un valor $v_{old}$ por $v$, se escribe $(WRITE, T_i , X, v)$ en el log. 
- Cuando $T_i$ hace commit, se escribe $(COMMIT, T_i)$ en el log y se hace flush del log a disco ([[Log#FLC|FLC]]). Recién entonces se escribe el nuevo valor en disco. 

## Observaciones

- En el punto 1, ahora se escribe el valor nuevo en el log! 
- Si la transacción falla antes del commit, no será necesario deshacer nada (al reiniciar se abortarán las transacciones no commiteadas). Si en cambio falla después de haber escrito el COMMIT en disco, la transacción será rehecha al iniciar.
- Se considera que la transacción commiteó cuando el registro $(COMMIT, T_i)$ queda escrito en el log, en disco.
- En el algoritmo REDO, una transacción puede commitear sin haber guardado en disco todos sus ítems modificados. 

# Reinicio

- Cuando el sistema reinicia se siguen los siguientes pasos: 
	- Se analiza cuáles son las transacciones de las que está registrado el $COMMIT$. 
	- Se recorre el log de atrás hacia adelante volviendo a aplicar cada uno de los $WRITE$ de las transacciones que commitearon, para asegurar que quede actualizado el valor de cada ítem. 
	- Luego, por cada transacción de la que no se encontró el $COMMIT$ se escribe $(ABORT, T)$ en el log y se hace flush del log a disco.

# Checkpoint Activo

- El [[Log#Checkpoints Activos|checkpoint activo]] del algoritmo REDO.
- El **procedimiento** es el siguiente:
	- Escribir un registro $(BEGIN\ CKPT, t_{act})$ con el listado de todas las transacciones activas hasta el momento y volcar el log a disco. 
	- Hacer el volcado a disco de todos los ítems que hayan sido modificados por transacciones que ya commitearon. 
	- Escribir $(END\ CKPT)$ en el log y volcarlo a disco.
- En la **recuperación** hay dos situaciones:
	- Que encontremos primero un registro $(END\ CKPT)$. En ese caso, deberemos retroceder hasta el $(BEGIN , T_x )$ más antiguo del listado que figure en el $(BEGIN\ CKPT)$ para rehacer todas las transacciones que commitearon. Escribir $(ABORT, T_y )$ para aquellas que no hayan commiteado. 
	- Que encontremos primero un registro $(BEGIN\ CKPT)$. Si el checkpoint llego sólo hasta este punto no nos sirve, y entonces deberemos ir a buscar un checkpoint anterior en el log.