- Se refiere al diseño de [[Base de Datos/Modelo Lógico Relacional/Modelo Relacional|modelos relacionales]]. Más específicamente, nos referimos a la verificación del diseño de [[Base de Datos/Modelo Lógico Relacional/Esquema de Base de Datos|esquemas de bases de datos]].
- Los criterios de un buen diseño relacional son
	- Preservación de información
	- Redundancia mínima
- A través de las formas normales, la teoría del diseño relacional formaliza los requisitos para diseñar bien un esquema relacional. 
	- Sin tener el diagrama de entidad relación, podremos ver un esquema de base de datos y decir si estos siguen las reglas para estar bien hecho, siguiendo las restricciones del pasaje de modelo conceptual al relacional.

# Formas Normales

- Las formas normales son una serie de estructuras con las que un esquema de base de datos puede cumplir o no.
- Las formas normales clásicas son:
	- [[Base de Datos/Diseño Relacional/Primera Forma Normal|Primera forma normal (1FN)]].
	- [[Base de Datos/Diseño Relacional/Segunda Forma Normal|Segunda forma normal (2FN)]].
	- [[Base de Datos/Diseño Relacional/Tercera Forma Normal|Tercera Forma Normal (3FN)]].
	- [[Base de Datos/Diseño Relacional/Forma Normal Boyce-Codd|Forma Normal Boyce-Codd (FNBC)]].
	- Cuarta forma normal (4FN).
	- Quinta forma normal (5FN).
- En el orden anterior, cada forma normal es más fuerte que las anteriores.
$$\displaystyle \large \text{S está en } 5FN \to \text{S está en } 4FN \to \dots \to \text{S está en } 1FN$$
- **Normalización:** Proceso a través del cual se convierte un esquema de base de datos en uno equivalente (que preserve toda la información) y que cumple con una determinada forma normal.
- El objetivo es
	- Preservar la información
	- Eliminar la redundancia
	- Evitar las anomalías de ABM.
- Cuando avanzamos en las formas normales todas nuestras restricciones terminan siendo claves primarias.

# Resumen

1. Estoy en 1ra forma normal cuando no tengo vectores en mis atributos. Todos los atributos deben ser monovaluados.
2. Estoy en 2da forma normal cuando no tengo atributos no primos dependiendo de atributos primos que no son por sí mismos una CC; o sea, atributos no primos dependiendo parcialmente de una clave. Puedo tener atributos primos dependiendo parcialmente de CCs, y puedo tener atributos no primos dependiendo de otros atributos no primos. También puedo tener atributos no primos dependiendo de una CC entera. Pero no puedo tener atributos no primos dependiendo de parte de una CC.
3. Estoy en 3ra forma normal cuando no hay transitividad de no primos. O sea, puedo tener primos dependiendo parcialmente de CCs, pero no puedo tener no primos dependiendo de otros no primos (porque todo no primo depende de una CC entera, por definición de CC, y si hay un no primo dependiendo de otro no primo, entonces inevitablemente tengo una dependencia transitiva). Es decir, para estar en 3FN, todo atributo no primo debe sí o sí depender solamente de CCs enteras (no parcialmente por 2FN y no de atributos no primos por 3FN).
4. Estoy en FNBC cuando todo atributo, sea primo o no primo, depende sí o sí de una CC entera. No puedo tener primos dependiendo parcialmente de otras CCs. Es decir, las únicas dependencias permitidas son las de atributos (primos o no primos) dependiendo de CCs enteras. Todo implicante debe ser sí o sí CC, aunque todo implicado puede ser primo o no primo.