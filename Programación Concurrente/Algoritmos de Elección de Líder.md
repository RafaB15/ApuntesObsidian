- Son algoritmos que hacen uso de la concurrencia distribuida
- Varios algoritmos requieren de un **coordinador/líder** con un rol especial (ej: algoritmos de exclusión mutua distribuida). 
- En general, no es importante cuál es el proceso, sino que debe cubrirse el rol. 
- Se asume: todos los procesos tienen un ID único, se ejecuta un proceso por máquina y conocen el número de los demás procesos. 
- El objetivo: cuando la elección comienza, concluye con un líder elegido.

# Algoritmo Bully

- Cuando un proceso P nota que el **coordinador** no responde, inicia el proceso de elección:
1. P envía el mensaje ELECTION a todos los procesos que tengan número/ID mayor que él.
2. Si nadie responde, P gana la elección y es el nuevo coordinador
3. Si contesta algún proceso con número mayor, éste continúa con el proceso y P finaliza. Luego estos procesos con ID mayor repiten el proceso hasta que ningún proceso con ID mayor les responda.
4. El nuevo coordinador se anuncia con un mensaje COORDINATOR
Siempre gana el proceso con mayor número.

![[Pasted image 20240521123313.png]]

# Algoritmo Ring

1. Los procesos están ordenados lógicamente; cada uno conoce a su sucesor. Le puede enviar mensajes solo a este y recibir mensajes solo del ID anterior.
2. Cuando un proceso nota que el coordinador falló, arma un mensaje ELECTION que contiene su número de proceso y lo envía al sucesor 
3. El proceso que recibe el mensaje, agrega su número de proceso a la lista dentro del mensaje y lo envía al sucesor
4. Cuando el proceso original recibe el mensaje, lo cambia a COORDINATOR y lo envía. El nuevo coordinador es el proceso de mayor número de la lista. La lista se mantiene para informar el nuevo anillo.
5. Cuando este mensaje finaliza la circulación, se elimina del anillo

![[Pasted image 20240521123434.png]]

La imagen es un snapshot, el algoritmo no está terminado, por eso faltan mensajes. El 5 y el 2 se dieron cuenta que el 7 no andaba y ambos empezaron el algoritmo.