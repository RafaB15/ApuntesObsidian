- Decimos que una relación está en tercera forma normal (3FN) cuando no existen [[Base de Datos/Diseño Relacional/Dependencia Funcional#Transitiva|dependencias transitivas]] $CK_i \to Y$ de atributos no primos (i.e. $Y \not \subset \bigcup_i CK_i$), con $CK_i$ clave candidata.
- Una definición equivalente es que para toda dependencia funcional no trivial $X \to Y$, o bien *X* es superclave, o bien *Y - X* contiene sólo atributos primos.
- Por lo tanto, si en una tabla tenemos una dependencia funcional entre atributos no primos, pero alguno de estos depende funcionalmente de una clave candidata, entonces no estamos en 3FN al haber una dependencia transitiva.
- Para normalizar en la tercera forma normal haremos lo siguiente, si es que tenemos una dependencia de atributos no primos de la forma $A \to B$.
	1. Hacemos una nueva tabla en donde tendremos como atributos a *A* y a *B*, siendo *A* la llave primaria. 
	2. Sacamos a *B* de la table original y *A* es ahora una llave foránea.

# Algoritmo de descomposición a 3FN

**Input:** Una relación universal *R* y un conjunto de [[Base de Datos/Diseño Relacional/Dependencia Funcional|dependencias funcionales]] *F*.

**Output**: Una [[Base de Datos/Diseño Relacional/Descomposición|descomposición]] de *R*, $D = (R_1, R_2, \dots, R_n)$ que preserva la información y las dependencias funcionales, y está en 3FN.

![[Base de Datos/Diseño Relacional/images/Algoritmo 3FN.png]] 
- En este algoritmo se garantiza la preservación de todas las dependencias funcionales en la [[Base de Datos/Diseño Relacional/Descomposición|descomposición]].