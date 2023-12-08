- El lenguaje SQL (Structured Query Language) es hoy en día el estándar para la operación de bases de datos relacionales. 
- Es tanto un [[Base de Datos/Structured Query Language/Lenguajes para BDD#Lenguajes de definición de datos|lenguaje de definición de datos (DDL)]] como de [[Base de Datos/Structured Query Language/Lenguajes para BDD#Lenguajes de manipulación de datos|manipulación de datos (DML)]]. 
- Como lenguaje de manipulación de datos, SQL: 
	- Es no procedural. 
	- Está basado en el cálculo relacional de tuplas.
- Del modelo relacional a SQL podemos pensar que cambian estas cosas:

| Modelo Relacional | SQL |
| - | - |
| Relación | Tabla |
| Tupla | Fila |
| Atributo | Columna |

# Definición de Datos (DDL)

## Esquema

Un esquema (schema en inglés) dentro de una base de datos es un conjunto de tablas dentro de un [[Base de Datos/Introducción/Sistemas de gestión de bases de datos|SGBD]].

## Catálogo

En un entorno SQL pueden haber varios esquemas de bases de datos. 
Un catálogo es una colección de esquemas.

Todo catálogo contiene un esquema llamado **INFORMATION_SCHEMA**, que describe a todos los demás esquemas contenidos en él.

## Crear un esquema en SQL

- El comando **CREATE SCHEMA** nos permite crear un nuevo esquema de base de datos dentro de nuestro SGBD.
```SQL
CREATE SCHEMA nombre_esquema {AUTHORIZATION AuthId};
```

Ejemplo:

```SQL
CREATE SCHEMA empresa { AUTHORIZATION Rafita};
```

- La opción **AUTHORIZATION** identifica quién será el dueño del esquema.

## Tipos de Variables en SQL

### Tipos Numéricos Estándar

- **INTEGER**: Tipo entero. Abreviado INT. 
- **SMALLINT**: Tipo entero pequeño. 
- **FLOAT(n)**: Tipo numérico aproximado. n indica la precisión en bits. 
- **DOUBLE PRECISION**: Tipo numérico aproximado de alta precisión. 
- **NUMERIC(i,j)**: Tipo numérico exacto. Permite especificar la precisión (i) y la escala (j) en dígitos.
### Strings

Se delimitan con comillas simples (').
- **CHARACTER(n)**: De longitud fija. Abreviado CHAR(n). 
- **CHARACTER VARYING(n)**: De longitud variable. Abrev. VARCHAR(n).
### Fecha y hora 
- **DATE**: Precisión de días. Se ingresa como string con formato YYYY-MM-DD.
- TIME(i): Precisión de hasta microsegundos. Se ingresa como string con formato HH:MM:SS.$[0-9]^i$ (ISO 8601). Tantos dígitos decimales como i. 
- TIMESTAMP(i): Combina un **DATE** y un **TIME(i)**.

### Booleanos:
- **BOOLEAN**: TRUE, FALSE o UNKNOWN. Se emplea lógica de tres valores.

### Otros tipos:
- **CLOB**: (Character Large Object) Para documentos de texto de gran extensión. 
- **BLOB**: (Binary Large Object) Para archivos binarios de gran extensión

### Definir tipos

```SQL
CREATE DOMAIN NOMBRE_DOMINIO AS TIPO_BASICO;
```

## Crear una tabla

El comando **CREATE TABLE** nos permite definir la estructura de una tabla:
```SQL
CREATE TABLE Persona ( 
dni_persona INT PRIMARY KEY, 
nombre_persona VARCHAR(255) , 
fecha_nacimiento DATE);
```

```SQL
CREATE TABLE HijoDe ( 
dni_hijo INT, 
dni_padre INT, 
PRIMARY KEY (dni_hijo , dni_padre ), 
FOREIGN KEY (dni_hijo) REFERENCES Persona( dni_persona ), 
FOREIGN KEY ( dni_padre ) REFERENCES Persona( dni_persona ));
```

A las foreign keys también les podemos agregar un parámetro **ON DELEATE** o uno **ON UPDATE** para especificar qué sucede si se borra el valor que se está referenciando de la tabla en el que está siendo referenciado.
### Restricciones de dominio

También podemos restringir los tipos de datos aceptados como

```SQL
fecha_nac DATE NOT NULL,
CUIT_tipo INT CHECK ( CUIT_tipo =20) OR ( CUIT_tipo =23),
```

### Restricciones de unicidad

- Indicamos una llave primaria con **PRIMARY KEY**. Si está compuesta por más de una columna entonces lo hacemos en una línea aparte.
- Si usamos la palabra clave **UNIQUE** entonces en esa columna no podrán haber valores iguales en filas distintas.
### Restricciones de integridad

- **Integridad de entidad**: La clave primario de una talba nunca debería ser NULL.
- **Integridad referencial:** Las claves foráneas se especifican con **FOREIGN KEY... REFERENCES**

En SQL se permite que una fila esté repetida muchas veces en una tabla si así se quiere. Este concepto se conoce como multiset o bag of tuples.

# Manipulación de Datos (DML)

## Select From Where

- El esquema básico de una consulta en SQL es:
```SQL
SELECT A1, A2, ..., An
FROM T1, T2, ..., Tm
[WHERE CONDITION];
```
- En donde las A son columnas y las T son tablas.
- La proyección en SQL no elimina filas repetidas.
- Las condiciones atómicas admitidas dentro de la cláusula **WHERE** son:
	- $A_i \odot A_j$ 
	- $A_i \odot c$, con $c \in dom(A_i)$ 
	- $A_i$ \[NOT] LIKE p, en donde $A_i$ es un string y p es un patrón.
	- $(A_i, A_{i+1}, \dots)$ \[NOT] IN m, en donde m es un set o un multiset.
	- $A_i$ \[NOT] BETWEEN a AND b, con $a,b \in dom(A_i)$ 
	- $A_i$ is \[NOT] NULL.
	- EXISTS *t*, en donde *t* es una tabla.
	- $A_i \odot$ \[ANY|ALL] *t*, en donde *t* es una tabla
- En donde $\odot$ debe ser un operador de comparación
	- $=, \ne$
	- $>,\ge , <, \le$ (para atributos con dominios ordenados)
- Varias condiciones atómicas pueden unirse a través de operadores lógicos como **AND, OR** y **NOT**.
- Se puede usar WHERE para reconocer patrones en columnas que son strings con la palabra LIKE.
	- Se acepta como patrón una secuencia de caracteres delimitada por comillas simples combinada con caracteres especiales
		- _ (representa un caracter arbitrario)
		- % (representa cero o más caracteres arbitrarios)
		- Si se necesita un _ o un % literal en el patrón, es debe escapear.

## Alias

En la clausula FROM es posible indicar un alias para las tablas
```SQL
...FROM Persona p... 
...FROM Persona AS p...
```

```SQL
..FROM Persona AS p1(dni1 , nombre1), Personas AS p2(dni2 , nombre2 )..
```

También las columnas en el resultado

```SQL
SELECT p1.nombre AS NPadre , p2.nombre AS NHijo ...
```

```SQL
SELECT Producto.precio * 0.90 AS precioDescontado ...
```

Las operaciones permitidas son:
- +, - ,\*, / (columnas numéricas)
- || (concatenación de strings)
- +, - (sumar a una fecha, hora o timestamp un intervalo)
- LN, EXP, POWER, LOG, SQRT, FLOOR, CEIL, ABS, (no son core SQL)

## Funciones de Agregación

- Podemos aplicar una función de agregación a cada una de las columnas del resultado. Las más habituales son: 
	- **SUM(A)** Suma los valores de la columna A de todas las filas 
	- **COUNT(\[DISTINCT] A | \*)** 
		- **COUNT(A)**: cuenta la cantidad de filas con valor no nulo de A. 
		- **COUNT(DISTINCT A)**: cuenta la cantidad de valores distintos de A, sin contar el valor nulo. 
		- **COUNT(\*)**: cuenta la cantidad de filas en el resultado. 
	- **AVG(A)**: Calcula el promedio de los valores de A, descartando los valores nulos. 
	- **MAX(A)**: Sólo para dominios ordenados. 
	- **MIN(A)**: Sólo para dominios ordenados. 
- En este caso, el resultado colapsa a una única fila.
- La palabra clave **DISTINCT** después de la cláusula **SELECT** elimina los duplicados en el resultado.
## JOIN

Se implementan las operaciones de Junta a través del Join.
- Junta Theta $\bowtie$ 
```SQL
...FROM R INNER JOIN S ON condition ... 
...FROM R INNER JOIN S USING( attribute )...
```
- Junta natural (\*)
```SQL
...FROM R NATURAL JOIN S...
```
Los nombres de las columnas de junta deben coincidir en ambas talbas.
- Junta externa 
```SQL
...FROM R LEFT OUTER JOIN S ON condition ... 
...FROM R RIGHT OUTER JOIN S ON condition ... 
...FROM R FULL OUTER JOIN S ON condition ...
```

Ejemplo:

```SQL
SELECT DISTINCT p.Id , p.Title , p. ViewCount 
FROM ((( Tags t1 INNER JOIN PostTags pt1 ON t1.Id=TagId) 
	   INNER JOIN Posts p ON pt1.PostId=p.Id) 
	   INNER JOIN PostTags pt2 ON p.Id=pt2.PostId) 
	   INNER JOIN Tags t2 ON pt2.TagId=t2.Id 
WHERE t1.TagName=’relational’ 
AND t2.TagName=’entity−relationship’;
```
## Operaciones de conjuntos

```SQL
... R UNION [ALL] S ...
... R INTERSECT [ALL] S ...
... R EXCEPT [ALL] S...
```
- Las tablas R y S pueden venir de subconsultas.
- R y S deben ser union compatibles.
- Si no se agrega la palabra clave ALL, el resultado será un set en vez de un multiset y entonces no habrá filas repetidas.
## Ordenamiento y paginación

Para ordenar las columnas seleccionadas usamos

```SQL
SELECT A1, A2, ..., An 
FROM T1, T2, ..., Tm 
[ WHERE condition ]
[ ORDER BY Ak1 [ ASC | DESC ], Ak2 [ ASC | DESC ], ...];
```

También, si queremos obtener solo una porción de las filas podemos usar la paginación, que es la posibilidad de escoger un rango $[t_{inicio}, t_{fin}]$ del listado de filas del resultado
Se hace de la forma:

```SQL
SELECT Title , CreationDate , ViewCount 
FROM Posts 
WHERE CreationDate >=’2017−01−01’ 
AND ParentId IS NULL 
ORDER BY ViewCount DESC 
OFFSET 0 ROWS FETCH FIRST 10 ROWS ONLY;
```

En postgress podemos hacer

```SQL
SELECT padron, codigo, numero, fecha, nota * 10 as nota
FROM notas 
LIMIT 5 OFFSET 5
```

## GROUP BY ... HAVING

Seleccionamos las columnas, algunas con funciones de agregación. Luego agrupamos por las columnas que queramos que no tenga funciones de agregación y podemos usar having para poner condiciones.
```SQL
SELECT nombre_tenista , COUNT( nombre_torneo ), SUM(premio) 
FROM Campeones 
GROUP BY nombre_tenista ;
```

```SQL
SELECT Ak1 , Ak2 , ..., f1(B1), f2(B2), ..., fp(Bp) 
FROM T1, T2, ..., Tm 
[ WHERE condition1 ] 
GROUP BY A1, A2, ..., An 
[ HAVING condition2 ] 
[ ORDER BY Ak1 [ ASC | DESC ], Ak2 [ ASC | DESC ], ...];
```

- A1, A2, ..., An son las columnas de agrupamiento, y algunas de ellas participan de la selección final. B1, B2, ..., Bp no son columnas de agrupamiento, pero participan de la selección final a través de las funciones de agregación anteriormente mencionadas.
- La cláusula HAVING es opcional, y nos permite seleccionar sólo algunos de los grupos del resultado. condition2 es por lo tanto una condición que involucra funciones de agregación sobre las columnas que no son de agrupamiento en el GROUP BY

```SQL
SELECT t.TagName 
FROM Tags t, PostTags pt , Posts p 
WHERE t.Id = pt.TagId 
AND pt.PostId = p.Id 
GROUP BY t.TagName 
HAVING MIN(p. CreationDate )>=’2018−01−01’;
```

## Consultas Anidadas

### Subqueries en la cláusula WHERE

```SQL

SELECT ... FROM ... 
WHERE A IN (SELECT X FROM ...); −− Debe devolver una única columna 

SELECT ... FROM ... 
WHERE A = (SELECT X FROM ...); −− Debe devolver sólo 1 fila! 

SELECT ... FROM ... −− (feature opcional) 
WHERE (A, B) IN (SELECT X, Y FROM ...); −− Debe devolver 2 columnas 

SELECT ... FROM ... 
WHERE A < [ SOME | ALL ] (SELECT X FROM ...); 

SELECT ... FROM ...                       −− Devuelve FALSE/TRUE según 
WHERE [ NOT ] EXISTS (SELECT ... FROM ...); −− la tabla esté vacía o no

```
Podemos poner una subconsulta en cualquier lado en donde SQL espere un solo valor, si hay una fila o columna solamente como resultado de la subconjunta.
## Inserciones

Se puede insertar un listado de n-filas:

```SQL
INSERT INTO T 
VALUES (a11, a12, ..., a1n),(a21, a22, ..., a2n), ...,(ap1, ap2, ..., apn);
```

O insertar de un subset de filas

```SQL
INSERT INTO T(Ai1 , Ai2 , ..., Aik ) 
VALUES (a1i1 , a1i2 , ..., a1ik ),(a2i1 , a2i2 , ..., a2ik ), ...,(api1 , api2 , ..., apik );
```

También podemos insertar una consulta
```SQL
INSERT INTO T(Ai1 , Ai2 , ..., Aik ) SELECT ... FROM ...;
```

Las columnas deben ser union compatibles

- En cualquiera de los casos, una fila no se inserta si:
	- Se asigna a una columna un valor fuera de su dominio. 
	- Se omitió una columna que no podía ser NULL.
	- Se puso en NULL una columna que no podía ser NULL. 
	- La clave primaria asignada ya existe en la tabla.
	- Una clave foránea hace referencia a una clave no existente.
- Las inserciones son a todo o nada. Si no se puede insertar alguna fila, entonces el [[Base de Datos/Introducción/Sistemas de gestión de bases de datos|gestor de base de datos]] va a dejar la tabla como antes de intentar la inserción.

## Eliminaciones

```SQL
DELETE FROM T 
WHERE condition;
```

Si se elimina una fila de una llave primaria que era referenciada como llave foránea en otra tabla, lo que pasará en esa tabla dependerá de las condiciones que fueron impuestas al crearla.
- Si dicha clave foránea se configuró en ON DELETE CASCADE 
	- Se eliminan todas las filas que referencian a ésta, y luego se elimina t. 
- Si en cambio se configuró en ON DELETE SET NULL 
	- Se ponen en NULL todas las claves foráneas de las filas que referencian a ésta, y luego se elimina t. 
- Si se configuró en ON DELETE RESTRICT 
	- No se elimina t.

## Modificaciones
```SQL
UPDATE T 
SET A1 = c1, A2 = c2, ..., Ak = ck 
WHERE condition;
```

## Drop

Una tabla se elimina con DROP TABLE

```SQL
DROP TABLE T [ RESTRICT|CASCADE ];
```

Un esquema se elimina con DROP SCHEMA

```SQL
DROP SCHEMA S [ RESTRICT|CASCADE ];
```

# Funciones y estructuras auxiliares

## Manejo de strings

- SUBSTRING(string FROM start FOR length): Selecciona un substring desde la posición start y de largo length. 
- UPPER(string)/LOWER(string): Convierte el string a mayúsculas/minúsculas. 
- CHAR_LENGTH(string): Devuelve la longitud del string.

## Conversión de tipos

- CAST(attr AS TYPE) permite realizar conversiones entre tipos. 
- EXTRACT(campo FROM attr) permite extraer información de una columna de fecha/hora (feature opcional). 

```SQL
SELECT (EXTRACT(DAY FROM fecha )) AS dia , COUNT( nro_factura ) 
FROM Facturas f; 
GROUP BY dia;
```

   - Valores posibles para el campo: YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, ... 
- COALESCE(expr1, expr2, ..., exprN) devuelve para cada tupla la primera expresión no nula de izquierda a derecha. 
`
```SQL
−−Reemplaza los valores nulos en la columna domicilio 
−−por el string desconocido. 
SELECT apellido , nombre , COALESCE(domicilio , ’’) 
FROM Clientes;
```

## Estructura CASE WHEN ... THEN ... ELSE ... END

La estructura CASE nos permite agregar cierta lógica de la programación estructurada a una sentencia SQL

```SQL
SELECT padrón, apellido , nombre , CASE 
	WHEN primera_op >=4 OR primer_rec >=4 OR segundo_rec >=4 
	THEN ’APROBO_PARCIAL’ 
	ELSE ’DESAPROBO_PARCIAL’ 
	END AS situacion_parcial 
FROM Notas_Parcial ;
```

```SQL
SELECT nro_factura , 
	CAST( 
		CAST(año_venc AS CHAR) || ’−’ || 
		CASE WHEN mes_venc >9 THEN ’’ ELSE ’0’ END || 
		CAST(mes_venc AS VARCHAR)|| ’−’ || 
		CASE WHEN dia_venc >9 THEN ’’ ELSE ’0’ END || 
		CAST(dia_venc AS VARCHAR) 
		AS DATE 
		) AS fecha_venc 
FROM Facturas f;
```

## Clausula WITH 
La cláusula WITH permite construir una tabla auxiliar temporal previa a una consulta. No es Core-SQL.

```SQL
WITH T[(A1, A2, ..., An)] 
AS (<subquery>) 
<query>;
```

```SQL
WITH Jon 
AS (SELECT Id 
	FROM Users 
	WHERE DisplayName =’Jon Skeet’) 
SELECT DISTINCT Name 
FROM Badges b, Jon j 
WHERE b.UserId = j.Id;
```

## WITH Recursivo

Dada una tabla *T* que es input de una consulta, permite que el resultado de la misma, $T_{new} \leftarrow \text{subquery(T)}$, sea utilizado en el lugar de *T* para volver a ejecutar la misma consulta. Esto se repite hasta encontrar un punto fijo en el que $T = \text{subquery(T)}$.

```SQL
WITH RECURSIVE T[(A1, A2, ..., An)] 
AS ( <initial_value_query> 
	UNION <subquery>) 
<query with T>;
```

- La consulta inicial <initial_value_query> no puede depender de T.
- Tanto en WITH como en WITH RECURSIVE puede definirse más de una tabla auxiliar antes de la consulta.
### Ejemplo:

Dada la relación Vuelos(codVuelo, ciudadDesde, ciudadHasta) que indica todos los vuelos que ofrece una aerolínea, encuentre todas las ciudades que son ‘alcanzables’ desde París, independientemente de la cantidad de escalas que sea necesario hacer.

```SQL
WITH RECURSIVE DestinosAlcanzables(ciudad) 
AS (VALUES ('Paris') -- Valor para el único campo de DestinosAlcanzables. Values es palabra clave.
	UNION 
	SELECT v. ciudadHasta AS ciudad 
	FROM DestinosAlcanzables d, Vuelos v 
	WHERE d.ciudad = v. ciudadDesde 
) 
SELECT ciudad FROM DestinosAlcanzables ;
```

- Es como buscar la componente conexa de París en un grafo.

## Funciones de Ventana

- Las funciones de ventana (window functions) permiten aplicar un procesamiento final a los resultados de una consulta, siguiendo estos pasos: 
1.  ... dividiéndolos en grupos, llamados particiones, 
2. ... ordenando internamente cada partición, 
3. ... y cruzando información entre las filas de cada partición. 
- A cada atributo del SELECT de una consulta se le puede aplicar una función de ventana distinta, o bien puede no aplicarsele función alguna.

### Ventanas bajo una única partición

- No se utiliza la palabra clave PARTITION
- Esquema básico
```SQL
SELECT .., [ f(Ai) | w([Ai], ..) ] OVER ({ ORDER BY Aj [ ASC | DESC ] }), .. 
FROM ...
```

- Esto ordena el resultado de la consulta por el atributo *Aj* y para cada fila imprime el resultado de una función de agregación, *f(Ai)*, ó de una función de ventana *w(\[Aj], ...)*.
- Hasta acá, *f(Ai)* no parece nada muy novedoso y que no podemos hacer con un GROUP BY.
- Bajo este esquema también podemos usar funciones de ventana como, *w(\[Aj], ...)*, como:
1. **RANK():** Nos devuelve el ranking de cada fila, de acuerdo al valor del atributo de ordenamiento de la partición.
2. **ROW_NUMBER():** Nos devuelve el número de orden de la fila en la partición.
3. **LAG(Ai, offset):** Nos devuelve el valor que toma el atributo *Ai* en una fila a distancia *offset* hacia atrás de la actual.

#### Ejemplo:
![[Base de Datos/Structured Query Language/images/Tabla ejemplo ventanas.png]]

Si hacemos la query 

```SQL
SELECT RANK() OVER (ORDER BY marca_seg ) AS posición, nombre_atleta , país_origen , marca_seg 
FROM Final_2009 ;
```

Obtenemos:

![[Base de Datos/Structured Query Language/images/Ejemplo rank over.png]]

Si queremos la diferencia de tiempo que cada atleta tuvo con el anterior usamos

```SQL
SELECT 
RANK() OVER (ORDER BY marca_seg ) AS posición, nombre_atleta , país_origen , marca_seg , marca_seg − LAG(marca_seg , 1) OVER (ORDER BY marca_seg ) AS diferencia 
FROM Final_2009 ;
```

![[Base de Datos/Structured Query Language/images/Ejemplo lag over.png]]
### Ventanas bajo múltiples particiones
