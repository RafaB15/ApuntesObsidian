**a) Obtener el padrón y apellido de el/los alumno/s que tenga/n la mayor cantidad de materias aprobadas
Nota: Considerar la posibilidad de que sean más de uno.**

```SQL
SELECT alumnos.padron, alumnos.apellido
FROM alumnos INNER JOIN notas USING(padron)
WHERE notas.nota >= 4
GROUP BY alumnos.padron, alumnos.apellido
HAVING COUNT(notas.nota) = 
	(SELECT MAX(cant)
	FROM (
		SELECT COUNT(notas.nota) as cant
		FROM notas
		WHERE notas.nota >= 4
		GROUP BY notas.padron
	) AS candidate_table)	
```

*Resultado:*

![[Base de Datos/Parcialitos/images/Resultado parcialito 3 a.png]]

**b) Obtener el padrón y apellido de aquellos alumnos que tienen nota en las materias 71.14 y 71.15 y no tienen nota ni en la materia 75.01 ni en 75.15.**

```SQL

SELECT DISTINCT al.padron, al.apellido
FROM alumnos al INNER JOIN notas n USING(padron)
WHERE(n.codigo = 71 AND (n.numero = 14 OR n.numero = 15))
EXCEPT(
	SELECT DISTINCT al.padron, al.apellido
	FROM alumnos al RIGHT OUTER JOIN notas n USING(padron)
	WHERE(n.codigo = 75 AND (n.numero = 1 OR n.numero = 15))
)

```

*Resultado:*

Tabla vacía, no hay matches para nuestra query.

**c) Se necesita saber el promedio general para cada carrera y cada departamento. Devolviendo código de carrera, código de departamento, y el promedio de notas para todos los alumnos de cada departamento, ordenados por carrera y departamento. 
Nota: no considerar combinaciones de departamento / carrera tal que no haya alumnos de dicha carrera con notas en dicho departamento. 
Nota 2: Si un alumno está inscripto en más de una carrera, sus notas aportan a los promedios de todas esas carreras.**

```SQL

SELECT cod_carrera, cod_departamento, ROUND(AVG(nota), 2) as nota_promedio
FROM alumnos 
	INNER JOIN (SELECT padron, codigo as cod_carrera FROM inscripto_en) as tabla_inscripciones USING(padron)
	INNER JOIN (SELECT padron, codigo as cod_departamento, nota FROM notas) as tabla_notas USING(padron)  
GROUP BY cod_carrera, cod_departamento
ORDER BY cod_carrera ASC, cod_departamento ASC

```

*Resultado:*

![[Base de Datos/Parcialitos/images/Resultado parcialito 3 c.png]]

**d) Mostrar el padrón, apellido y promedio para aquellos alumnos que tienen nota en más de 3 materias y un promedio de al menos 5**

```SQL

SELECT al.padron, al.apellido, ROUND(AVG(nota), 2) as nota_promedio
FROM alumnos al INNER JOIN notas n USING(padron)
GROUP BY al.padron, al.apellido 
HAVING COUNT(nota) > 3 AND AVG(nota) >= 5

```

*Resultado:*

![[Base de Datos/Parcialitos/images/Resultado parcialito 3 d.png]]

**e) Para cada nota del alumno más antiguo, mostrar su padrón, código de departamento, número de materia y el valor de la nota. 
Nota: En caso de que sean más de uno los alumnos más antiguos, mostrar dichos datos para todos esos alumnos. 
Nota 2: Si bien en la realidad puede darse que los valores de padrón sean estrictamente crecientes en el tiempo. NO utilizar este criterio para determinar al alumno más antiguo.**

```SQL

SELECT al.padron, n.codigo as cod_departamento, n.numero, n.nota
FROM alumnos al LEFT OUTER JOIN notas n USING(PADRON)
WHERE al.fecha_ingreso = (SELECT MIN(fecha_ingreso)
							FROM alumnos)

```

*Resultado:*

![[Base de Datos/Parcialitos/images/Resultado parcialito 3 e.png]]

**f ) Listar el padrón de aquellos alumnos que, por lo menos, tienen nota en todas las materias que aprobó el alumno de padrón 71000.**

```SQL

SELECT n.padron
FROM notas n
	INNER JOIN (SELECT DISTINCT codigo, numero FROM notas WHERE padron = 71000 AND nota >= 4) as alumno_pedido
	ON(n.codigo = alumno_pedido.codigo AND n.numero = alumno_pedido.numero)
GROUP BY n.padron
HAVING COUNT(DISTINCT (n.numero, n.codigo)) = (SELECT COUNT(DISTINCT (codigo, numero)) FROM notas WHERE padron = 71000)

```

*Resultado:*

![[Base de Datos/Parcialitos/images/Resultado parcialito 3 f.png]]