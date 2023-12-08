 - Es una abstracción del sistema operativo que provee datos persistentes con un nombre.
	 - **Datos persistentes:** Se almacenan hasta que son explícitamente borrados, incluso si la computadora tiene un desperfecto con la alimentación eléctrica. 
- Es el encargado dentro de un [[Sistema Operativo|sistema operativo]] de manejar [[Archivo|archivos]], [[Directorio|directorios]] y [[Links simbólicos|links simbólicos]].
- Permite a los usuarios organizar sus datos para que persistan a través de un largo periodo de tiempo.
- El file system posee una tabla de todos los **Inodos** que se encuentran en el sistema de archivos. Se almacena:
	- El tipo de archivo
	- Un puntero a la lista de los [[Lock|locks]] que se mantienen sobre ese archivo.
	- otras propiedades del archivo.


# Link y Unlink

- Cuando el File System crea un [[Archivo|archivo]], este utiliza la [[System Call]] `link` para asociar un nombre legible por los usuarios al [[Inode Number|inode number]] del archivo. 
- Esto crea un **hard link** entre el nombre y los contenidos del archivo identificado con su inode number.
- Utilizando el comando `ln` en la terminal podemos asignar otro nombre que referencie al mismo [[Inode Number|inode number]], usando internamente `link`. 
- Al utilizar `rm` para borrar un archivo (internamente se utiliza `unlink`), si borramos uno de los dos nombres legibles que referencian a un mismo inode number, el otro seguirá referenciando al mismo archivo.
- Cuando se borra un nombre que referencia a un archivo se chequea cuantas referencias existen. Cuando este número llega a cero es cuando el file system verdaderamente libera el [[Inode Number|inode number]] y sus bloques de memoria relacionados.
- Podemos ver cuantas referencias tiene un archivo utilizando `stat`.
- La mayoría de fs tienen mecanismos para permitir y prohibir compartir archivos. Estos controles son representados a través de bits de permiso.

# Creación de File Systems

- Se hace con la herramienta `mkfs`, a la que se le pasa como parámetro un dispositivo como una partición de disco y un tipo y se creará un fs vacío.
- Para que el nuevo fs esté disponible se utiliza `mount`, con lo que ahora el **root** del file system estará en el directorio en el que esté fue montado. Mount unifica todos los file systems en un solo árbol, haciendo que nombrar cosas sea uniforme y conveniente.
- Accediendo al programa mount, podemos ver todos los fs que están en nuestro sistema.

# Virtual File System

- El VFS es el subsistema del [[Kernel]] que implementa la interfaz que tiene que ver con los archivos y el sistema de archivos provisto a los programas corriendo en modo usuario.
- El VFS provee syscalls para que los programas puedan interactuar con los diferentes file systems sin necesariamente saber como están constituidos por debajo.
- Todos los sistemas de archivos deben basarse en VFS para :
	- coexistir
	- inter-operar
- Esto habilita a los programas a utilizar las [[System Call|system calls]] de Unix (open, read, write) para leer y escribir en diferentes sistemas de archivos y diferentes medios.

![[Virtual File System Representation.png]]

*Nota: ext3 y ext2 son dos file systems distintos*
*cp es current program*

- Es un tipo genérico de interfaz para cualquier tipo de file system (ext3, ext2, etc).
- Esta **capa de abstracción** habilita a Linux a soportar sistemas de archivos diferentes, incluso si difieren en características y comportamiento.

![[Capa de abstracción VFS.png]]

- Trabaja mediante la definición de interfaces conceptualmente básicas y de estructuras que cualquier sistema de archivos soporta.

![[Cadena de eventos VFS.png]]

## Objetos

- VFS presenta una serie de estructuras que modela un file system. Estos objetos son:
	- Super bloque: Representa un sistema de archivos.
	- Inodo: Representa a un determinado archivo
	- Dentry: Representa una entrada de directorio, que es un componente simple de un path.
	- File: Representa a un archivo asociado a un determinado proceso.

![[Objetos VFS.png]]

# Volumen

- Es una abstracción que corresponde a un disco lógico. Es una colección de recursos físicos de almacenamiento.

![[Volumen.png]]

- **Punto de montura:** Es un punto en el cual el root de un volumen se engancha dentro de la estructura existente de otro file system

![[Puntos de montura.png]]

# Comandos

- cat
- rm
- fstat
- tee
- tousc
- ls

# Implementación VSFS

- **VSFS** $\to$ Very Simple File System
- Es importante pensar en las **estructuras de datos** y los **métodos para acceder a estas**.

## Organización general

- Dividimos la memoria en una serie de bloques, todos de igual tamaño.
- Reservamos la mayoría de los bloques para *user data*.
- También necesitamos reservar espacio en el disco para los **inodos** en una **inode table**.
	- Los inodos son estructuras que guardan:
		- El inode number.
		- Los bloques de memoria que conforman al inodo.
		- Su tamaño
		- Su dueño
		- Los derechos de acceso.
		- Tiempos de acceso y modificación.
- También necesitaremos espacio para estructuras que nos hablen del estado de las listas de inodos y datos de usuario. Podemos usar **bitmaps** para nuestro caso.
- Finalmente, necesitaremos espacio para el **superblock**. El super bloque contiene información acerca de este file system en específico, como la cantidad de inodos y bloques de datos que tiene. También puede tener magic numbers para identificar el tipo de file system.
- La estructura finalmente queda así:

![[Estructura vsfs.png]]

## Inode

- Es una de las estructuras más importantes para un fs.
- Abreviación de *index node*. 
- Cada inodo se identifica por un número llamado el i-number.
- Teniendo el i-number, tendríamos que poder localizar el inodo en el disco.

## Organización de directorios

- Los directorios contienen una lista de `(entry_name, inode_number)`
- Como los nombres pueden varias en tamaño esa información a veces se incluye también.
- Cada directorio también contiene la información de **"."** y **".."**.

![[Contenido de un directorio.png]]

- Los directorios son tratados como un tipo especial de archivo, por lo que también tienen inode numbers.

## Manejo del espacio libre

- Si utilizamos un bitmap, al momento de querer crear un nuevo archivo buscaremos algún espacio libre para un nuevo inode y si lo encontramos lo tomamos. Lo mismo hacemos con el bitmap con bloques de memoria.

