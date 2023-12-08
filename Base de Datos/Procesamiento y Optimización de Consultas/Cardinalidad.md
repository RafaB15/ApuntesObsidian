- Es parte de la estimación del costo de una consulta.
- Es la estimación del tamaño de las relaciones intermedias que se vana calcular en una consulta.
- Se espera que una estimación de cardinalidad cumpla con los siguientes requisitos: 
	- Sea precisa. 
	- Sea fácil de calcular. 
	- No dependa de la forma en que esa relación intermedia se calculó.

# Proyección

- **Ejemplo**: Persona(DNI, nombre, f_nacimiento, género  ) 
	- 40 millones de tuplas 
	- El DNI es un entero de 4 bytes 
	- El nombre es un string variable de tamaño promedio 15 bytes 
	- La fecha de nacimiento es un timestamp de 4 bytes 
	- El género es un caracter 
- Supongamos que los bloques son de 1024 bytes con un header de 24 bytes. 
- La estimación de la cantidad de bloques que ocupa la relación es: $$B(Persona) = \frac{40 \cdot 10^6 \cdot (4 + 15 + 4 + 1)}{10^3} = 960000$$
- *Se pone mil en vez de 1024 por aproximación*
- Ahora queremos estimar $B(\pi_{DNI}(Persona))$. La cantidad de tuplas no se modifica, por lo tanto: $$B(\pi_{DNI}(Persona)) = \frac{40 \cdot 10^6 \cdot (4)}{10^3} = 160000$$
- El DNI tiene 4 bytes.
# Selección

- La selección reduce el número de tuplas en el resultado, aunque mantiene el tamaño de cada tupla. 
- Para estimar el tamaño de una selección de la forma $\sigma_{A_i=c}(R)$, utilizaremos la variabilidad de $A_i$ en $R (V(A_i , R))$, que es la cantidad de valores distintos que puede tomar el atributo $A_i$ en dicha relación. 
- Realizaremos la siguiente estimación: $$n(\sigma {A_i=c}(R)) = \frac{n(R)}{V(A_i , R)}$$ La fracción $\frac{1}{V(A_i ,R)}$ se denomina selectividad de $A_i$ en $R$.