- Son bases de datos [[No SQL]].
- Las bases de datos clave-valor (key-value stores) almacenan vectores asociativos ó diccionarios, es decir conjuntos formados por pares de elementos de forma (clave, valor).
- Las claves son únicas (es decir, no puede haber dos pares que posean la misma clave), y el único requisito sobre su dominio es que sea comparable por igual (=).

# Operaciones Elementales

- Insertar un nuevo par (put)
- Eliminar un par existente (delete)
- Actualizar el valor de un par (update)
- Encontrar un par asociado a una clave particular (get)
# Ventajas

- Simplicidad 
	- No se define un [[Esquema de Base de Datos|esquema]].
	- No hay [[Lenguajes para BDD#Lenguajes de definición de datos|DDL's]], restricciones de integridad, ni dominios.
	- El [[Agregado|agregado]] es mínimo, y está limitado al par. 
	- El objetivo es guardar y consultar grandes cantidades de datos, pero no de interrelaciones entre los datos. 
- Velocidad 
	- Ya que se prioriza la eficiencia de acceso por sobre la integridad de los datos. 
- Escalabilidad 
	- Generalmente proveen replicación (ya sea maestro-esclavo ó distribuida) y permiten repartir las consultas entre los nodos.