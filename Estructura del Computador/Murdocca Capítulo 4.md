El ***lenguaje de máquina*** es el lenguaje que puede entender el hardware.

Se analiza habitualmente en función del ***lenguaje ensamblador (assembly language)*** o lenguaje simbólico. Es como el lenguaje de máquina pero legible. 

Se utilizará como modelo de arquitectura la de la computadora ***ARC***, simplificación de la arquitectura comercial ***SPARC***, común en las computadores Sun.

Ejecutar una aplicación significa sacarla de su archivo de disco (.exe) y traerla a memoria a ram.

# Componentes circuitales de la arquitectura de programación

Al programar en lenguaje ensamblador nos coloca ante una visión que incluye todos los elementos circuitales accesibles al programador y las instrucciones que manejan información delntro del hardware.

## Modelo de bus

Usado por los modelos de computadora basado en buses. 

El propósito del bus es reducir la cantidad de interconexiones entre la CPU y sus subsistemas. La CPU se interconecta con la memoria y con cada uno de los dispositivos de entrada y salida a través del ***bus del sistema***.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled.png|Untitled]]

La CPU genera las direcciones que se transfieren sobre el bus direcciones, mientras que la memoria recibe esas direcciones a través del bus de direcciones. La memoria nunca genera direcciones, por consiguiente no hay interconexión en ese sentido.

Normalmente el usuario escribe un programa en un lenguaje de alto nivel, por medio de un programa compilador se traduce a lenguaje ensamblador, luego un programa ensamblador convierte el programa en lenguaje simbólico a lenguaje de máquina, para su almacenamiento en disco.

Antes de ejecutarlo, el sistema operativo de la computadora carga el programa en lenguaje de máquina desde el disco a la memoria principal.

Durante la ejecución del programa cada instrucción se carga en la CPU desde la memoria, a razón de una instrucción por vez.  La salida del programa se coloca en un dispositivo.

La comunicación entre los tres componentes CPU, memoria y entrada-salida se maneja por medio de buses.

## Memoria

La memoria de una computadora consiste en un conjunto de ***registros*** numerados (direccionados) en forma consecutiva, cada uno de los cuales normalmente almacena un byte de información.

Dirección del registrto → locación de memoria.

Un byte →    8 bits

Un nibble → 4 bits

Una ***palabra →*** Depende de la arquitectura del procesador. Tipicamente son de 16, 32, 64 o 128 bits. Si no se indica otra cosa estamos usando 32 bits en este libro.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 1.png|Untitled]]

Las palabras de más de un byte se almacenan como una secuencia de bytes y se direccionan a partir del byte menos significativo de la palabra almacenada.

Hay dos alternativas en cuanto a como almacenar estos bytes en memoria.

- ***Big endian:***  El byte más significativo se almacena en la dirección más baja de memoria.
- ***Little endian:*** El byte menos significativo es el que se almacena en la dirección más baja de memoria.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 2.png|Untitled]]

El número que identifica univocamente cada palabra se define como su ***dirección.*** La última dirección de una memoria de $2^{32}$ bytes es $2^{32}-1$ y la primera dirección es 0. ($2^{32}$ direcciones posibles)

En este capítulo se supone que la memoria de la computadora está organizada en un único espacio de direcciones.

***Espacio de direcciones →*** Rango numérico de direcciones de memoria al que puede hacer referencia la unidad de proceso.

El rango de las direcciones de memoria va desde $0$ hasta $2^{32}-1$, o desde $00000000H$ Y $FFFFFFH$.

## La unidad central de proceso (CPU)

La estructura de la CPU consiste en una ***sección de datos***, formada por los ***registros*** y la ***unidad aritmético-lógica (ALU),*** y una ***sección de control,*** la que interpreta las instrucciones y realiza las transferencias entre registros. La sección correspondiente a los datos se conoce también como ***trayecto de datos (datapath).***

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 3.png|Untitled]]

***Unidad de control →*** Encargada de la ejecución de las instrucciones del programa almacenadas en memoria principal.

Existen dos registros que forman la interfaz entre la unidad de control y la unidad de datos, llamados ***contador de programa (PC, program counter)*** y ***registro de instrucción (IR, instruction register).*** El contador del programa contiene la dirección de la instrucción en ejecución. La instrucción a la que apunta el PC se rescata de memoria y se almacena en el IR, desde donde se la interpreta.

Pasos que lleva a cabo la unidad de control en la ejecución de un programa:

1. Búsqueda en memoria de la próxima instrucción a ser ejecutada.
2. Decodificación del código de operación.
3. Búsqueda de operandos en memoria, si los hubiera.
4. Ejecución de la instrucción y almacenamiento de los resultados.
5. Vuelta al paso 1.

Este proceso se conoce como ***ciclo de búsqueda-ejecución.***

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 4.png|Untitled]]

El trayecto de datos está constituido por un ***conjunto*** o ***bloque de registros*** y por la unidad aritmético-lógica.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 5.png|Untitled]]

El conjunto de registros de la figura puede verse como una memoria, pequeña y rápida, separada de la memoria del sistema, que se utiliza para el almacenamiento temporario durante las operaciones de cálculo. 

Cada registro recibe una dirección de memoria, aunque estás son mucho más chicas que las direcciones recibidas por la memoria, si hay 32 registros solo se requerirá una palabra de direcciones de cinco bits. 

Las diferencias principales entre el conjunto de registros y la memoria del sistema derivan de que los registros están contenidos dentro de la CPU, por consiguiente, funcionan con mayor rapidez que aquella.

Una instrucción que se ejecuta sobre operandos almacenados en el conjunto de registros puede ejecutarse unas diez veces más rápido que si los operandos estuviesen en memoria.

La ALU está conectada a través de 3 buses con el conjunto de registros. 

La Alu implementa una variedad de operaciones de uno o dos operandos (suma, producto, operaciones lógicas de disyunción ***(or)***, conjunción ***(and)***, negación ***(not)***). 

### El conjunto de intrucciones:

Es la colección de instrucciones que un procesador puede ejecutar, lo cual lo define. Varían dependiendo del procesador, a diferencia de lenguajes de alto nivel que mientras se los compile para cada procesador de una forma específica se escriben igual.

# ARC, una computadora RISC (**A** **R**isc **C**omputer)

## Memoria en ARC

ARC es una máquina de 32 bits con capacidad de direccionamiento de memoria por bytes; puede manejar tipos de datos de 32 bits, pero toda la información se almacena en memoria en la forma de bytes. 

La dirección de la palabra de 32 bits es la del byte almacenado en la menor de las direcciones de la palabra (***Big endian)***

***Mapa de memoria →*** Distribución de los espacios de direcciones de una arquitectura

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 6.png|Untitled]]

- Las $2^{11} = 2048$ primeras direcciones del mapa de memoria se reservan para ser usadas por el sistema operativo.
- El espacio para el usuario es aquel que se reserva para la carga de los programas ensamblados del usuario, y puede crecer, durante la operación, desde la dirección 2048 hasta que se encuentre con la pila del sistema.
- La pila del sistema comienza en la dirección $2^{31} - 4$ y crece hacia las direcciones inferiores de memoria.
- La zona del espacio de direcciones ubicada entre $2^{31}$ y $2^{32} - 1$ se reserva para los dispositivos de entrada y salida. Cada dispositivo tiene asignada una serie de direcciones de memoria para el almacenamiento de sus datos, en lo que se denomina “entrada-salida mapeada en memoria”.
- Todas las instrucciones ocupan 32 bits.

La máxima dirección disponible para el almacenamiento de un byte en ARC es $2^{32}-1$, de modo que la dirección de la palabra más alta de memoria está ubicada tres bytes por debajo de esta en $2^{32}-4$. (Esto es así porque las palabras de 32 bits se almacenan en memoria como un conjunto de 4 bytes y estamos usando big endian).

## Conjunto de instrucciones ARC

Primero revisemos las características del CPU

- ARC tiene 32 registros de uso general, de 32 bits cada uno, así como un contador de programas (PC) u un registro de instrucción (IR).
- Existe un registro de estado del procesador (PSR, processor status register) que contiene información acerca del estado del procesador, incluida la información acercad de los resultados de las operaciones artiméticas. Almacenan las “banderas aritméticas” (lso flags), cero ***z,*** negativo  ***n***, si se obtuvo un arrastre a la salida de la unidad aritmético-lógica de 32 bits ***c*** y desborde **v.**
- El tamaño de todas las instrucciones es de una palabra (32 bits).
- ARC es una máquina de arquitectura carga-descarga (load-store). Las únicas instrucciones permitidas para el acceso a memoria cargan un valor hacia alguno de los registros, o almacenan en alguna posición de memoria el contenido de algunos de los registros. Todas las operaciones aritméticas se ejecutan sobre operandos contenidos en registros y los resultados también quedan almacenados en un registro.
- El conjunto de instrucciones del procesador SPARC, sobre el que se basa ARC tiene aproximadamente 200 instrucciones.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 7.png|Untitled]]

### Instrucciones para el movimiento de datos

***ld*** (load) y ***st*** (store) transfieren unan palabra entre la memoria principal y alguno de los registros de ARC.

Estas son las únicas instrucciones que permiten el acceso a memoria dentro de ARC.

Las instrucción ***sethi*** carga los 22 bits más significativos de un registro con la constante de 22 bits contenida dentro de la instrucción.

### Instrucciones aritméticas y lógicas

Las instrucciones ***andcc, orcc*** y ***orncc*** realizan operaciones Y, O y NOR respectivamente sobre sus operandos.

Para ***andcc***, cada bit del resultado se coloca en 1 si los bits correspondientes de ambos operandos son simultaneamente 1, en caso contrario va un cero.

Or y nor son análogos.

Los sufijos ***cc*** indican que luego de realizada la operación deben actualizarse los códigos de condición del registro de estado de modo que permitan reflejar el resultado de la operación realizada.

Las instrucciones de desplazamiento permiten desplazar el contenido de un registro hacia otro. 

La instrucción ***srl*** (shift right logical) desplaza un registro hacia la derecha y carga ceros en los bits más significativos.

La instrucción ***sra*** (shift right arithmetic) que no se indica en la tabla, desplaza le contenido original del registro a la derecha y almacena una copia del bit más significativo del contenido original en los bits vacíos creados por el desplazamiento del registro. Esto hace que el operando preserve su signo, pues se extiende.

La instrucción ***addcc*** realiza sobre sus operandos una suma de 32 bits en complemento a dos.

De los operandos al menos uno tiene que estar guardado en un registro.

### Instrucciones de control

Las instruicciones ***call*** y ***jmpl*** forman un par utilizado para el llamado de subrutinas y el retorno desde las mismas, respectivamente.

***jmpl*** también se utiliza para transferir el control a otro sector del programa.

## Formato del lenguaje simbólico de ARC

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 8.png|Untitled]]

Los rótulos se forman con cualquier palabra, numero, (_), ($) y (.), siempre que no empiece con un dígito. Termina en dos puntos.

Los 32 registros de ARC se denominan  ***%***r0 - %r31***, cada uno de los cuales contiene una palabra de 32 bits.

El registro de estado del procesador (PSR), que describe el estado vigente del procesador, se denomina &***psr***.

El contador de programa (PC) que controla la dirección de la instrucción en ejecución se designa como %***pc.***

El registro %***r0*** siempre contiene el valor 0, el cual no puede modificarse. 

Los registros %***r14*** y %***r15*** tienen aplicaciones adicionales como ***puntero de pila*** (%sp, stack pointer) y ***registro de enlace*** (link register), respectivamente.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 9.png|Untitled]]

Los operandos que aparecen en las sentencias del lenguaje se separan por comas, el de destino es el más a la derecha.

Si en el destino esta %r0 entonces el resultado se descarta.

## Directivas al ensamblador

Existen directivas (pseudo operaciones) que no son código de operación sino más bien instrucciones dirigidas al ensamblador para que realice ciertas acciones en el momento del ensamble.

Las instrucciones son específicas de un procesador.

Las directivas son específicas de un programa ensamblador.

Algunas generan información en la memoria otras no.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 10.png|Untitled]]

## Formatos de instrucción en ARC

- Todas las instrucciones ocupan 32 bits.
- No todas las instrucciones siguen el mismo formato.
- Se definen grupos de bits a los que se les da un significado.
- El formato de instrucción define la manera en que el ensamblador distribuye los diversos campos de una instrucción y la forma en la que los interpreta la unidad de control de ARC.
- Respecto a su código de máquina, todos los formatos de instrucciones se pueden agrupar en 5 formatos:
    - Formato de la instrucción Sethi
    - Formato de instrucciones tipo Branch
    - Formato de la instrucción Call
    - Formato de instrucciones aritméticas
    - Formato de instrucciones de acceso a memoria

 

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 11.png|Untitled]]

Hay dos bits (el 30 y 31) que hacen la clasificación gruesa. op. Si ambos son 0 entonces es SETHI (set high) o Branch. Si es 01 es CALL, si es 10 son funciones aritméticas y lógicas y cuando son 11 entonces es de Memoria.

Si op2 vale 100 se trata de un SETHI. Tednrá 5 bits para el registro destino y en los 22 bits restantes tendrá la famosa constante SETHI.

Si op2 vale 010 se trata de un Branch. En 22 bits tiene guardada la dirección a la cual saltar. En 4 bits me indicaen qué flags se fija.

CALL me indica la dirección a la que salto.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 12.png|Untitled]]

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 13.png|Untitled]]

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 14.png|Untitled]]

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 15.png|Untitled]]

## Formatos de datos en ARC:

ARC soporta 12 formatos de datos.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 16.png|Untitled]]

ARC no diferencia entre enteros signados y no signados. Se manejan y almacenan como enteros en complemento a dos, pero se interpretan distinto.

## Variantes en las arquitecturas y en los direccionamientos.

Las máquinas presentaban instrucciones aritméticas de una, dos y tres direcciones. Esto significa que una instrucción podía realizar cálculos aritmético con tres, dos o uno de sus resultados u operandos en emmoria, lo que se contrapone con la arquitectura de ARC, en la que todas las operaciones aritméticas y lógicas requieren que sus operandos estén almacenados en registro.

$A = B \ * \ C \ +\ D$ podría codificarse como:

### Instrucciones de tres dimensiones:

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 17.png|Untitled]]

### Instrucciones de dos dimensiones:

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 18.png|Untitled]]

### Instrucciones de una dimensión:

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 19.png|Untitled]]

Las instrucciones de una dimensión son las que tienen el menor tamaño del programa y el menor tráfico de instrucciones.

# El acceso a la información en la memoria. Modos de direccionamiento

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 20.png|Untitled]]

Esta notación difiere de la de ARC.

La notación $M[x]$ en la columna de significados supone que la memoria es un arreglo, $M$, indexado según una dirección que se obtiene del cálculo indicado entre corchetes.

- El direccionamiento inmediato permite hacer referencia a una constante cuyo valor se conoce al momento del ensamble.
- El direccionamiento directo se utiliza para acceder a aquellos datos cuya dirección se conoce al momento del ensamble.
- El direccionamiento indirecto se utiliza para acceder a una variable puntero cuya dirección se conoce al momento de la compilación.
- El direccionamiento indirecto a través de registro se usa cuando la dirección del operando no se conoce hasta el momento de la ejecución.
- El direccionamiento indexado, el basado en registro y el indexado basado en registro se usan para acceder a los componentes de arreglos y a aquellos componentes ubicados más allá del comienzo de la pila, en una estructura conocida como bloque de datos (***stack frame***).

# Acceso a subrutinas y pilas

Una subrutina es exactamente el mismo concepto que una función o procedimiento en alto nivel.

Toda rutina o procedimiento tiene un return, el return en una subrutina se llama jmpln 

Al llamar a una subrutina con call, la dirección en la que estaba guardada la instrucción de hacer ese call es guardada en %r15, por lo que al finalizar la subrutina hacemos un jmpl a %r15 + 4 para estar ubicados en la instrucción que le seguía al call, dado que cada instrucción pesa 4 bytes.

Existen diversos métodos para pasar argumentos hacia y desde la rutina invocada conocidos como ***convenciones de llamada***. El proceso de transferencia de argumentos entre subrutinas suele conocerse como ***enlace entre sbrutinas***.

Una de estas convenciones de llamada es cargar los argumentos en registros como se ve a continuación:

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 21.png|Untitled]]

Otra forma es crear una zona de transferencia de datos. La dirección de esta zona se entrega  a la rutina invocada en un registro predeterminado. En el ejemplo la directiva .dwb que aparece en la rutina invocante genera una zona de transferencia de datos, de tres palabras en las direcciones x, x+4 y x+8.

![[Estructura del Computador/Murdocca Capítulo 4/Untitled 22.png|Untitled]]

Otra convención para las llamadas a subrutinas es una pila. La idea general es que la rutina invocante coloca (push) todos sus argumentos en una pila secuencial del tipo LIFO (last in first out). La rutina invocada extrae de la pila los argumentos transferidos y coloca en la misma cualquier valor a retornar. Luego el programa invocante lo recupera.

El registro de la CPU conocido como puntero a la pila (stack pointer) contiene la dirección de la cabeza de la pila.

![[Untitled 23.png|Untitled]]

Si tuviéramos que llamar a diferentes subrutinas dentro de subrutinas podemos guardar el %r15 (registro de enlace)  también en una pila para que no se nos sobreescriba y lo perdamos.

![[Untitled 24.png|Untitled]]

![[Untitled 25.png|Untitled]]

![[Untitled 26.png|Untitled]]

# Macro

Una macro es una secuencia de código que voy a repetir en varias partes de mi programa a la que le puedo asignar un nombre para que al compilar se reemplace.

Se diferencia con la subrutina en que no se hace ningún call, por lo que no hay saltos.

Los códigos con macro pesan más, porque se reescribe el mismo código muchas veces.

# Localización de las variables:

- Registros
- “Segmento de datos” Ram. Lo que señalamos con etiquetas, la memoria de usuario.
- Stack (RAM).