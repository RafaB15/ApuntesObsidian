Es una técnica de [[Virtualización de Memoria|virtualización de memoria]].

Mientras que con al técnica de [[Segmentación|segmentación]] se le asignaba a cada espacio lógico de memoria un bloque de longitud variable, con paging, vamos a dividir la memoria en bloques de igual tamaño e irlos asignando.

Los bloque en un proceso son conocidos como  **páginas virtuales**, mientras que en memoria física se los conoce como **marcos físicos** o **marco de página**.

Por ejemplo, en un proceso, su [[Address Space]] sería algo como esto

![[Address space paging.png]]

Y la memoria física sería 

![[Memoria física paging.png]]

- Da una abstracción para el programador de como se organiza la memoria, incluyendo para qué lado crece un espacio de direcciones.
- Simplicidad para manejar memoria libre, pues si necesitamos asignar 3 bloques de 16 bytes, entonces se fija en memoria física si tiene 3 bloques disponibles. Como todos son del mismo tamaño no habrá que esperar que justo haya uno que nos convenga, o tener que reorganizar la memoria. A veces el [[Sistema Operativo|OS]] guarda una lista con los espacios libres y toma los primeros 3.
- La forma de las direcciones de memoria varía dependiendo del tamaño de las páginas, pero una cantidad de bits se usan para identificar el número de la página (*Virtual Page Number, VPN*), y los siguientes bits son para identificar en cual byte de la página se encuentra el dato (*offset*).

![[Dirección Virtual paging.png]]

![[Address translation paging.png]]
# Page table

- Por cada proceso, el sistema operativo guarda una estructura conocida como la **page table**, que contiene las direcciones de todas las páginas virtuales en memoria física. Te diría en qué **marco físico** está cada **página virtual**.
- Las **page table** a veces terminan ocupando mucho espacio. Son guardadas en memoria y no en algún hardware especial como el MMU.
- La forma más simple se conoce como **linear page table**, que es solo un array que el [[Sistema Operativo|OS]] indexa con el VPN, buscando la page-table entry (PTE) obteniendo el número de marco físico (*physical frame number, PFN*) deseado. 
- Dentro del PTE hay algunos bits que nos dicen si una página es válida. Las páginas no usadas en un [[Address Space]] se catalogan como inválidas para evitar reservarlas y ahorrar memoria. También almacenan muchos más datos.
- Sin un diseño cuidadoso que tenga en cuenta el software y el hardware, las page tables harán que el sistema corra muy lento, así como ocupe mucha memoria.

# Translation-lookaside buffer (TLB)

- Es parte de la MMU.
- Es un cache de las traducciones de memoria virtual a física más *populares* (un address translation cache).
- Cuando se referencia memoria virtual, primero nos fijamos en la TLB para ver si ahí está la traducción. En caso de tenerla, la traducción se hace rápidamente al no tener que consultar a la page table.
- El algoritmo funciona de la siguiente manera:
	1. Primero se extrae el *virtual page number* (VPN) de la memoria virtual.
	2. Nos fijamos si la TLB tiene la traducción para esa VPN.
	3. Si la tiene entonces tenemos un **TLB hit**. Extraemos el *page frame number* de la entrada de la TLB, la concatenamos con el *offset* de la dirección virtual original y obtenemos la dirección física, en donde podemos acceder a memoria.
	4. Si no la tiene entonces tenemos un **TLB miss**. Entramos a la page table para encontrar la traducción y si la dirección es válida y accesible entonces actualizamos la TLB con la dirección. Luego el hardware vuelve a intentar encontrar la dirección en la TLB y al encontrarla hace el paso 3.
- Buscar en la page table es una opción más costosa por las referencias a memoria extra que implica entrar a la page table.