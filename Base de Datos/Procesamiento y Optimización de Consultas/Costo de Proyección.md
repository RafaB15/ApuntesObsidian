- Costos calculados con la [[Información de Catálogo]]. 
- Teniendo una proyección del tipo $\pi_{X}(R)$, tenemos dos casos:
	- X **es** superclave.
		- No es necesario eliminar duplicados $$cost(\pi_{X}(R)) = B(R)$$
	-  X **no es** superclave.
		- Debemos eliminar duplicados. Llamaremos $\hat \pi_X(R)$ a la proyección de multisets (sin eliminar duplicados). Podemos:
		1. **Ordenar** la tabla: Si $B(\hat \pi_X)(R)) \le M$ podemos ordenar en memoria. De lo contrario, el costo usando sort externo será: $$cost(\pi_X(R)) = cost(Ord_M(R)) = 2.B(R).[\log_{M-1}(B(R))] - B(R)$$
		2. Utilizar una estructura de **hash**: Si $B(\hat \pi_X)(R)) \le M$ también podemos hacer el hashing en memoria, con costo $B(R)$. Utilizando hashing externo el costo es de $B(R) + 2.B(\hat \pi_X)(R))$ .

- Tener en cuenta que si la consulta [[SQL]] no incluye **DISTINCT**, entonces el resultado es un multiset y no hay que eliminar duplicado, por lo que el costo es siempre $B(R)$.