- Costos calculados con la [[Información de Catálogo]]. 

# Unión e intersección

- Primero ordenamos las tablas *R* y *S*. 
	- Si alguna no entra en memoria, usamos sort externo.
- Asumimos que no se devuelven repetidos (comportamiento default en [[SQL]]). 
	- Se puede modificar sencillamente en caso de querer repetidos. 
- Procesaremos ambas tablas ordenadas haciendo un **merge** que avanza por las filas $r_i$ y $s_j$ ordenadas de cada tabla. 
- El costo es: $$cost(R\ [\cup|\cap|-]\ S) = cost(Ord_M(R)) + cost(Ord_M(S)) + 2.B(R) + 2.B(S)$$
- Para la **unión** ($\cup$), debemos devolver todas las filas: 
1.  Si $r_i = s_j$ devolver una de ellas y avanzar sobre ambas tablas hasta que cambien de valor. 
2. Sino, devolver la menor y avanzar sobre su tabla hasta que cambie de valor. 
3. Cuando alguna tabla se termine, devolver todo lo que queda de la otra, sin duplicados.

- Para la **intersección** ($\cap$), devolver las tuplas que están en ambas relaciones: 
1. Si $r_i \not= s_j$ avanzar sobre la tabla de la menor de ellas un lugar, sin devolver nada. 
2. Si $r_i = s_j$ devolver una de ellas y avanzar sobre ambas tablas hasta que cambien de valor. 
3. Cuando alguna tabla se termine, finalizar.

- Para la **diferencia** ($-$), devolver las tuplas que están en *R* pero no en *S*:
1. Si $r_1 > s_j$ avanzar sobre la tabla *S* hasta que cambie de valor.
2. Si $r_i < s_i$ devolver $r_i$ y avanzar sobre la tabla *R* hasta que cambie de valor.
3. Si $r_1 = s_j$ avanzar sobre ambas tablas hasta que cambien de valor.
4. Cuando *R* se termine, finalizar. Cuando *S* se termine, devolver todo lo que queda de *R*, sin duplicados.