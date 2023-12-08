Necesitaremos un archivo **.h** en el que escribiremos la firma de las funciones que queremos en nuestra biblioteca de la forma

```c
/* File aritmetica .h */
# ifndef ARITMETICA_H
# define ARITMETICA_H

int sumar (int numero_uno , int numero_dos );// prototipo de la funcion sumar

# endif /* ARITMETICA_H */
```

Luego, en un archivo **.c** escribimos el contenido de las funciones de la siguiente forma

```c

/* File aritmetica .c */
# include "aritmetica .h"

int sumar (int numero_uno , int numero_dos ){
	return numero_uno + numero_dos ;
}
```

Luego para poder utilizar esta biblioteca en nuestro programa, escribimos el header file entre comillas 

```c
/* File Ejemplo .c */
# include < stdio .h >
# include " aritmetica .h"

int triplicar (int numero ){
	return sumar ( numero , sumar ( numero , numero )) ;
}

int main(){
	int valor = 1;
	int suma , triple ;
	suma = sumar ( valor , valor ) ;
	triple = triplicar ( valor );
	printf ("\n La suma es : %d y el triple es %d \n\n", suma , triple );

	return 0;
}
```

A la hora de compilar este código lo tendremos que hacer de la forma:

```c
gcc Ejemplo.c aritmetica.c -o ejemplo
```

teniendo el archivo **.h** en el directorio.