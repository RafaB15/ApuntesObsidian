Cuando se quiere pasar de tener un archivo de código escrito en algún lenguaje de alto nivel a tener un archivo ejecutable, el [[Sistemas Operativos/Resumen/Sistema Operativo|sistema operativo]], mediante el [[Sistemas Operativos/Resumen/Kernel|kernel]], se encargan de esto.
# Preprocesamiento

El preprocesador (cpp) modifica el código fuente original de un programa escrito en C de acuerdo a las directivas que comienzan con un caracter (#). El resultado de este proceso es otro programa en C con la extensión *.i*.

Esto, por ejemplo, intercambia cada instancia de una constante por el valor de esta. Es como lo que sucedía con las macros en assembler.

# Compilación 

El compilador (cc) traduce el programa *.i* a un archivo de texto *.s* que contiene un programa en lenguaje assembly.

# Ensamblaje 

El ensamblador (as) traduce el archivo *.s* en instrucciones de lenguaje de máquina empaquetándolas en un formato conocido como programa objeto realocable. Este es almacenado en un archivo con extensión *.o*.

A compiler converts that code into a sequence of machine instructions and stores those instructions in a file, called the program’s executable image. The compiler also defines any static data the program needs, along with its initial values, and includes them in the executable image.

# Link edición

El linker se encarga de mezclar archivos objeto (*.o*) que contengan la información de las diferentes funciones siendo usadas en el programa principal (como las funciones de la biblioteca standard de C que es provista por cualquier compilador del lenguaje, o archivos que nosotros creamos con funciones externas) en un único **archivo objeto ejecutable**.

![[Sistemas Operativos/Resumen/images/Proceso de Compilación.png]]
