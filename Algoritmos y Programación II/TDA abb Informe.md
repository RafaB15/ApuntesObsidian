$\text{[7541/9515] Algoritmos y Programación II}$

                                                                       

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

El TDA abb consistía en la implementación de un árbol binario de búsqueda, que podría ser controlado por un usuario, sin necesidad de que este sepa como funciona por debajo, a través de diversas funciones escritas por nosotros.

## 2. Teoría:

### **¿Qué es un árbol?**

Un árbol se podría definir como una  **colección de nodos**, los cuales son un tipo de dato abstracto que almacena un elemento y direcciones de memoria a otros nodos.

Tenemos un nodo desde el que empezamos al que llamamos **nodo raíz.** Ese nodo luego va a apuntar a otros nodos, a los que llamamos **hijos**, los cuales a su vez también apuntan a otros nodos.

Un nodo que apunta a otro nodo se conoce como su **padre** y dos nodos con el mismo padre se conocen como nodos **hermanos**. De la misma forma podemos definir a los nodos **abuelos** y nodos **nietos**. 

### **¿Qué es un árbol binario?**

Un árbol binario es un árbol en el que cada nodo puede tener como máximo dos hijos.

### **¿Qué es un árbol binario de búsqueda?**

Un árbol binario de búsqueda es un árbol binario donde se cumple que:

- Si existe el nodo izquierdo, su elemento es **menor** al del nodo padre.
- Si existe el nodo derecho, su elemento es **mayor** al del nodo padre.
- Los árboles que tienen como raíz a los elementos derecho e izquierdo son también arboles binarios de búsqueda.

Al tener esta relación entre los nodos, se hace posible crear funciones que los recorran con distintos criterios, en distintos órdenes.

### **¿Por qué es importante diferenciar todos estos casos?**

La cantidad de tipos de árboles es muy grande. Hay algunos con varios hijos, otros con solo dos; algunos que tienen relación de padres a hijos; otros que la tienen también con sus hermanos. 

Como hay árboles, como el **árbol B**, que tienen más de dos hijos, no todos los árboles son binarios. Y hay árboles binarios que tienen distintas características al árbol binario de búsqueda, como el **árbol rojo negro**.

También podemos buscar con una eficiencia que se asemeja a la de la búsqueda binaria, con complejidad logarítmica. 

Por eso es muy importante hacer distinción de cada caso.

## 3. Detalles de implementación:

Los archivos que precisaremos para poder controlar el TDA son **abb.h** y **abb.c.**

También tenemos los archivos **pa2mm.h, ejemplo.c** y **pruebas.c** que podremos usar junto a **makefile** para testear nuestro archivo (la función **pruebas.c** implementada por nosotros).

Las funciones elaboradas fueron:

```c
abb_t* abb_crear(abb_comparador comparador);
```

Esta función, en caso de recibir un comparador válido, devuelve la dirección de memoria de un elemento de tipo **abb_t**, con el campo comparador inicializado con el que nos pasaron por parámetro.

![[Algoritmos y Programación II/TDA abb Informe/Untitled.png|Untitled]]

                                    **Diagrama 1: Creación  e inicialización de un árbol**

```c
abb_t* abb_insertar(abb_t* arbol, void* elemento);
```

Si el árbol es válido, se crea en el **heap** un nuevo **nodo** en el que almacenamos el elemento que queremos insertar.

Luego utilizamos la función **insertar_nuevo_nodo** para insertar el nuevo nodo en nuestro árbol.

Aumentamos el tamaño del árbol y lo devolvemos.

![[Algoritmos y Programación II/TDA abb Informe/Untitled 1.png|Untitled]]

                                            **Diagrama 2: Creación del nuevo nodo**

```c
nodo_abb_t* insertar_nuevo_nodo(nodo_abb_t* nodo_actual, nodo_abb_t* nuevo_nodo, abb_comparador comparador);
```

Esta es una función recursiva que tiene como objetivo insertar el nodo que queremos agregar al árbol.

Usamos el **comparador** pasado por parámetro para chequear si el elemento que queremos insertar es mayor o menor al del nodo actual. En caso de ser mayor o igual, hago que el nodo a la derecha se iguale a llamar a la función de nuevo. Lo mismo con el nodo izquierdo en caso de que el elemento sea menor.

La razón por la que hacemos que el siguiente nodo se iguale al resultado de llamar a la función es que cuando el nodo actual sea nulo, simplemente devolvemos el nodo que queríamos agregar. Si este no es el caso devolvemos el nodo actual y, como en una cadena, se van devolviendo todos los nodos iniciales. 

![[Algoritmos y Programación II/TDA abb Informe/Untitled 2.png|Untitled]]

                    **Diagrama 3: Inserción si el nuevo elemento es mayor a su predecesor**

![[Algoritmos y Programación II/TDA abb Informe/Untitled 3.png|Untitled]]

                   **Diagrama 4: Inserción si el nuevo elemento es menor a su predecesor**

```c
void* abb_quitar(abb_t* arbol, void *elemento);
```

Primero declaramos una variable de tipo **void*** llamada **elemento_quitado**, para guardar la dirección del elemento que quitemos del árbol, en caso de encontrarlo.

Vamos a usar otra vez lo que me imagino como una "táctica de cadena". Igualaremos el **nodo_raiz** del árbol a la función **abb_quitar_elemento**, la cual devuelve un **nodo_abb_t***.

Después de esto, si el **elemento_quitado** ya no es **NULL** eso significa que pudimos eliminar un elemento, por lo que disminuimos en uno el tamaño del árbol y regresamos el elemento.

```c
nodo_abb_t* abb_quitar_elemento(nodo_abb_t* nodo_actual, void* elemento_a_quitar, void** elemento_quitado, abb_comparador comparador);
```

Esta es una función recursiva, por lo que requerirá una condición de corte, la cual será encontrar un **NULL**, pues en ese caso el elemento no estaría en el árbol y regresaríamos **NULL**.

Comparamos los elementos y si nos devuelve un número mayor a cero entonces llamamos a la función de nuevo con el nodo derecho. Si la comparación es menor a cero hago lo mismo con el nodo izquierdo. Si la comparación es igual a cero, significa que el elemento que queremos quitar ha sido encontrado.

Ahora tenemos tres casos, que el nodo actual tenga cero, uno o dos hijos.

Lo que haremos en caso de que tenga uno o cero hijos es  declarar una variable **hijo**, a la que le asignaré el único hijo que tiene el nodo o NULL si no tiene ninguno.

Luego hacemos que el **elemento eliminado** sea el elemento del **nodo actual y** liberamos el nodo actual. Finalmente regresamos el hijo para que reemplace al padre.

Ahora veamos el caso en que tengamos dos hijos. En este caso no podemos hacer que un hijo reemplace al padre, sino que lo tendremos que reemplazar con algún elemento que tenga uno o cero hijos y respete el orden.

A través de la función **extraer_predecesor_izquierdo** consigo el predecesor. Intercambio el nodo actual por este, guardo la dirección del elemento, libero el nodo y finalmente regreso el elemento.

```c
nodo_abb_t* extraer_predecesor_izquierdo(nodo_abb_t* nodo_actual, nodo_abb_t** predecesor);
```

Vamos a seguir llamando a la función hasta encontrar un elemento cuyo nodo derecho sea **NULL**. Una vez encontrado hacemos que **predecesor** guarde la dirección del nodo actual y regresamos el nodo izquierdo, su único hijo, con lo cual este reemplazará al nodo actual. En caso de que el nodo izquierdo sea **NULL** también nos servirá devolverlo para que todo esté en orden.

![[Algoritmos y Programación II/TDA abb Informe/Untitled 4.png|Untitled]]

                                              **Diagrama 5: Árbol en su estado inicial**

![[Algoritmos y Programación II/TDA abb Informe/Untitled 5.png|Untitled]]

                                  **Diagrama 6: Árbol al quitarle hojas (elementos 1 y 5)**

![[Algoritmos y Programación II/TDA abb Informe/Untitled 6.png|Untitled]]

                     **Diagrama 7: Quitar un nodo con un hijo hace que este lo reemplace** 

                                                      **(quitamos el elemento 7)**

![[Algoritmos y Programación II/TDA abb Informe/Untitled 7.png|Untitled]]

       **Diagrama 8: Quitamos el elemento 6, que tenía dos hijos. Fue reemplazado por el 4, su** 

                        **predecesor izquierdo y el hijo del 4 (el elemento 3) lo reemplazó**

```c
void* abb_buscar(abb_t* arbol, void* elemento);
```

Si el árbol es válido, se regresa lo que devuelve la función **buscar_elemento**, la cual recibe el **nodo raíz**, el **comparador** y el **elemento** que queremos buscar.

```c
void* buscar_elemento(nodo_abb_t* nodo_actual, void* elemento, abb_comparador comparador);
```

Usamos el **comparador** y si este regresa cero, eso significa que encontramos el elemento, por lo que lo devolvemos.

Si nos da un número mayor o igual a cero entonces si estuviera en el árbol el elemento estaría en el nodo derecho, así que volveríamos a llamar a la función con ese nodo como el nodo actual. En caso de que la comparación nos devuelva un número menor a cero hacemos lo mismo pero hacia la izquierda.

Si el nodo actual es nulo, eso significa que el elemento no está en el árbol, por lo que regresamos **NULL**.

```c
bool abb_vacio(abb_t* arbol);
```

Regresa **verdadero** si el árbol es nulo o si su tamaño es cero.

Regresará **false** en caso contrario.

```c
size_t abb_tamanio(abb_t* arbol);
```

Devuelve el **tamaño** del árbol.

```c
void abb_destruir_todo(abb_t *arbol, void (*destructor)(void *));
```

Esta función libera todo el árbol y, en caso de que se le pase por parámetro un **destructor** válido, también liberará los elementos en cada nodo.

Si el árbol es válido y su tamaño no es cero, entonces se llamará a la función **liberar_nodos**, a la cual se le pasará el nodo **raíz** y el **destructor**.

Finalmente liberamos el **árbol** en sí.

```c
void liberar_nodos(nodo_abb_t* nodo_actual, void (*destructor)(void*));
```

Esta es una función recursiva que libera todos los odos en un árbol.

Primero le mandamos el nodo raíz de todo un árbol, luego llamamos a la función otra vez pero con los nodos a la izquierda y a la derecha como raíces.

Cuando le mandemos un nodo que sea **NULL,**  esta simplemente terminará sin volverse a llamar.

Después de que las funciones regresen se liberará al nodo actual y, en caso de que el **destructor** que nos pasaron por parámetro no sea nulo, también se liberará al **elemento**.

```c
void abb_destruir(abb_t* arbol);
```

El objetivo de esta función es el de liberar el árbol, pero no sus elementos.

Esto se puede hacer fácilmente llamando a la función que ya creamos, **abb_destruir_todo**, pero pasándole un destructor **NULL**, lo cual hará que no elimine los elementos.

```c
size_t abb_con_cada_elemento(abb_t *arbol, abb_recorrido recorrido, bool (*funcion)(void *, void *), void *aux);
```

Declaramos una variable **continuar** que usaremos para saber cuando parar a la hora de recorrer.

Luego, dependiendo del recorrido elegido por el usuario, llamamos a **abb_con_cada_elemento_inorden**, **abb_con_cada_elemento_preorden** o **abb_con_cada_elemento_postorden**.

```c
size_t abb_con_cada_elemento_inorden(nodo_abb_t* nodo_actual, bool (*funcion)(void *, void *), void *aux, bool* continuar);
```

Como el recorrido es **inorden**, primero revisamos el nodo de la izquierda, luego el del medio y luego el de la derecha.

Como tenemos que devolver cuantas veces se llamó la función, declaro una variable llamada **total**, la cual en las hojas va a empezar en cero, y va a aumentar en uno al subir por el árbol con cada vez que llamemos a la función.

Si llamamos a la función y esta devuelve **false** entonces aumento en uno el total y cambio el valor de la variable continuar a **false**. Como tengo el puntero a continuar entonces al cambiar su valor lo cambio para todos los otros ámbitos también, asegurándome de que ni la función se llame ni el total aumente más.

```c
size_t abb_con_cada_elemento_preorden(nodo_abb_t* nodo_actual, bool (*funcion)(void *, void *), void *aux, bool* continuar);
```

Es exactamente la misma estrategia que con el recorrido **inorden**, con la diferencia de que ahora lo haremos primero con el nodo actual, luego con el izquierdo y luego con el derecho.

```c
size_t abb_con_cada_elemento_postorden(nodo_abb_t* nodo_actual, bool (*funcion)(void *, void *), void *aux, bool* continuar);
```

Es exactamente la misma estrategia que con el recorrido **inorden** y **preorden**, con la diferencia de que ahora lo haremos primero con el nodo izquierdo, luego con el nodo actual y luego con el derecho.

```c
size_t abb_recorrer(abb_t* arbol, abb_recorrido recorrido, void** array, size_t tamanio_array);
```

En esta función haremos uso de la función **abb_con_cada_elemento**, sin embargo, la cantidad de datos que le tendríamos que pasar como auxiliar es mayor a uno. Por eso creamos un tipo de dato llamado **datos_auxiliar_funcion_t**, el cual tiene un campo para el vector, otro para el índice y otro para la capacidad máxima.

También le pasamos la función **guardar_elemento**, la cual hará uso de los datos auxiliares.

Paso una variable con los datos auxiliares cargados cómo auxiliar y la función a **abb_con_cada_elemento** y devuelvo el **indice**, ya que eso nos dirá cuantos elementos fueron ingresados.

```c
bool guardar_elemento(void* elemento, void* aux);
```

Si el índice no ha superado la cantidad máxima, entonces colocamos el elemento en el vector, aumentamos el índice en uno y regresamos **true**. Regresamos false en caso contrario.