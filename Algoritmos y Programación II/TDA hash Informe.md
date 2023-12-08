$\text{[7541/9515] Algoritmos y Programación II}$

                                                                       

                        $\def\arraystretch{1.4}\begin{array}{|c|c|}\hline

\text{\textbf{Alumno:}}  &
\text{\textbf{Rafael Francisco Berenguel Ibarra}}

\\\hline

\text{Padrón:} &
\text{108225}

\\\hline

\text{Email:} &
\text{rberenguel@fi.uba.ar}

\\\hline\end{array}$

## 1. Introducción:

El TDA hash consistía en la implementación de un hash abierto, direccionalmente cerrado. Este tendría que poder ser controlado por un usuario, sin necesidad de que este sepa cómo funciona por dentro, a través de diversas funciones escritas por nosotros.

## 2. Teoría:

### ¿Qué es un hash? ¿Qué es una tabla de hash?

Un hash es un tipo de dato abstracto en el que guardamos elementos, con la característica de que una vez lo tengamos hecho, buscar elementos en este apunta a tener complejidad **O(1).**

El componente más importante del hash es sin lugar a dudas la tabla hash. 

Una tabla de hash es un vector en donde guardaremos, o los elementos que vayamos insertando en el hash, o punteros a estructuras que los contengan, dependiendo del tipo de hash que hayamos implementado.

Al querer ingresar un elemento se nos dará también una clave, y dependiendo de esta creamos un **número hash**. De este número dependerá el lugar en la tabla hash en donde intentaremos insertar el elemento. 

Hay dos tipos de tablas hash:

**Hash abierto:**

Un hash abierto tiene en cada lugar de la tabla hash un puntero hacia una estructura en la que guardaremos el elemento.

Esta puede ser de cualquier tipo, pero obviamente habrán algunas que nos convengan más. 

Si queremos insertar un elemento, debemos calcular con nuestra función de hash la posición en la tabla en donde se apunta a la estructura en la que debemos insertar, ir allí e insertar nuestro elemento.

Si insertamos un elemento con la misma clave que un elemento existente en el hash este será reemplazado.

Si la clave genera el mismo número hash que un elemento ya insertado entonces estos estarán almacenados en la misma estructura.

Si se cumplen ciertas condiciones relacionadas con la cantidad de elementos almacenados y la capacidad máxima de la tabla, podemos llegar a tener que agrandar la tabla y redistribuir los elementos. Con esto intentamos que no hayan muchos elementos en una misma estructura, pues eso haría la búsqueda más parecida a **O(n)** que a **O(1)**.

Para quitar un elemento también recibimos una clave y buscamos el elemento en la estructura que le corresponde para eliminarlo.

Buscar y obtener elementos en este tipo de hash también es ir a la estructura en la que estén almacenados y buscarlos ahí.

Para eliminar este tipo de hash se tendrá que liberar todas las estructuras armadas para guardar los elementos, así como lo que respecta a la estructura del hash en sí.

![[Algoritmos y Programación II/TDA hash Informe/Untitled.png|Untitled]]

                                                   **Diagrama 1: Hash abierto**

**Hash cerrado:**

En un hash cerrado, a diferencia de un hash abierto, no guardaremos los elementos en estructuras aparte, sino que los guardaremos directamente en la tabla hash.

En caso de que la posición que le corresponda al elemento esté ocupada por un elemento con la misma clave, este es eliminado y se inserta el nuevo elemento en su lugar. Si el elemento que ocupa el lugar tiene clave distinta entonces iremos recorriendo el vector hasta encontrar un espacio libre y ahí lo insertaremos.

Para buscar un elemento en la tabla hash podemos usar  varios métodos, entre los que se encuentra el probing lineal, en el que si no encontramos el elemento en el lugar que le corresponde, recorremos el vector hasta encontrarlo o encontrar un espacio vacío.

Para eliminar también buscamos el elemento, y al encontrarlo lo borramos tomando las precauciones necesarias para que el resto de los elementos de la tabla puedan seguir siendo encontrados.

![[Algoritmos y Programación II/TDA hash Informe/Untitled 1.png|Untitled]]

                                              **Diagrama 2: Hash cerrado**

## 3. Detalles de implementación:

Los archivos que precisaremos para poder controlar el TDA son **hash.h, hash.c y estructura_hash.h.**

También tenemos los archivos **pa2mm.h, ejemplo.c** y **pruebas.c** que podremos usar junto a **makefile** para testear nuestro archivo (la función **pruebas.c** implementada por nosotros).

Para este **TDA** usaremos las estructuras **nodo_hash_t** y **hash_t**. El **nodo_hash** posee una **char*** en el que guardaremos la clave, un **void*** en el que guardaremos el elemento y un puntero a otro nodo hash. El **hash_t** tendrá un campo en el que guardaremos el **destructor**, un puntero a un vector de punteros a **nodo_hash_t** que será nuestra tabla hash, un **size_t** en donde almacenaremos la capacidad que tiene nuestra tabla y otro **size_t** en donde guardaremos la cantidad de elementos almacenados en el hash.

En lo que sigue, nos referiremos a una sucesión de nodos hash apuntándose los unos a los otros como una "**cadena**". Utilizo este termino para no confundir con el **tda_lista**, pues aunque es parecido, no es exactamente lo que estamos usando.

Las funciones implementadas para el correcto funcionamiento del TDA son

```c
hash_t* hash_crear(hash_destruir_dato_t destruir_elemento, size_t capacidad_inicial);
```

Esta función crea e inicializa un hash_t  en el heap y devuelve un puntero a este. 

![[Algoritmos y Programación II/TDA hash Informe/Untitled 2.png|Untitled]]

                            **Diagrama 3: Inicialización para un hash con capacidad inicial 5**

```c
size_t generar_numero_hash(const char* clave);
```

Recibe una clave y devuelve un número que depende de esta. 

Dado que cada caracter tiene asociado un número que podemos revisar en una tabla ASCII, los usamos para generar el número hash.

Definimos una variable en donde sumaremos cada caracter multiplicado por su posición en la clave más uno. De esta forma no solo se diferencia el número hash por qué letras se usen en la clave, sino también por el orden en el que estas letras estén. 

```c
int hash_insertar(hash_t* hash, const char* clave, void* elemento);
```

Lo primero que hacemos es ver si nuestra tabla está lo suficientemente llena como para que tengamos que rehashear. En caso de que este sea el caso, llamamos a la función **rehash.**

Para insertar un elemento en nuestro hash, lo primero que hacemos es utilizar la función **generar_numero_hash** para calcular el número hash de nuestro elemento y luego usamos el módulo con la capacidad de la tabla para que la posición sea válida.

Utilizamos la función **insertar_nodo_hash**, pasándole la dirección del primero de la cadena de nodos en la que almacenaremos este elemento.

Si no hubo un reemplazo, entonces aumentamos la cantidad de elementos almacenados del hash y regresamos cero. En caso de error regresamos menos uno.

```c
nodo_hash_t* insertar_nodo_hash(nodo_hash_t* nodo_actual, const char* clave, void* elemento, hash_destruir_dato_t destruir_elemento, bool* error, bool* reemplazo);
```

Esta será una función recursiva que tendrá como objetivo insertar un elemento en una cadena de nodos. 

La función se va a llamar a sí misma hasta que suceda una de dos posibilidades.

La primera es que el **nodo_actual** sea NULL, en cuyo caso llegamos al final de la cadena y lo podemos insertar. Llamamos a la función **crear_nuevo_nodo** para crear un nodo con los datos requeridos y lo insertamos en la cadena.

La segunda es que la clave del elemento almacenado en **nodo_actual** sea igual a la clave del elemento que queremos insertar, en cuyo caso tenemos que reemplazarlos. En este caso no es necesario crear un nuevo nodo, pues simplemente debo destruir el elemento en la tabla en caso de tener destructor no **NULL** y poner en su lugar al nuevo elemento, ya que la clave es la misma.

```c
nodo_hash_t* crear_nuevo_nodo(const char* clave, void* elemento, bool* error);
```

Reserva espacio para un nuevo nodo y lo inicializa con el elemento pasado por referencia y una copia de la clave también pasada por referencia. 

Guardamos una copia de la clave de cuya creación y posterior liberación nos ocuparemos nosotros debido a que el usuario podría en cualquier momento eliminar la clave y consecuentemente romper nuestro hash.

Devuelve el nuevo nodo.

![[Algoritmos y Programación II/TDA hash Informe/Untitled 3.png|Untitled]]

                         **Diagrama 4: Insertamos un elemento "Banana" con clave "33" y**

                                          **un elemento "Manzana" con clave "15"**

![[Algoritmos y Programación II/TDA hash Informe/Untitled 4.png|Untitled]]

                  **Diagrama 5: Si el número hash de dos elementos es el mismo, estos terminan** 

                                                              **en la misma cadena**

![[Algoritmos y Programación II/TDA hash Informe/Untitled 5.png|Untitled]]

                   **Diagrama 6: Insertamos el elemento "Pera" con clave "15", lo cual hace que** 

                                                                  **reemplace a "Manzana"**

```c
int rehash(hash_t* hash);
```

Esta función se encarga de dejar al hash pasado por referencia con una tabla con mayor capacidad.

Usamos esta función cuando la tabla tiene una cantidad de elementos igual al **75%** de su capacidad y no por longitud de las cadenas porque no me pareció muy necesario. En un principio intenté también rehashear en caso de que una cadena tuviera cierta longitud, argumentando que si una de ellas crecía hasta cierto punto es porque por el tipo de claves que se están ingresando solo seguirá creciendo y habría que rehashear, sin embargo luego me di cuenta que por la manera de decidir donde se inserta algo, la cual depende de la capacidad y de tener una función hash buena que dependa de varios factores, una situación en donde una cadena de nodos se haga tan grande que el rendimiento del programa se vea afectado tiene muy pocas probabilidades de darse antes de que se cumpla la condición del **75%**.

Dependiendo de la capacidad actual, vamos a triplicar o duplicar el tamaño de la tabla.

Creamos un nuevo hash con este nuevo tamaño en el que volveremos a meter los elementos del hash original.

Llamamos a la función **rehash_cadena** cuantas veces sean necesarias. Con esto se habrán pasado todos los nodos del hash original al nuevo.

Luego llamamos a la función **reorganizar_memoria**, que se encargará de liberar lo que sea necesario y dejar listo el hash original.

Regresamos 0 si todo salió bien.

```c
void rehash_cadena(nodo_hash_t* cadena_original, hash_t* hash_nuevo);
```

Esta función recibe el inicio de una cadena del hash original y el hash nuevo.

Esta función es recursiva, pues lo primero que sucede es que la función se llama a sí misma con el siguiente nodo hasta que este sea **NULL**. Luego hacemos el resto de las operaciones y cuando vaya regresando al final de cada una irá retrocediendo en la cadena hasta haber pasado por todos los nodos.

Primero hacemos que el nodo que queremos pasar al hash nuevo tenga **NULL** como siguiente. Esto lo hacemos porque como se explicó  en el párrafo anterior, primero operamos en el último nodo de la cadena y luego de a uno hacia atrás, por lo que a medida que los vayamos insertando habrá que borrarles la información de quién solía estar después.

Luego con **generar_numero_hash** vemos en qué posición en el nuevo hash deberíamos insertar estos nodos y lo hacemos a través de la función **insertar_nodo_rehash.** Luego regresamos.

En un principio hice el **rehash** reinsertando cada elemento del hash original con la función **hash_insertar**. Funcionaba perfecto, sin embargo, luego me di cuenta que no había por qué descartar reacomodar los nodos. Es decir, haciéndolo de esta forma no tengo que crear nuevos nodos ni liberar los antiguos, lo cual hace a esta función más eficiente.

```c
nodo_hash_t* insertar_nodo_rehash(nodo_hash_t* cadena_nueva, nodo_hash_t* nodo_a_insertar);
```

Es una función recursiva que recibe el inicio de una cadena de nodos y un hash que tiene que insertar en esta. 

Como estamos pasando nodos de una tabla hash a otra, sabemos que todos tienen claves distintas, por lo que lo único que tenemos que hacer es insertarlo al final, en otras palabras, cuando nos topemos con **NULL.**

```c
void reorganizar_memoria(hash_t* hash, hash_t* hash_nuevo);
```

Esta función se encarga de actualizar el hash original con todos lo datos necesarios y liberar toda la memoria que ya no necesitemos.

![[Algoritmos y Programación II/TDA hash Informe/Untitled 6.png|Untitled]]

                                **Diagrama 7: Tenemos un hash con capacidad 5 y 4 elementos**

                                      **Si intentamos agregar un elemento más haremos rehash**

![[Algoritmos y Programación II/TDA hash Informe/Untitled 7.png|Untitled]]

                                   **Diagrama 8: Creamos un nuevo hash con más capacidad**

![[Algoritmos y Programación II/TDA hash Informe/Untitled 8.png|Untitled]]

                       **Diagrama 9: Hacemos que los punteros correspondientes en la nueva tabla** 

                                        **apunten a los nodos de la tabla original**

![[Algoritmos y Programación II/TDA hash Informe/Untitled 9.png|Untitled]]

                    **Diagrama 10: Reorganizo la memoria y los datos para quedarme solo con**

                                                                              **lo necesario**

*Nota: En los gráficos elementos almacenados debería ir aumentando, pero me olvidé. 

```c
int hash_quitar(hash_t* hash, const char* clave);
```

Primero averiguamos en donde debería estar el elemento calculando su número de hash.

Luego llamamos a la función **quitar_nodo_hash** para que quite el nodo de la cadena en la que se debería encontrar el elemento que queremos eliminar en caso de estar en la tabla.

Si el elemento estaba en la tabla, disminuimos la cantidad de elementos almacenados y regresamos 0. En caso contrario regresamos -1.

```c
nodo_hash_t* quitar_nodo_hash(nodo_hash_t* nodo_actual, const char* clave, hash_destruir_dato_t destruir_elemento, bool* quitado);
```

Esta es una función recursiva que recorrerá la cadena que empieza con el nodo pasado por referencia hasta encontrar un nodo con una clave igual a la también pasada por referencia o un **NULL.**

En caso de encontrar un elemento con la misma clave, libera el nodo y utiliza el destructor para liberar el elemento.

En caso de encontrar **NULL** significa que el elemento no estaba n la tabla hash, por lo que no lo puede eliminar.

```c
void* hash_obtener(hash_t* hash, const char* clave);
```

Llama a la función recursiva **obtener_elemento_nodo_hash** pasándole el inicio de la cadena en la que tiene que buscar el elemento. Devuelve el elemento si lo encontró o **NULL** en caso contrario. 

```c
void* obtener_elemento_nodo_hash(nodo_hash_t* nodo_actual, const char* clave);
```

Es una función recursiva que recorrerá toda la cadena que nace del nodo pasado por referencia buscando un nodo con una clave igual a la también pasada por referencia. En caso de encontrarla devuelve el elemento en ese nodo. En caso de no hacerlo devuelve **NULL**.

```c
bool hash_contiene(hash_t* hash, const char* clave);
```

Llama a la función recursiva **buscar_nodo_hash** pasándole el inicio de la cadena en la que tiene que buscar el elemento. Devuelve **true** si encontró al elemento o **false** en caso contrario. 

```c
bool buscar_nodo_hash(nodo_hash_t* nodo_actual, const char* clave);
```

Es una función recursiva que recorrerá toda la cadena que nace del nodo pasado por referencia buscando un nodo con una clave igual a la también pasada por referencia. En caso de encontrarla devuelve **true**. En caso de no hacerlo devuelve **false**.

```c
size_t hash_cantidad(hash_t* hash);
```

Devuelve la cantidad de elementos almacenados en el hash pasado por referencia.

```c
void hash_destruir(hash_t* hash);
```

Primero llama a la función **destruir_cadena_hash** a la que le pasa el destructor y el inicio de cada cadena para que las libere.

Luego libera la tabla y el hash en sí.

```c
void destruir_cadena_hash(nodo_hash_t* nodo_actual, hash_destruir_dato_t destruir_elemento);
```

Es una función recursiva que libera cada elemento y clave de los nodos de una cadena, así como el nodo en sí.

El **destruir_elemento** puede ser **NULL**, si el usuario quiere encargarse él mismo del manejo de memoria de los elementos. Por eso ponemos un **if** por si es **NULL**.

```c
size_t hash_con_cada_clave(hash_t* hash, bool (*funcion)(hash_t* hash, const char* clave, void* aux), void* aux);
```

Esta función recorre iterativamente toda la tabla hash, usando la función pasada por referencia en cada elemento.

Para hacer esto utilizamos un **doble while loop**, dado que quiero que todo pare cuando al evaluar la función en algún elemento esta nos de **true**. Con el primer **while** me encargo de la cadena en la que estoy y con el segundo de la posición en esta.

Al finalizar cada llamado a la función aumento en uno la variable **numero_de_invocaciones**, la cual finalmente regreso.