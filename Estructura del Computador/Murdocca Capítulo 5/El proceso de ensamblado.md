Se conoce como proceso de ensamblado al proceso de traducción de un programa expresado en lenguaje simbólico.

Es un proceso lineal y relativamente simple, dado que hay una relación directa y unívoca entre sentencias del lenguaje simbólico y sus correspondientes expresiones en el lenguaje de máquina.

Los ensambladores comerciales deben ofrecer, al menos, las siguientes prestaciones:

- Permitir que el programador especifique la ubicación de las variables y programas al momento de la ejecución.
- Ofrecerle al programador la posibilidad de inicializar los valores de los datos en memoria antes de la ejecución del programa.
- Proveer expresiones nemotécnicas en el lenguaje de progrmaación para todas las instrucciones del lenguaje de máquina y modos de direccionamiento, y traducir lassentencias válidas del lenguaje simbólico hacia sus valores binarios equivalentes en el lenguaje absoluto.
- Permitir el uso del rótulos simbólicos para identificar o representar direcciones y constantes.
- Ofrecerle al programador una forma de especificar la dirección de comienzo de un programa si existiera.
- Ofrecer cierto grado de cálculo al momento del ensamblado.
- Incluir un mecanismo que permita la definición de variables en un programa escrito en lenguaje simbólico y el uso de las mismas en otro programa ensamblado por separado.
- Proveer la expansión de macro rutinas, o sea, rutinas que puedan definirse una vez y utilizarse tantas veces como sea necesario.

Al ensamblar un programa se utilizan los formatos de codificación para ARC.

# El proceso de ensamblado y los ensambladores de dos pasadas

La mayoría de los ensambladores recorren dos veces el texto escrito en lenguaje simbólico. 

En la primera pasada el ensamblador se dedica a determinar las direcciones de todos los datos e instrucciones del programa y a seleccionar qué instrucción del lenguaje de máquina debe generarse para cada instrucción del lenguaje simbólico, pero sin generar aún el código de máquina.

Estas direcciones se determinan en el momento del ensamblado del programa mediante el contador de posición (location counter). 

.org cambia su valor.

Durante la primera pasada el ensamblador realiza también cualquier operación aritmética necesaria e inserta las definiciones de todos los rótulos y constantes en una tabla de símbolos.

Principalmente se requiera una segunda pasada para poder utilizar símbolos que se definen luego en el programa (referencia previa). Estos en la primera pasada son colocados en la tabla de símbolos, por lo que en la segunda pasada se pueden insertar en el código sin ningún problema.

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de ensamblado/Untitled.png|Untitled]]

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de ensamblado/Untitled 1.png|Untitled]]

Como técnica general, el proceso de ensamblado se lleva a cabo leyendo las sentencias del lenguaje simbólico en forma secuencial, desde la primera hasta la última, y generando el código de máquina para cada una de las sentencias.

Ejemplo de referencia previa

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de ensamblado/Untitled 2.png|Untitled]]

# El proceso de ensamblado y la tabla de símbolos

En la primera pasada de un proceso de ensamblado de dos pasadas se crea una ***tabla de símbolos***. Un símbolo puede ser un rótulo o un nombre simbólico que se refiere a un valor utilizado durante el proceso de ensamblado.

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de ensamblado/Untitled 3.png|Untitled]]

Si encuentra un símbolo y aún no tiene un valor asignado porque se hace más abajo , su entrada en la tabla de símbolos se declara “indeterminado”.

Si al final de la primera pasada quedaran todavía rótulos sin definir, existe un error en el programa, el ensamblador señala los ´simbolos que no fueron definidos y termina.

# Tareas finales del programa ensamblador

Terminado el proceso de traducción, el ensamblador debe agregarle al módulo traducido información adicional para uso de los programas de enlace y carga.

- El nombre y tamaño del módulo.
- La dirección del símbolo del comienzo, si es que se define alguno en le módulo.
- Información acerca de símbolos globales y externos.
- Información acerca de las rutinas de biblioteca a las que el módulo hace referencia.
- Los valores de cualquier constante que deba cargarse en memoria.
- Información de reubicación.

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de ensamblado/Untitled 4.png|Untitled]]

# Enlace y carga

La mayoría de aplicaciones de cualquier tamaño tienen una cantidad de módulos que han sido compilados o ensamblados por separado.

Un ***editor de enlace,*** o ***linker,*** es un programa que combina programas ensamblados por separado (llamados ***módulos objeto***) en un único programa (llamado ***módulo de carga***).

El linker resuelve todas las referencias globales y externas y reubica las direciones de los diferentes módulos. El módulo de carga puede ser cargado en memoria por medio de un ***cargador***. 

## Enlace (linking)

Al combinar módulos ensamblados o compilados por separado en un módulo de carga el programa de enlace debe:

- Resolver referencias de direcciones externas a los módulos a medida que los vincula.
- Reubicar cada módulo por medio de la combinación más apropiada de los mismos.
- Especificar el símbolo de comienzo del módulo de carga.
- Si el modelo de memoria incluye más de un segmento de memoria, debe especificar los contenidos e identidades de los diversos segmentos.

### Resoluciones de referencias externas

Las directvas .global y .extern ayudan a diferenciar los tipos de variables al linker.

![[Estructura del Computador/Murdocca Capítulo 5/El proceso de ensamblado/Untitled 5.png|Untitled]]

### Reubicación

Fijémonos en la figura anterior, en la que ambos programas empiezan en la posición 2048. Obviamente no pueden estar los dos en la misma posición de memoria. 

Al ensamblar los dos módulos por separado no se puede saber acerca de este conflicto durante el proceso de traducción.

Es por esto que el ensamblador define como reubicables a aquellos símbolos que pueden admitir que sus direcciones sean modificadas durante el proceso de enlace (fig 5.7).

La idea es que un programa ensamblado en una dirección inicial, como 2048, pueda cargarse no a partir de ella sino a partir de por ejemplo 3000. 

Para permitir esta modificación todas las referencias a direcciones reubicables incluidas en el programa deben incrementarse 3000 - 2048 = 952. La reubicación se realiza a través del programa linker.

Las direcciones absolutas, no reubicables (como la dirección más alta para la pila $2^{31}-4$) se mantiene sin modificaciones independiéntemente del origen de la carga.

## Carga

El ***cargador (loader)*** es un programa que ubica el módulo de carga en la memoria principal. Debe cargar lo diversos segmentos de memoria con los valores apropiados e inicializar ciertos registros, como el puntero de pila %sp y el contador de programa &pc, a sus valores iniciales.

El cargador modifica las direcciones reubicables que encuentra dentro de un módulo de carga dado para permitir la coexistencia en memoria de varios programas en forma simultánea.

### Bibliotecas de enlace dinámico (DLL)