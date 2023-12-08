- Decimos que una [[Base de Datos/Modelo Lógico Relacional/Modelo Relacional#Relación|relación]] está en segunda forma normal (2FN) cuando todos sus atributos no [[Base de Datos/Modelo Conceptual de BDD/Atributos#Atributo primo|primos]] tienen [[Base de Datos/Diseño Relacional/Dependencia Funcional#Total|dependencia funcional completa]] de las claves candidatas.

- Identificamos [[Base de Datos/Diseño Relacional/Dependencia Funcional|dependencias funcionales]] semánticas, basándonos en lo que sabemos de los datos.
- Una vez que las tenemos identificadas, si tenemos 5 atributos *A, B, C, D* y *E*, siendo *A* y *B* una clave candidata y *B* y *C* otra, si:

$$\{A, B\} \to D$$
	eso está en 2FN debido a que D tiene una dependencia completa con una clave candidata.
	Pero si
$$C \to E$$
	entonces es cierto que
	$$\{C, D\} \to E$$
	Entonces *E* tiene una dependencia parcial a una llave candidata, con lo que ya no se cumple 2FN.
	Esto significa que para diferentes combinaciones de *C* y *D*, se van a repetir muchas veces los valores de *E* para el mismo valor de *C* y distinto *D*, lo cual queremos evitar.
- Lo que hacemos para solventar esto y normalizar la relación, de manera de quedar en 2FN, es:
	1. Creamos una nueva tabla con *C* y *E* como atributos, siendo *C* la llave primaria.
	2. En la tabla original, quitamos el atributo *E* y dejamos el de *C*, el cual es ahora una llave foránea.

- Las dependencias funcionales de la tabla original se van a repartir entre las dos tablas resultantes de la normalización.