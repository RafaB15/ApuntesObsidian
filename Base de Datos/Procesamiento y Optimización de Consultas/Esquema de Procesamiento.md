- Un esquema de procesamiento de una expresión de SQL se ve de la siguiente forma

![[Esquema de Procesamiento.png]]

- Cuando se hace una consulta en [[SQL]], se arma un [[Planes de Consulta y Ejecución|plan de consulta y ejecución]] utilizando la [[Información de Catálogo]].
- Se parsea la consulta para pasarla de un lenguaje declarativo a un lenguaje procedural como el [[Álgebra Relacional]] en el caso de las bases de datos realcionales.
- Se elije el plan más eficiente usando la [[Información de Catálogo]] para calcular los [[Costos de los Operadores|costos]].