- Costos calculados con la [[Información de Catálogo]]. 
- Partimos de una selección básica del tipo $\sigma_{cond}(R)$, en donde *cond* es una condición atómica del tipo: 
	- $A_i \odot c$, con $c \in dom(A_i)$, en donde $\odot$ es un operador de comparación.
- Existen distintas estrategias de búsqueda, según los recursos con los que contamos.
- Analizaremos distintas situaciones para la comparación por =
# File Scan vs Index Scan

## File Scan

- Sus métodos recorren el/los archivo/s en busca de los registros que cumplen con la condición.

### Búsqueda lineal

- Consiste en explorar cada registro, analizando si se verifica la condición.
$$cost(S_1) = B(R)$$

## Index Scan

- Sus métodos utilizan un índice de búsqueda.

### Búsqueda con índice primario

- Cuando $A_i$ es un atributo clave del que se tiene un [[Índices|índice primario]]. 
	- Solo una tupla puede satisfacer la condición (si es que la consulta compara por =).
	- Si utilizamos un árbol de búsqueda:
	$$cost(S_{3a}) = Height(I(A_i, R)) + 1$$
	- Si utilizamos una clave de hash:
	$$cost(S_{3b}) = 1$$
- El $+ 1$ es porque por cada nivel de altura en el árbol accedemos a memoria, y luego cuando encontramos el puntero en la hoja tenemos que también acceder a este.
### Búsqueda con índice clustering

- Cuando $A_i$ no es clave pero se tiene un índice de ordenamiento (clustering) por él.
	- Las tuplas se encuentran contiguas en los bloques, los cuales estarán disjuntos.
	 $$cost(S_5) = Height(I(A_i, R)) + \frac{n(R)}{V(A_i,R) . F(R)}$$
### Búsqueda con índice secundario

- Cuando $A_i$ no tiene un índice de clustering, pero existe un índice secundario asociado a él.
 $$cost(S_6) = Height(I(A_i, R)) + \frac{n(R)}{V(A_i,R)}$$

- Aunque los cálculos vistos se hicieran con el operador = en mente, se pueden extender para el resto de operadores.

# Selecciones complejas

- Si la selección involucra la **conjunción** de varias condiciones simples, pueden adoptarse distintas estrategias:
	- Si uno de los atributos tiene un [[Índices|índice]] asociado, se aplica primero esta condición, y luego se selecciona del resultado a aquellas tuplas que cumplen con las demás condiciones.
	- Si hay un índice compuesto que involucra a atributos de más de una condición, se utiliza este índice y luego se seleccionan las tuplas que cumplen los demás criterios. 
	- Si hay índices simples para varios atributos, se utilizan los índices por separado y luego se intersecan los resultados. 
- Si la selección involucra una **disyunción** de condiciones simples, debemos aplicar las mismas por separado y luego unir los resultados. 
	- Si uno de los atributos no dispone de índice, hay que usar fuerza bruta.