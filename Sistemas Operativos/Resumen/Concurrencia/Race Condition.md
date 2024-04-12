- Las race conditions (condiciones de carrera o data race) son problemas comunes que pueden suceder cuando se trabaja con [[Thread|threads]]. 
- Se da cuando el resultado de un programa depende en como se intercalaron las operaciones de los [[Thread|threads]] que se ejecutan dentro de un [[Sistemas Operativos/Resumen/Proceso|proceso]].
- Un thread podría estar en el medio de modificar la variable, cargando registros con la información que esta tenía, y de pronto hay un **context switch** y el [[Scheduling|scheduler]] pasa al otro thread, haciendo que por ejemplo en la siguiente imagen, se ejecute la operación de sumar 1 a una variable 2 veces, pero la variable aumente solo en 1.

![[Race Condition.png]]

- Esto genera que al ejecutar el mismo código varias veces, los resultados puedan no ser los mismos, que sean indeterminados.
- **Critical Section** $\to$ Una sección de código que accede a una variable compartida y no debería ser ejecutada concurrentemente con algún otro thread.
- **Mutual Exclusion** $\to$ Propiedad que garantiza que si un thread está ejecutando una sección crítica, entonces ningún otro thread la puede ejecutar la mismo tiempo.