## Codificación Naive

 Le asignamos a cada posibilidad una combinación difernete del mismo número de dígitos (bits).

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled.png|Untitled]]

## Compresión por codificación

Usamos la cantidad de bits mínimo que nos dice la fórmula

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 1.png|Untitled]]

Podemos multiplicar las probabilidades de usar cada símbolo por la cantidad de bits y vemos que no es igual a la entropía de Shannon, que sería el número óptimo.

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 2.png|Untitled]]

## Codificación de Huffman

En un texto agarramos todos los caracteres y contamos cuantas veces aparece cada uno

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 3.png|Untitled]]

Usamos 4 bits para cada uno y al ser 27 caracteres tenemos 108 bits

Agarramos los dos caracteres de menor frecuencia y creando un nodo arriba, como un árbol binario. Seguimos agarrando a todos los que tienen menor frecuencia y los unimos en nodos.

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 4.png|Untitled]]

Ahora invertimos las flechas y ponemos 1s en las ramas derechas y 0s en las izquierdas. 

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 5.png|Untitled]]

Entonces si queremos codificar las letras, solamente tenemos que bajar desde la raíz hasta la letra y nos quedamos con los números en las ramas.

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 6.png|Untitled]]

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 7.png|Untitled]]

Ahora tenemos 103 bits en vez de 108, para textos más grandes se nota mucho más la diferencia.

## Compresión aritmética

![[Organización de datos/Compresión e IA/Compresión sin pérdida/Untitled 8.png|Untitled]]