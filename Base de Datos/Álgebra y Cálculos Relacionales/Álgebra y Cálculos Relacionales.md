Los lenguajes que permiten extraer información de un modelo de datos se denominan **lenguajes de manipulación de datos**, o DML (Data Manipulation Languages)
- **Lenguajes Procedurales:** Indican un procedimiento a seguir utilizando operaciones que indican cómo manipular los datos (son de más bajo nivel).
- **Lenguajes Declarativos:** Indican qué resultado se quiere obtener, sin especificar cómo hacerlo.

Algunos DML son formales y algunos otros son prácticos ([[Base de Datos/Structured Query Language/SQL|SQL]]).
Los lenguajes formales del modelo relacional son:
- El [[Álgebra Relacional|álgebra relacional]] (procedural).
- El [[Cálculo Relacional|cálculo relacional]] (declarativo).

# Completitud Relacional

E. Codd demostró la equivalencia entre el álgebra relacional básica y el cálculo relacional.
Esta equivalencia implica que ambos lenguajes tienen el mismo poder expresivo, pues toda consulta expresable a través del cálculo relacional es también expresable en el álgebra relacional básica y viceversa.

A su vez, se dice que un lenguaje es relacionalmente completo cuando tiene la misma capacidad expresiva que el cálculo relacional. El álgebra relacional básica es relacionalmente completa.