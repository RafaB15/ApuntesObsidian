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

# 1. Introducción:

Este **TP** consistía en la elaboración de un simulador de un hospital pokemon, que  pudiera simular ciertos eventos, y un **main** para controlarlo cómodamente desde la terminal.

Un aspecto importante de este **TP** es que no podíamos tener vectores dinámicos y estáticos en las estructuras, siendo así necesario utilizar los **tdas** que hicimos en entregas pasadas.

Los **TDAs** utilizados para este **TP** fueron **abb**, **lista**, **cola** y **heap.**

# 2. Detalles de implementación:

## 2.1. Compilación:

Los archivos necesarios para compilar nuestro programa son **simulador.c**, **simulador.h**, **hospital.c**, **hospital.h**, **abb.c**, **abb.h**, **cola.c**, **cola.h**, **estructuras_hospital.h**, **estructuras_simulador.h**, **heap.c**, **heap.h**, **lista.c**, **lista.h, split.c** y **split.h.** Estos los usaremos en **main.c**.

También tenemos los archivos **pa2mm.h, pruebas.c**, **pruebas_heap.c** y **pruebas_simulador.c** que podremos usar junto a **makefile** para testear nuestro archivo.

Para compilar y correr las pruebas_heap.c se tienen que ingresar los siguientes comandos en la terminal 

```c
gcc src/heap.c pruebas_heap.c-o pruebas_heap
valgrind ./pruebas_heap
```

Se hicieron algunas pruebas del heap porque, a  pesar de tener una forma muy parecida al hecho en clase, se tuvo que cambiar para que tenga toda la forma de un TDA que se pueda usar con cualquier tipo de dato.

Para compilar y correr las pruebas del hospital podemos usar el makefile escribiendo 

```c
make valgrind-pruebas
```

Para compilar y correr el main utilizamos el makefile

```c
make valgrind
```

Aunque al ser la primera instrucción del makefile. podemos directamente escribir make.

Para compilar y correr las pruebas_simulador escribimos estos comandos en la terminal.

```c
gcc pruebas_simulador.c src/*.c -o pruebas_simulador
valgrind ./pruebas_simulador
```

También, si quisiéramos agilizar el proceso utilizando makefile, le podríamos agregar esto al provisto por la cátedra

```c
pruebas-simulador: pruebas_simulador.c src/*.c src/*.h
	gcc $(CFLAGS) -o pruebas_simulador pruebas_simulador.c src/*.c 2>&1

valgrind-pruebas_simulador: pruebas-simulador
	valgrind $(VFLAGS) ./pruebas_simulador 2>&1
```

Y luego bastaría con escribir

```c
make valgrind-pruebas_simulador
```

en la terminal.

## 2.2. Cambios al hospital:

El hospital que necesitábamos para este TP  era ligeramente diferente al desarrollado en el TP 1.

Las dos diferencia más notables son el impedimento para usar vectores dinámicos en estructuras y  la adición de los entrenadores como nueva estructura.

Para no usar vectores dinámicos, cambiamos el **pokemon_t*** de la estructura del hospital por un **abb_t***. Usamos un abb para poder recorrer a los pokemon en orden. Al crear este árbol binario le paso por referencia una función que creé, llamada **comparador_nombres_pkm**, para que los pokemon se almacenen en orden alfabético. Agrego los nuevos pokemon con **abb_insertar** y consigo la cantidad de pokemon con **abb_tamanio.** Hacer **hospital_con_cada_elemento** era un poco más complicado, pues esta recibe solo el pokemon, sin un auxiliar, lo cual la diferencia de **abb_con_cada_elemento**. Esto lo podemos resolver creando una **funcion_para_abb** que recibe un pokemon y una función como auxiliar. Esa función será la que originalmente me pasaron. De esta forma puedo hacer **abb_con_cada_elemento.**

Incluir los entrenadores es más fácil. En cada línea vamos a encontrar a un entrenador y a sus pokemon. Como yo ingreso los pokemon por línea, antes de ingresarlos creo a un entrenador y se lo asigno a cada pokemon. No tengo una lista de entrenadores en sí, sino que sé cuantos pokemon tienen, cual es su nombre y en qué orden llegó. En nuestra implementación, si un entrenador con los mismo datos es ingresado, será tratado como un entrenador nuevo con pokemon nuevos. Esto lo hacemos así para conservar el orden de llegada de los pokemon que lleva el entrenador al hospital al ingresar. 

Para destruir el hospital, utilizo **abb_destruir** pasandole la función **destructor_de_pokemon** la cual se encargará de liberar al pokemon y a sus entrenadores. Para liberar a los entrenadores verán cuantos pokemon les quedan. Si al entrenador le queda solo un pokemon, significa  que el único pokémon suyo que queda sin liberar es el que estamos liberando, así que liberamos al entrenador. Si le quedan más de un pokemon, reducimos su **cantidad_pkm** en uno.

![[Algoritmos y Programación II/TP2 Simulador/Untitled.png|Untitled]]

            **Diagrama 1: Nuevo diseño de hospital (no se incluyeron los nombres por espacio)**

## 2.3. Simulador

```c
**simulador_t* simulador_crear(hospital_t* hospital);**
```

Nuestro simulador  tiene unos cuantos campos que tendremos que inicializar.

### **hospital_t* hospital:**

Aquí ponemos el hospital que nos pasan por referencia en la función. Lo tenemos en el **struct** para poder liberarlo cuando queramos destruir el simulador.

### **bool funcionando:**

Este campo lo usaremos para saber si la simulación está en funcionamiento o ya ha terminado. En caso de haber terminado no se podrán hacer más simulaciones.

### **cola_t* sala_de_espera:**

Esta será una cola en la que almacenaremos listas, cada una con los pokemon de un entrenador.

Para lograr esto, creamos primero un vector de listas (**lista_t***) con la función **crear_listas.**

Esta función crea un vector dinámico del tamaño de la cantidad de entrenadores y a cada espacio le crea una lista.

Posteriormente usamos **abb_con_cada_elemento** en el arbol de pokemon del hospital con la función **agregar_pokemon_a_las_listas**, la cual va a agregar a cada pokemon a la lista que tenga el índice igual al orden de llegada de su entrenador. De esta manera el vector de listas tendrá en su primer espacio una lista con los pokemon del entrenador que llegó primero, luego el segundo y así.

Luego usamos la función **crear_sala_de_espera** para crear una cola que tenga encoladas las listas con los pokemon de los entrenadores, siendo el primero en la cola el primer entrenador en llegar y el último el último en llegar.

### **heap_t* pokemon_esperando:**

Este es el **heap** en el que almacenaremos a los pokemon recepcionados que esperan a ser atendidos. Lo creamos con la cantidad total de pokemon como **capacidad inicial** y le pasamos una función **comparador_niveles_pkm** que hará que al insertar pokemon a este heap estos queden con el de menor nivel en la raíz. Al principio está vacío, pero lo llenaremos al atender entrenadores.

### **pokemon_t* tratando_actualmente:**

Aquí almacenaremos al pokémon que estemos tratando actualmente. Se inicializa en NULL.

### **EstadisticasSimulacion estadisticas:**

Son las estadisticas del juego. Las inicializamos con los datos adecuados.

### **lista_t* lista_dificultades:**

Esta es una lista en la que guardaremos variables de tipo **DatosDificultad***. Aquí guardaremos los datos de todas las dificultades de nuestro juego.

Con la función **simulador_agregar_dificultades_iniciales** llenamos la lista con las tres dificultades iniciales (fácil, normal y difícil). Esta función va a crear en el stack, a través de la función **inicializar_datos_dificultad**, variables del tipo **DatosDificultad** que tengan los datos de las nuevas dificultades. Haremos que estas apunten a las funciones creadas antes: **calcular_puntaje_facil**, **verificar_nivel_facil**, **verificacion_a_string_facil**, **calcular_puntaje_normal**, **verificar_nivel**, **verificacion_a_string_normal**, **calcular_puntaje_dificil** y **verificacion_a_string_dificil**.

Luego usaremos la función **agregar_dificultad** (que explicaremos más tarde) para agregarlas a la lista.

### **DatosDificultad* dificultad_actual:**

Apunta a la dificultad en uso actualmente. Se inicializa apuntando a la dificultad **Normal**.

### **size_t cantidad_intentos_actual:**

Este campo lo usamos al estar adivinando el nivel de un pokemon. La cantidad de intentos subirá con cada vez que nos equivoquemos y cuando adivinen correctamente se usará para calcular el puntaje. Después de esto será reseteada a cero.

![[Algoritmos y Programación II/TP2 Simulador/Untitled.jpeg|Untitled]]

                                     **Diagrama 2: Memoria después de crear un simulador**

```c
ResultadoSimulacion simulador_simular_evento(simulador_t* simulador, EventoSimulacion evento, void* datos);
```

Esta función solo funciona si el simulador no es NULL, si el evento es válido y si el simulador está funcionando.

Esta función se comporta distinto dependiendo del evento que le pasemos por parámetro.

### **ObtenerEstadisticas:**

Si nos pasan este evento tendremos como dato un puntero a un elemento de tipo **EstadisticasSimulacion***. Nosotros llamaremos a la función **obtener_estadisticas**, la cual copiará las estadísticas del campo **estadisticas** del simulador al elemento que nos pasaron como dato. Si sale todo bien devuelve ExitoSimulacion.

### **AtenderProximoEntrenador:**

Si nos pasan este evento el dato será **NULL**. Nosotros llamaremos a la función  **atender_proximo_entrenador**. 

Devolverá ErrorSimulación si ya no hay más entrenadores para atender. 

Lo primero que hacemos es desencolar una lista de nuestra cola de listas (el campo **sala_de_espera** en el simulador), ya que esta contendrá a todos los pokemon del siguiente entrenador. 

Luego utilizamos **lista_con_cada_elemento** pasándole una función llamada **reposicionar_pokemon** y nuestro heap (el campo **pokemon_esperando** en el simulador) como auxiliar. La función inserta los pokemon en el heap.

De esta manera, todos los pokemon que estaban en la lista pasaran a ser insertados en el heap, dejando siempre al de menor nivel como raíz.

En caso de que no se esté tratando actualmente a ningún pokemon, extraemos la raíz de nuestro heap y hacemos que **tratando_actualmente** apunte a ese pokemon.

También actualizamos las estadísticas como corresponda.

![[Algoritmos y Programación II/TP2 Simulador/Untitled 1.jpeg|Untitled]]

         **Diagrama 3: La primera lista que tenía los pokemon del primer entrenador en llegar**

                                        **pasan a ser parte del heap y el de menor nivel es atendido**

### **ObtenerInformacionPokemonEnTratamiento:**

El dato en este evento será **InformacionPokemon*.** 

Llamamos a la función **obtener_informacion_pokemon_en_tratamiento** pasándole el pokemon en tratamiento y la información para rellenar.

Si no hay pokemon en tratamiento inicializo los campos de la información a **NULL** y regreso **ErrorSimulacion**.  En caso contrario, inicializo la información con los datos del pokemon y regreso **ExitoSimulacion**.

### **Adivinar_nivel_pokemon**

El dato en este evento es **Intento*.**

Llamamos a la función **adivinar_nivel_pokemon** pasándole el simulador y el intento. 

Utilizaremos las funciones de la dificultad actual para primero, verificar el nivel. 

Si el nivel verificado es distinto de cero, eso significa que no acertamos, por lo que inicializo el campo es_correcto del intento en false y aumento los intentos actuales del simulador.

En caso de que el nivel sea cero, inicializaremos es_correcto a true y calcularemos el puntaje para aumentarlo, actualizamos las estadísticas y extraemos al siguiente pokemon de menor nivel esperando. 

Sea cual sea el caso, inicializamos el campo **resultado_string** con el resultado de la función **verificación_a_string** de la dificultad y devolvemos **ExitoSimulacion**.

### AgregarDificultad:

Recibe como dato **DatosDificultad***. Llama a la función **agregar_dificultad** pasándole el simulador y la nueva dificultad.

Si la dificultad o sus campos son **NULL**, entonces devolveremos **ErrorSimulacion**. 

Primero creamos una variable de tipo **DatosDificultad*** que sea exactamente igual a la pasada por referencia, con la diferencia de que esta está almacenada en el **heap**. 

Creamos una variable de tipo **comparacion_dificultad_t**, la cual utilizaremos para cerciorarnos de que el nombre de la dificultad no se repite. Inicializo los campos de esta variable con el nombre de la dificultad y false en el campo repetido.

Llamo a **lista_con_cada_elemento** pasándole la lista de dificultades, la función **comparador_nombre_dificultades** y la dirección de la variable de comparación de dificultades.

Si el campo repetido sigue siendo false significa que el nombre no se repite, por lo que inserto la nueva dificultad en la lista.

Si todo salió bien, regreso **ExitoSimulacion**.

### SeleccionarDificultad

Recibe un puntero a un **int** que representa el índice. Se llama a la función **seleccionar_dificultad** pasándole el simulador y la direccion al indice. Si este es válido, la dificultad actual se cambiará al resultado de usar **lista_elemento_en_posicion** pasándole la lista de dificultades y el indice pedido.

Devolvermos **ExitoSimulacion**.

### ObtenerInformacionDificultad

Recibe un puntero a **InformaciónDificultad** como dato. Se lo pasamos a la función **seleccionar_dificultad** junto al simulador como parámetros.

Si el id de informacion no es válido, inicializamos todos los campos a **false**, **NULL** y **-1** y devolvemos **ErrorSimulacion**. 

En caso contrario utilizamos **lista_elemento_en_posicion** para conseguir los datos de la dificultad buscada e inicializamos con estos **informacion**.

Devolvemos **ExitoSimulacion**.

### FinalizarSimulacion:

Lo único que hacemos en este caso es cambiar el valor del campo funcionando del simulador de **true** a **false** y deovlvemos **ExitoSimulacion**. 

Si le pasan cualquier otro evento a simulador_simular_evento se devolverá ErrorSimulacion.

```c
void simulador_destruir(simulador_t* simulador);
```

Esta función se encarga de liberar toda la memoria del simulador y del hospital.

Primero nos fijamos en la cantidad de entrenadores restantes, o mejor dicho, la cantidad de filas que quedaron si ser puestas en el heap. Las desencolamos y las liberamos todas.

Luego destruimos la **cola** y el **heap**.

Usamos **lista_con_cada_elemento** pasándole la lista de dificultades y la función **destruir_dificultad** con auxiliar **NULL** para que libere todas las dificultades. Luego destruyo la lista en sí.

Destruyo el hospital y libero el simulador.