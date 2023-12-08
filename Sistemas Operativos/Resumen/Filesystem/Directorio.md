- Como los [[Archivo|archivos]], también tiene un nombre de bajo nivel ([[Inode Number|inode number]]).
- Contiene una lista de pares `(nombre_legible_usuario, inode_number)`, refiriéndose a otros directorios o archivos que este contiene.
- Poniendo muchos directorios dentro de directorios obtenemos una **jerarquía de directorios** o **árbol de directorios**.
- En Unix, la jerarquía de directorios empieza en el **root directory** (**/**)
- Los paths absolutos empiezan con **"/"**.
- Dentro de un directorio:
	- **"."** se refiere al mismo directorio
	- **".."** se refiere a su directorio padre.


# Interfaz

## Creación de directorios

Se hace con la [[System Call]] mkdir con la flag O_CREAT.

## Lectura de directorios

Se usa la [[System Call]] opendir pasándole como parámetro el directorio que queramos leer (puede ser **"."**). Esta función devuelve un puntero a una estructura del tipo **DIR**.

Luego usamos la [[System Call]] readdir tantas veces como archivos haya hasta que nos devuelve NULL.

Terminamos usando la syscall closedir.

## Eliminación de directorios

Se utiliza la syscall `rmdir`. Como requerimiento, el directorio tiene que estar vacío para poder borrarlo (tener referencias únicamente a **"."** y a **".."**).