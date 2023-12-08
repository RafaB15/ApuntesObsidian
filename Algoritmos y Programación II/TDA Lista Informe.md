$\text{[7541/9515] Algoritmos y Programación II}$

                                                   $\text{Segundo cuatrismestre de 2021}$     

                       $\def\arraystretch{1.4}\begin{array}{|c|c|}\hline

\text{\textbf{Alumno:}}  &
\text{\textbf{Rafael Francisco Berenguel Ibarra}}

\\\hline

\text{Padrón:} &
\text{108225}

\\\hline

\text{Email:} &
\text{rafaelberenguel15@gmail.com}

\\\hline\end{array}$

## 1. Introducción:

El TDA lista consistía en la implementación de tres tipos de datos abstractos que tendría que poder controlar alguien, a través de diversas funciones, sin necesariamente saber cómo funciona todo por debajo.

Estos TDAs eran **Lista**, **Cola** y **Pila** y en su implementación usaremos otro TDA llamado **nodo**.

## 2. Teoría:

**¿Qué es una lista y cómo funciona?**

Una lista es un tipo de dato abstracto que consiste en una secuencia de elementos.

Se debe poder acceder y eliminar elementos en cualquier posición de la lista independientemente de cual sea el primer elemento y cual el último.

Esta se puede implementar de distintas maneras, entre las que están implementarla con un vector estático, que está almacenado en el **stack** y tiene una cantidad predefinida de elementos; implementarla con un vector dinámico, que está almacenado en el **heap** y se le puede aumentar el tamaño; e implementarla con nodos, los cuales se almacenan en el **heap** al igual que el vector dinámico, pero a diferencia de este, sus elementos pueden no estar almacenados de manera consecutiva y cada uno tiene información acerca del nodo que le precede y el que le sigue.

**¿Qué es una cola y como funciona?**

Una cola es un tipo de dato abstracto que consiste en una secuencia de elementos.

Este TDA tiene una estructura del tipo F.I.F.O., que son las siglas de ***first in first out***. Esto significa que lo que metamos primero a la cola será lo primero que saldrá. 

En una cola, solo tendremos acceso al frente de esta, que es el elemento que estuvo en la cola por más tiempo y que es el próximo que saldrá.

Esta la podremos implementar de diferentes maneras. Al igual que la lista, podemos hacer uso de vectores estáticos y dinámicos, sin embargo, dado que agregamos elementos de un lado y los sacamos del otro, existe otra implementación llamada **cola circular**, en la cual el último elemento del vector es seguido del primero. Esta implementación ayuda a lidiar con tener que reposicionar los elementos del vector para aprovechar el espacio. También podemos utilizar nodos de la misma manera que con la lista.

**¿Qué es una pila y como funciona?**

Una pila es un tipo de dato abstracto que consiste en una secuencia de elementos.

Este TDA tiene una estructura del tipo L.I.F.O, que son las siglas de ***last in first out***. Esto significa que lo que metamos último a la pila será lo primero que sacaremos de esta.

En una pila, solo tendremos acceso al tope de esta, que es el último elemento que ingresamos a la pila y que es el próximo que saldrá.

La podemos implementar con un vector estático, teniendo espacio limitado y almacenándola en el **stack**; con un vector dinámico, teniendo una cantidad de espacio predefinido pero pudiendo ampliarlo ya que se encuentra en el **heap**; y con **nodos**, no teniendo un límite de espacio ni la necesidad de que estos se almacenen uno al lado del otro.

## 3. Detalles de implementación:

Los archivos que precisaremos para poder usar todos los TDA son **lista.h, lista.c, cola.h, cola.c, pila.h, pila.c.** 

También tenemos los archivos **pa2mm.h, ejemplo.c** y **pruebas.c** que podremos usar junto a **makefile** para testear nuestro archivo (la función **pruebas.c** implementada por nosotros).

La implementación de lista es la siguiente

### Lista:

```c
lista_t* lista_crear();
```

Devuelve una dirección a un bloque de memoria en el **heap**, reservado a través de **calloc**, con lo cual los punteros del **struct** estarán inicializados a **NULL** y los enteros a **0**.

**Calloc** devuelve **NULL** en caso de no encontrar memoria, por lo que eso es lo que devolverá la función en caso de error.

![[Algoritmos y Programación II/TDA Lista Informe/Untitled.png|Untitled]]

                                        Diagrama 1: Un puntero a lista apunta a una lista en el heap

```c
lista_t* lista_insertar(lista_t* lista, void* elemento);
```

Inserta un nuevo elemento al final de la lista. Lo primero que hacemos es crear un **nodo** y asignarle memoria y el elemento.  Asignamos este nuevo **nodo** a la posición siguiente del que era el último nodo, y hacemos de este el nuevo último nodo. En caso de que este sea el primer elemento que le estemos insertando a la lista, también haremos que el puntero **primer_nodo** le apunte.

Aumento la **cantidad** y regreso la lista.

![[Algoritmos y Programación II/TDA Lista Informe/Untitled 1.png|Untitled]]

                                   Diagrama 2: Asignar nuevo elemento cuando no hay elementos

![[Algoritmos y Programación II/TDA Lista Informe/Untitled 2.png|Untitled]]

                              Diagrama 3: Asignar nuevo elemento cuando hay elementos

```c
nodo_t* lista_buscar_nodo(nodo_t* nodo_actual, size_t posicion);
```

Esta es una función auxiliar que usamos bastante en otras funciones. Lo que hace es buscar y devolver el **nodo** en la posición pedida empezando a contar desde el **nodo_actual** que le pasamos por parámetro.

```c
lista_t* lista_insertar_en_posicion(lista_t* lista, void* elemento, size_t posicion);
```

Si al posición es mayor o igual al tamaño de la lista, directamente llamo a **lista_insertar**, ya que lo tendré que insertar al final. 

Si ese no es el caso, reservo memoria para un **nodo**, y al momento de asignarlo tengo dos casos distintos. 

Si la posición en la que quieren ingresar el nuevo nodo es **cero** tengo que hacer que el nuevo nodo apunte al primer nodo de la lista y luego cambio el puntero **nodo_inicio** para que apunte al nuevo nodo. Esto funciona incluso si el tamaño de la lista fuera cero, porque en ese caso **nodo_inicio** estaría apuntando a **NULL**, y hacer que el nuevo nodo apunte a **NULL** está bien pues es el único elemento.

Si la posición no es cero, entonces tendré que hacer uso de la función **lista_buscar_nodo** para encontrar el nodo que está antes de la posición en la que insertaré el nuevo nodo. Como este tiene la dirección del elemento que está en la posición que quiero ocupar se la asigno al nuevo nodo como **siguiente**. Luego asigno la dirección del nuevo_nodo como el siguiente del nodo que encontré con **buscar_nodo**. 

Aumento la **cantidad** y regreso la lista. 

```c
void* lista_quitar(lista_t* lista);
```

Libero el último nodo y disminuyo la cantidad después de haber obtenido la dirección del elemento que este tenía. 

Luego, si no queda ningún elemento hago que nodo_inicio y nodo_final apunten a NULL y regreso el elemento.

Si quedan elementos utilizo **lista_buscar_nodo** para encontrar el nuevo final y se lo asigno a **nodo_fin**. Luego regreso el elemento.

![[Algoritmos y Programación II/TDA Lista Informe/Untitled 3.png|Untitled]]

                                                     Diagrama 4: Lista antes de borrar una elemento

![[Algoritmos y Programación II/TDA Lista Informe/Untitled 4.png|Untitled]]

                              Diagrama 5: Eliminamos el último elemento y hacemos un puntero que 

                                                                                    apunte al nuevo último

```c
void* lista_quitar_de_posicion(lista_t* lista, size_t posicion);
```

Si la posición es mayor o igual al tamaño de la lista - 1 entonces se puede referir a quitar el último elemento o una posición que no existe, por lo que directamente llamo a **lista_quitar**.

Si ese no es el caso, tenemos dos posibilidades.

Si quieren quitar el elemento en la posición cero, hago que mi auxiliar nodo_a_quitar apunte al primer elemento y hago que **nodo_inicio** apunte al segundo elemento.

Si el elemento que quieren quitar no está al inicio, utilizo **lista_buscar_nodo** para encontrar el elemento antes de la posición que quiero quitar, asigno su **siguiente** al auxiliar **nodo_a_quitar** y luego hago que apunte hacia el siguiente elemento en la lista.

 Luego, en ambos casos, guardo la dirección al elemento a remover, libero el nodo, disminuyo la cantidad y regreso el elemento.

```c
void* lista_elemento_en_posicion(lista_t* lista, size_t posicion);
```

Utiliza **lista_buscar_nodo** para encontrar el nodo en la posición pedida y devuelve su elemento.

```c
void* lista_primero(lista_t* lista);
```

Devuelve el elemento en el primer nodo de la lista.

```c
void* lista_ultimo(lista_t* lista);
```

Devuelve el elemento del último nodo de la lista.

```c
bool lista_vacia(lista_t* lista);
```

Devuelve true si la lista tiene cero elementos y false en caso contrario.

```c
size_t lista_tamanio(lista_t* lista);
```

Devuelve la cantidad de elementos de la lista.

```c
void liberar_nodos(nodo_t* nodo);
```

Es una función recursiva que libera todos los nodos que se apuntan en una lista. Su condición de corte es cuando el siguiente nodo es **NULL**, lo cual significa que llegamos al final de la lista.

```c
void lista_destruir(lista_t* lista);
```

Si hay elementos en lista, los libera con **liberar_nodos**. Luego libera la lista.

```c
lista_iterador_t* lista_iterador_crear(lista_t* lista);
```

Devuelve un puntero a un elemento de tipo **lista_iterador** en el **heap**, con la lista pasada por parámetro en el campo lista y el primer elemento de la lista en el campo corriente.

```c
bool lista_iterador_tiene_siguiente(lista_iterador_t* iterador);
```

Devuelve true si el elemento en corriente no es **NULL**, y false en caso contrario.

```c
bool lista_iterador_avanzar(lista_iterador_t* iterador);
```

Hay un primer if en el que, si corriente es NULL, se devuelve false.

Luego avanzo hacia el siguiente elemento y lo devuelvo.

Lo hago de esta forma porque así, si llego al final de la lista, corriente pasa a ser NULL y al devolver NULL este será falso. Además, como ahora corriente es NULL, **lista_iterador_elemento_actual** devolverá NULL si se usa.

```c
void* lista_iterador_elemento_actual(lista_iterador_t* iterador);
```

Si corriente no es **NULL**, devuelve el elemento al que este apunta.

```c
void lista_iterador_destruir(lista_iterador_t* iterador);
```

Libera el iterador.

```c
size_t lista_con_cada_elemento(lista_t* lista, bool (*funcion)(void*, void*), void *contexto);
```

Primero creamos un iterador de la lista pasada por parámetro.

Pongo el elemento del nodo actual en una variable para usarla en la función pasada por parámetro. También declaro un contador.

Mientras lista_iterador_tiene_siguiente  y la función (a la que le paso el elemento actual como parámetro) me den true, aumento el contador, avanzo el iterador de la lista y actualizo el elemento actual.

Luego libero el iterador y regreso el contador.

### Cola:

Para la cola, llamamos mucho a las funciones de la lista, casteando cualquier instancia en la que necesitemos un elemento de tipo **lista_t** a **cola_t**.

```c
cola_t* cola_crear();
```

Devolvemos la dirección que nos devuelve **lista_crear** casteada a una **cola_t***.

```c
cola_t* cola_encolar(cola_t* cola, void* elemento);
```

Devolvemos la dirección que nos devuelve **lista_insertar** casteada a una **cola_t***. Usamos esta función para poner los elementos más recientes al final de la lista.

```c
void* cola_desencolar(cola_t* cola);
```

Devolvemos el elemento que nos devuelve **lista_quitar_de_posicion**. Usamos esta función ya que, como estamos ingresando los elementos al final de la lista, los tendremos que sacar al inicio de esta. Así que la posición de la que saco siempre es la primera, **cero**.

```c
void* cola_frente(cola_t* cola);
```

Devuelve el primer elemento de la cola a través de la función **lista_primero**. Este será el primer elemento a sacar.

```c
size_t cola_tamanio(cola_t* cola);
```

Devuelve el tamaño de la cola a través de la función **lista_tamanio**.

```c
bool cola_vacia(cola_t* cola);
```

Devuelve true si la cola está vacía y false en caso contrario. Lo averigua usando al función **lista_vacia**.

```c
void cola_destruir(cola_t* cola);
```

Libera la memoria de toda la cola a través de la función **lista_destruir**.

### Pila:

Para la pila, también llamamos mucho a las funciones de la lista, casteando cualquier instancia en la que necesitemos un elemento de tipo **lista_t** a **pila_t**.

```c
pila_t* pila_crear();
```

Devolvemos la dirección que nos devuelve lista_crear casteada a una **pila_t***.

```c
pila_t* pila_apilar(pila_t* pila, void* elemento);
```

Devolvemos la dirección a **pila_t** que nos devuelve la función **lista_insertar_en_posicion**.  Utilizo esta función para apilar porque mi tope va a ser el inicio de la lista, así que inserto en la primera posición, **cero**. ¿Y por qué no puse el tope al final de la lista? La respuesta está en la siguiente función.

```c
void* pila_desapilar(pila_t* pila);
```

Devuelve el elemento que devuelve la función **lista_quitar_de_posicion**. Utilizo esta función para sacar el primer elemento, ya que como los nuevos elementos los inserto por el inicio, ese será el más reciente. 

En un principio lo intenté hacer por el final de la lista, sin embargo había un problema, la complejidad para quitar un elemento al final de la lista es **O(n)**, pero sacar un elemento de una pila debería ser **O(1)**. Por eso lo hago por el inicio, en donde esto se cumple.

```c
void* pila_tope(pila_t* pila);
```

Devuelve el elemento al inicio de la pila a través de la función **lista_primero**.

```c
size_t pila_tamanio(pila_t* pila);
```

Devuelve el tamaño de la pila a través de la función **lista_tamanio**.

```c
bool pila_vacia(pila_t* pila);
```

Devuelve true si el tamaño de la pila es cero y false en caso contrario. Esto lo hace a través de la función **lista_vacia**.

```c
void pila_destruir(pila_t* pila);
```

Libera la memoria de toda la pila a través de **lista_destruir**.