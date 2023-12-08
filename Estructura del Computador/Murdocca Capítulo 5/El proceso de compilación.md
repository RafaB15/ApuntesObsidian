# Los pasos de la compilación

$$
A=B+4;
$$

- Se reconocen los símbolos básicos del lenguaje: A, B, 4, = y +.
- Analizar los símbolos para reconocer la estructura de programación subyacente. A este procedimiento se lo conoce como análisis sintáctico. Se encarga el analizador (parser).
- Análisis de nombres. Asociar los nombres con las variables y su espacio en memoria.
- Análisis de tipo. Determinar el tipo se todos los datos requeridos.
- Asignación de acciones y generación de código.

![[35EA274F-8600-41B1-B207-E56EF1C62249.jpeg|35EA274F-8600-41B1-B207-E56EF1C62249.jpeg]]

- También hay acciones adicionales que deben ser resueltas por el compilador.

# Cómo convierte el compilador los tres tipos de instrucciones al código ensamblador

## Almacenamiento de variables en memoria

Variables locales → Pila tipo LIFO

El puntero a esta pila se llama %fp

## Movimiento de datos

### Structs

Un struct en C sería acomodado por el compilador como tantas posiciones de memoria consecutivas como componentes tenga el struct.

### Arreglos

Si tenemos un arreglo declarado int A[10]; , y luego escribimos A[i], el valor de A[i] se determina en le momento de la ejecución en vez de conocerse de antes.

Dirección del elemento = BASE + (ÍNDICE - COMIENZO) * TAMAÑO

Comienzo en C es 0.

En ARC si se supone base en %r2, indice en %r3, comienzo en %r4 y tamaño = 4, el código necesario para la carga de un elemento del arreglo en memoria sería:

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de compilación/Untitled.png|Untitled]]

## Instrucciones aritméticas

Si tienen demasiadas variables a veces se tendrá que poner algunas en la fila al no alcanzar los registros.

También se analiza si los datos almacenados en registros siguen siendo necesarios (proceso “vivo o muerto”).

## Control de secuencia

### La sentencia goto

Esta se implementa en lenguaje de máquina con una instrucción de salto incondicional ba (branch always):

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de compilación/Untitled 1.png|Untitled]]

### La sentencia if-else

Supongamos que la expresión a evaluar es (%r1 == %r2).  La introducción salto por distinto, bne (branch if no equal), permite obtener este código para la implementación de la sentencia if-else

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de compilación/Untitled 2.png|Untitled]]

### La sentencia while

En c:

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de compilación/Untitled 3.png|Untitled]]

En ARC:

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de compilación/Untitled 4.png|Untitled]]

### La sentencia do-while

Igual al while pero sin la primera línea con el ba.

### La sentencia for

Igual al while, pero agregando el código requerido para el contador como condición.