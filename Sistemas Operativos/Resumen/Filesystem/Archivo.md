- Es un arreglo lineal de bytes, los cuales se pueden leer o escribir.
- Cada archivo tiene un nombre de bajo nivel conocido como [[Inode Number|inode number]].
- El [[Sistema Operativo|SO]] no conoce la estructura del archivo, pero el [[File System]] se encarga de guardarlo de manera persistente.
- Los nombres de los archivos normalmente tiene dos partes separados por un punto.
	- La primera parte es un nombre arbitrario.
	- La segunda parte indica el tipo del archivo.
- Un archivo tiene dos partes
	- **Metadata**: Información acerca del archivo que es entendida y manejada por el [[Sistema Operativo|SO]]. Ej: Tamaño, hora de modificación, dueño, información de seguridad.
	- **Data**: Puede ser cualquier tipo de información representada por un arreglo de bytes.

# Estructura

Una estructura posible de un archivo abierto puede ser la siguiente

```c
struct file {
	int ref;
	char readable;
	char writable;
	struct inode* ip;
	unit off;
};
```

# Interfaz

## Creación de archivos

Se hace con la [[System Call]] open con la flag O_CREAT.

Devuelve un [[File Descriptor]] del archivo creado.

## Lectura de archivos

Se hace con la [[System Call]] write, pasándole el [[File Descriptor]].

## Escritura de archivos

Se hace con la [[System Call]] read, pasándole el [[File Descriptor]].

## Eliminación de archivos

Se hace con la `rm`. Esta operación internamente utiliza la syscall [[File System#Link y Unlink|unlink]].  
