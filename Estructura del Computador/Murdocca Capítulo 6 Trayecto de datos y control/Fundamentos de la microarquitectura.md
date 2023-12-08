La funcionalidad de una microarquitectura se centra en el ciclo de búsqueda y ejecución de una instrucción.

Los pasos involucrados en el ciclo de búsqueda y ejecución son:

1. Buscar en memoria la siguiente instrucción que debe ejecutarse.
2. Decodificar el código de operación.
3. Si los hubiera, leer los operandos desde memoria o desde registros.
4. Ejecutar la instrucción y almacenar los resultados.
5. Volver al paso 1.

La microarquitectura de una máquina incluye una ***sección de datos***, que contiene registros y una unidad aritmético-lógica, y una sección de control.

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled.png|Untitled]]

La sección de datos también se conoce como ***trayecto de datos.***

# Una microarquitectura para ARC

## El trayecto de datos

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 1.png|Untitled]]

En este trayecto de datos hay:

- 32 registros de datos accesibles para el usuario.
- El contador del programa (%pc). Apunta a la dirección a ser leida desde la memoria principal.
- El registro de instrucciones (%ir). Contiene la instrucción en ejecución.
- La unidad aritmético lógica (ALU)
- Cuatro registros temporarios no accesibles (%temp0-%temp3). Se usan para interpretar el registro de instrucciones ARC.
- La conexiones entre estos elementos.

Si en la figura hay una barra diagonal acompañada de un número es para simplificar la representación de varios cables.

### La unidad aritmético-lógica (ALU)

Puede realizar una de 16 operaciones sobre los buses A y B. El resultado de cada operación se coloca en el bus C.

La unidad aritmético-lógica genera los códigos de condición c. n. z y v. que resultan ciertos cuando se produce, respectivamente, un arrastre, un resultado negativo. un resultado nulo y un desborde. Estos códigos de condición solo se modifican a través de las instrucciones que así lo indican en la tabla de la figura 6.4. En estos casos se genera una señal (SCC) que le indica al registro %psr que debe actualizar sus códigos de condición.

Una ALU se puede implementar de muchas formas distintas

### Tabla de consulta (LUT, look up table)

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 2.png|Untitled]]

La unidad aritmético lógica puede descomponerse en una cascada de 32 tablas de búsqueda que implementan cada una de las operaciones aritméticas y lógicas, seguida de un **circuito controlador de desplazamientos (barrel shifter)** que implementa los desplazamientos.

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 3.png|Untitled]]

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 4.png|Untitled]]

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 5.png|Untitled]]

### Los registros

Todos los registros están implementados con circuitos biestables D activados por flanco negativo.

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 6.png|Untitled]]

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 7.png|Untitled]]

## La sección de control

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 8.png|Untitled]]

En el corazón de la unidad de control, una memoria de lectura (ROM) de 2048 palabras de 41 bits contiene los valores de todas las lineas que deben controlarse para implementar cada instrucción a nivel del usuario. En este contexto la memoria de lectura suele considerarse como una **memoria de control (control store)**.

Cada palabra de 41 bits es una **microinstrucción**. La unidad de control es la responsable de la búsqueda de las microinstrucciones y de su ejecución.

La ejecución de microinstrucciones se controla a través del registro de instrucciones de microprograma (***MIR***, microprogram instruction register), del registro de estado &psr y de un mecanismo que permite determinar cuál es la siguiente microinstrucción a ejecutar.

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 9.png|Untitled]]

Cada palabra de 41 bits comprende 11 campos distintos.

- El campo A determina cuál es el registro del trayecto de datos cuyo contenido debe colocarse sobre el bus A.
- El campo AMUX selecciona si el decodificador A obtiene su entrada desde el campo A del registro MIR (AMUX = 0) o desde el campo rs1 del registro %ir (AMUX = 1).
- El campo B determina cuál de los registros del trayecto de daros debe colocar su contenido sobre el bus B.
- El campo BMUX determina si el decodificador B obtiene sus entradas desde el campo B del MIR (BMUX = 0) o desde el campo rs2 de %ir (BMUX = 1).
- El campo C determina en cuál de los registros del trayecto de datos se almacenará el dato transferido a través del bus C.
- El campo CMUX elige si la entrada al decodificador C se obtiene desde el campo C del MIR (CMUX = 0) o desde el campo rd de %ir
(CMUX = I).
- Dado que el contenido del registro %r0 no puede modificarse, puede usarse el patrón binario 000000 cuando no se requiere modificar el contenido de ningún registro.
- Las líneas RD y WR determinan, respectivamente, si se debe leer o escribir en meroria. Se realiza una lectura cuando RD = 1, en tanto que se realiza una escritura de memoria
cuando WR = 1.
- El campo denominado ALU determina cuál de las operaciones aritmético-lógicas se ejecuta de acuerdo con los valores establecidos en la figura 6.4. El campo ALU puede adoptar
16 valores diferentes, todos los cuales corresponden a operaciones aritmético-lógicas válidas. Esto implica que no hay forma de "apagar la unidad aritmético-lógica cuando no se la necesita, tal como cuando se realiza una lectura o una escritura en memoria. En estos casos debe elegirse una operación de la unidad aritmético-lógica que no presente efectos colaterales indeseados. Por ejemplo. no seria apropiado presentarle a la unidad aritmético-lógica la instrucción ANDCC, que cambia los códigos de condición, pero sí podría aceptarse la operación AND, que no los afecta.
- El campo COND (salto condicional) del formato de la microinstrucción hace que el **microcontrolador** rescate la micropalabra siguiente, ya sea desde la posición siguiente en la memoria de control. o desde la posición indicada en el campo JUMP ADDR del registro MIR, o bien desde los bits del código de operación almacenado en %ir. El campo COND se interpreta de acuerdo a la siguiente tabla.

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 10.png|Untitled]]

- Si el campo COND vale 000, no hay salto alguno y se utiliza la entrada next del multiplexor de direcciones de la memoria de control.
- Si el campo COND vale 001, 010, 011,100 o 101, se procede a realizar un salto condicional a la posición de la memoria de control indicada en el campo JUMP ADDR de acuerdo con el valor de las banderas n, z, v o c del bit 13 de %ir, respectivamente.
- La sintaxis “IR[13]” representa el bit 13 del registro de instrucciones %ir.
- Si el campo COND vale 110, se produce un campo incondicional.
- Durante la decodificación de una instrucción, el campo COND adopta el valor 111.

Cuando el campo COND vale 111, la dirección de memoria de control que debe copiarse en el registro MIR se toma desde una combinación de 11 bits creada mediante el agregado de un 1 a la izquierda de lo bits 30 y 31 de %ir y del agregado de ceros a la derecha de los bits 19-24 del mismo registro %ir.

![[Estructura del Computador/Murdocca Capítulo 6 Trayecto de datos y control/Fundamentos de la microarquitectura/Untitled 11.png|Untitled]]

## Temporización