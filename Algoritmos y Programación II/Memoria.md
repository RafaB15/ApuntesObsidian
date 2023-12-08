La memoria se divide en:

- **Stack:** Aquí se almacenan las variables locales durante la ejecución de nuestro programa. Es de       tamaño fijo.
- **Heap:** Es memoria dinámica. Nosotros la reservamos manualmente en tiempo de ejecución y la liberamos antes de finalizar nuestro programa.
- **BSS:** Datos no inicializados. Memoria estática.
- **Data:** Constantes globales, variables externas y valores literales del programa. Memoria estática.
- **Text:** Código fuente del programa. Memoria estática.

## Memoria dinámica:

Usaremos dos funciones de stdlib.h para reservar y liberar memoria del heap:

- malloc()
- free()

### Malloc:

Reserva "size" bytes y devuelve un puntero a la memoria reservada. La memoria no está
inicializada. Si size es 0, devuelve NULL en la mayoría de los casos.

### Free:

Libera el espacio de memoria, apuntado por un puntero, que debe haber sido devuelto por malloc(), calloc() o realloc().

```c
#include <stdlib.h>

int main(){
	int* puntero;
	puntero = malloc(sizeof(int));
	// Opero con el puntero
	free(puntero);
	return 0;
}
```

Si queremos crear una función que devuelva una dirección de memoria a algo, tendremos que usar memoria dinámica, pues cualquier variable que creemos dentro de la función se destruirá al finalizar esta, lo que significa que devolveremos una dirección de memoria que apunta a basura, cosa que no pasa si es memoria del heap.

### Calloc():

Reserva memoria para cualquier arreglo de **n** elementos de tamaño **size** bytes y devuelve un puntero al inicio de la memoria. Toda la memoria se setea con ceros.

```c
#include <stdlib.h>

int main(){
	int* puntero;
	int cantidad = 5;

	puntero = calloc(cantidad, sizeof(int));
	// Opero con el puntero
	free(puntero);
	return 0;
}
```

### Realloc:

Modifica el tamaño del bloque de memoria apuntado por el puntero en size bytes. La memoria que se va a relocalizar tiene que haber sido separada con malloc, calloc o realloc. 

Devuelve un puntero a la memoria relocalizada.

```c
#include <stdlib.h>

int main(){
	int* puntero;
	puntero = malloc(sizeof(int))
	puntero = realloc(puntero, 2*(sizeof(int)));
  //ahora el puntero tiene el doble de memoria disponible.
	free(puntero);
	return 0;
}
```

### Reallocarray:

Es realloc pero relocalizamos a n elementos de size bytes.

```c
#include <stdlib.h>

int main(){
	int* puntero;
	puntero = malloc(sizeof(int))
	puntero = reallocarray(puntero, 2, sizeof(int));
  //ahora el puntero tiene el doble de memoria disponible.
	free(puntero);
	return 0;
}
```