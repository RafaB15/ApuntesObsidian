# Interacción entre features categóricos:

- Podemos crear un nuevo feature que sea la concatenación de los features y encodear este nuevo feature.
- Podemos encodear cada feature individualmente y luego generar el producto entre los encodings.

# Interacción entre features numéricos

- Multiplicación
- Suma
- División → Cantidad de ventas exitosas / Cantidad de ventas totales
- Diferencia

- Con N variables hay N*N interacciones posibles y eso si solo tomamos de a dos.
- Es necesario establecer un loop para encontrar interacciones útiles.
- Ej: Fittear un Random Forest, usar la importancia de cada feature para filtrar.

# Múltiples interacciones:

- Estableces interacciones múltiples entre variables es una tarea compleja y artesanal.
- Una posible solución es usar pequeños árboles de decisión y encontrar el índice de la hoja ára cada dato, luego usarlo como feature.

![[Organización de datos/Feature Engineering/Interacción entre Features/Untitled.png|Untitled]]