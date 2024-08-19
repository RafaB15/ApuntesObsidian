# Adaptive Playout Mechanisms for Packetized Audio Applications in Wide-Area Networks

## By Ramachandran Ramjee, Jim Kurose, Don Towsley

- Paper de 1994
- Contexto en el que se estaba empezando a ver que se transmitía audio a través de paquetes por internet, impulsado por la reducción de su costo y la cada vez creciente cantidad de ejemplos en los que esto se había llevado a cabo, mostrando el internet de esa época podía soportarlo.
- Se pone los paquetes de audio recibidos en un buffer y su reproducción es atrasada en el host destino para compensar por los retrasos variables de la red. 
- Se apunta a que estos ya estén en el buffer para cuando llegue el momento en el que se los tiene que reproducir.
- Los paquetes que no llegan antes del momento de reproducción se consideran perdidos.
- Se exploran 4 algoritmos para ajustar dinámicamente el delay de los paquetes para afrontar variantes retrasos en la red.
- En el paper se centran en el comportamiento del host para lidiar con estos retrasos, no en como evitar los retrasos.
- Imagen en la que podemos ver como una fuente genera los paquetes de audio (se ve como escalera porque periódicamente se crea un paquete con audio) y un host los recibe en diferentes intervalos dependiendo del retraso en la red. El host que recibe puede lidiar con la cantidad excesiva de jitter creando un delay. Si el retraso es adecuado como $t_2$ entonces nos llegan todos los paquetes antes de tener que reproducirlos, pero si usamos $t_1$ entonces perderemos algunos paquetes y se nos cortará el audio, a pesar de que los paquetes te llegarán antes. En este caso está fijo el delay.

![[Pasted image 20240523224929.png]]
- Talkspurt $\to$ Ráfaga de voz. Segmento continuo de habla después de un periodo en el que lo único que se escucha es ruido de fondo.
- En la imagen anterior tenemos un delay fijo, o uno que puede ser recalculado al inicio de una ráfaga de voz.
- Usaremos las siguientes variables:
	- $t_i$ : El momento en el que el paquete i se genera en el sending host.
	- $a_i$ : El tiempo en el que el paquete i es recibido en el host receptor
	- $p_i$ : El momento en el que el paquete i es reproducido en el host receptor.
	- $D_{prop}$ : El retraso de propagación del emisor al receptor, que se asume constante a lo largo de la vida de una conexión de audio.
	- $v_i$ : El retraso de cola experimentado por el paquete i al ser mandado del host fuente al host destino.
	- $b_i$ : El tiempo que el paquete i pasa en el buffer en el receptor, esperando el momento en el que se lo reproduzca $b_i = p_i - a_i$ 
	- $d_i$ : La cantidad de tiempo desde que el paquete i es generado en la fuente hasta que es reproducido en el destino. Retraso de reproducción. $d_i = p_i - t_i$.
	- $n_i$ : El retraso total introducido por la red. $n_i = a_i - t_i$.

![[Pasted image 20240523232406.png]]

- Todos los algoritmos siguen el método de medición de tiempo absoluto (absolute timing method) definido por Montgomery.
- Si el paquete i es el primero en una ráfaga de voz, su tiempo de reproducción se computa como $$p_i = t_i + \hat d_i + 4 * \hat v_i$$ donde $\hat d_i$ y $\hat v_i$ son estimaciones del delay promedio y la variación del delay de la transmisión durante la ráfaga de voz.
- Se computan los siguientes paquetes como $$p_j = p_i + t_j - t_i$$
- Los cuatro algoritmos que estudiaremos difieren únicamente en la manera en la que se calcula $\hat d_i$  La variación se calcula igual.
### Algoritmo 1

- RFC793
- Se sigue la técnica de Van Jacobson de como calcular el RTT para el temporizador de retransmisión de TCP.
- La estimación del retraso del paquete i se computa tal que $$\hat d_i = \alpha * \hat d_{i - 1} + (1 - \alpha) * n_i$$ y la variación se computa como $$\hat v_i = \alpha \hat v_{i - 1} + (1-\alpha) |\hat d_{i} - n_1|$$
- Este algoritmo es básicamente un filtro linear recursivo y se caracteriza por el factor con peso $\alpha$. Este se eligió 0.998002 en los experimentos.

### Algoritmo 2

- Es parecido al primer algoritmo, pero se tiene una segunda variable $\beta$ que se usa para cuando hay una tendencia a un retraso  que aumenta, y $\alpha$ cuando tiene a decrecer
- Si $(n_i > \hat d_i)$ entonces $$\hat d_i = \beta * \hat d_{i - 1} + (1 - \beta) * n_i$$ sino $$\hat d_i = \alpha * \hat d_{i - 1} + (1 - \alpha) * n_i$$
- En los estudios se eligió a beta como 0.75.

### Algoritmo 3

- Siendo $S_i$ un set con todos los paquetes recibidos durante la ráfaga de voz antes del que inicia i, se estima la tardanza $$\hat d_i = \text{min}_{j \in S_i}\{n_j\}$$

### Algoritmo 4

- Al examinar muchas trazas de paquetes, los autores del libro se dieron cuenta de frecuente picos de retraso.
![[Pasted image 20240524002228.png]]

- Un pico constituye una un incremento repentino y largo en el retraso de punta a punta $n_i$ , seguido de una gran cantidad de paquetes llegando casi instantaneamente, concluyendo con el pico.
- Los primeros 3 algoritmos no se adaptan lo suficientemente rápido a estos picos, no pudiendo cambiar sus estimaciones de retraso a tiempo. Este algoritmo sí lo hace.
- Lo que hacemos es establecer un valor tal que si la diferencia entre el retraso de un paquete con otro lo supera, consideramos que estamos ante un spike. $$\text{if} (abs(n_i - n_{i-1})) > spike\_threshold): mode = IMPULSE$$
- Una vez en el modo impulso al detectar un pico, entonces seguimos a este. Por lo cual, nos fijamos únicamente en los valores más recientes para calcular el futuro retraso $$\text{if} (mode == IMPULSE): \hat d_i = \hat d_{i-1} + n_i - n_{i- 1}$$
- Ahora, será necesario detectar también entonces la finalización de un pico. Si vemos bien el gráfico del pico, vemos como el delay (eje y) al principio es muy grande, pero con el pasar de los paquetes se va haciendo menor. Lo que hacemos para detectar el final de un pico es ir actualizando una variable con la pendiente entre los últimos paquetes que llegaron, y cuando esta llegue a un punto de ser lo suficientemente bajo, se considera que se terminó el spike y el algoritmo vuelve al modo normal $$var = \frac{var}{2} + \text{abs}\left (\frac{(n_i - n_{i-1})}{8} + \frac{(n_i - n_{i-2})}{8}\right )$$ $$if(var \le var\_threshold): mode = NORMAL$$el valor que determinará si terminó es $$\text{abs}(2n_i - n_{i - 1} - n_{i - 2})$$ $$\hat d_i = 0.125*n_i + 0.875 * \hat d_{i - 1}$$
![[Pasted image 20240524153520.png]]

### Tests

- Se usó UDP.
- Se transmitieron 160 bytes de datos cada 20 milisegundos
- Una de nuestras principales métricas de rendimiento es el porcentaje de paquetes perdidos en el host receptor. Dicha pérdida resulta ya sea de la llegada tardía de un paquete (es decir, la llegada de un paquete después de su tiempo de reproducción programado) o de una llegada extremadamente prematura de un paquete. En este último caso, la pérdida de paquetes resulta de una limitación en el tamaño del búfer de almacenamiento de audio finito.
- Si estamos reproduciendo el paquete número i y nuestro buffer solo puede sostener k paquetes, entonces cualquier paquete con número mayor a i + k que nos llegue será descartado.
- 6 y 7 muy lossy 20% a 30%.
- 1 y 2 2% a 10%
- 3, 4, 5 1% a 4%
- Figura 7, trace 1 con 2-10% de packet loss. Se compara el porcentaje de paquetes perdidos versus el retraso promedio de reproducción de los paquetes que sí fueron reproducidos.
	- El retraso promedio se le resta el $d_i$ más pequeño para que solo represente el retraso desde que llega hasta que es reproducido y no los retrasos de propagación de la red.
	- Vemos que el algoritmo 4 se desempeña mejor que el algoritmo 1 y 3 en el ratio que nos interesa.
	- El 2do algoritmo tiene un bajo rendimiento. A pesar de ser efectivo para reducir la cantidad de retransmisiones en TCP, genera un delay más grande en los paquetes de audio sin tener ninguna ganancia adicional.

![[Pasted image 20240524164702.png]]

![[Pasted image 20240524164735.png]]



# Presentación

Buenos tardes profesor, mi nombre es Rafael Berenguel y a continuación estaré hablando acerca del paper Mecanismos de reproducción adaptativos para aplicaciones de audio paquetizado en redes de área amplia (WAN), escrito por Ramachandran Ramjee, Jim Kurose, Don Towsley y Henning Schulzrinne.

El paper fue publicado en 1994, época por la cual se estaba haciendo cada vez más común ver que gente se comunique con audio a través de internet, teniendo cada vez más ejemplos de casos en los que esto se logró.

Esto se hacía a través de un sistema de buffers y retrasos en la reproducción del audio. Como lo podemos poner en el lenguaje de lo visto en la materia, es más claro verlo con un ejemplo.

Podemos ver que tenemos un sender que genera paquetes de audio de manera periódica, lo cual podemos apreciar por la forma de escalera que vemos. Por otra parte, podemos ver como al host que recibe los paquetes, estos no le llegan en intervalos consistentes, sino que debido a retrasos en la red, estos pueden llegar antes o después. Debido a esto, en vez de reproducirlos apenas llegan, el receptor va a poner el paquete en un buffer y va a asignar un retraso para reproducirlo, así dará tiempo a que lleguen algunos de los paquetes siguientes y se pueda reproducir el audio de manera continua. Como vemos si elegimos $t_2$ todo bien, pero si elegimos $t_1$ perderemos algunos paquetes.

Como vemos, un retraso fijo no es lo más conveniente, por lo que el objetivo de este paper, la razón por la que fue hecho, fue para evaluar diferentes algoritmos con los que se decide el nuevo valor del retraso, el cual va variando a lo largo de la conexión

Antes de pasar a ver los algoritmos, definamos dos variables que usaremos mucho. Un es $n_i$, la cual se define como el retraso total de red y simboliza el tiempo transcurrido desde que el paquete fue generado hasta que efectivamente llegó al receptor. Luego tenemos $d_i$, el cual es $n_i$ sumado el tiempo que tuvo que esperar el paquete en el buffer para ser reproducido. El retraso de reproducción es la variable que intentamos estimar.

El primer algoritmo es usado para la estimación de RTT en TCP y es básicamente una ecuación recursiva lineal en la que estimamos el momento en el que se reproducirá un paquete i en base a la estimación del paquete previo y al tiempo de llegada del paquete. También tenemos la presencia de una variable $\alpha$ cuyo valor fue asignado después de experimentar.

El segundo algoritmo es muy parecido al primero, con la diferencia de que ahora tendremos una segunda variable $\beta$ que se utilizará cuando se detecte que el tiempo que tardan los paquetes en llegar está aumentando.

El tercer algoritmo es el algoritmo de adaptación de retraso y estima el retraso como el mínimo de los retrasos de red de los anteriores paquetes en la ráfaga de voz actual.

Al examinar muchas trazas de paquetes, los autores del libro se dieron cuenta de frecuente picos de retraso, en los que sucesivamente nos llegaban muchos paquetes de audio después de un periodo en el que no nos llega ninguno. Este fenómeno se vio que generaba muchas pérdidas de paquetes, pues los 3 algoritmos presentados con anterioridad no pueden actualizar sus estimaciones de cuando se tiene que reproducir el audio lo suficientemente rápido, llevando a la pérdida de muchos paquetes. Es por esto que los autores del libro proponen un nuevo algoritmo que lidia bien con picos.

El algoritmo va a tener dos modos, dependiendo de si está en un pico o no. Para detectar un pico, nos fijaremos si la diferencia de los dos últimos retrasos de red es menor a un threshold que definimos, lo cual nos indica que los paquetes empezaron a llegar a una velocidad que consideramos un pico.

Sin embargo, también habrá que saber cuando salimos de este pico, para lo cual utilizamos otra fórmula. Entonces, dependiendo del estado en el que nos encontremos, usaremos una fórmula como la del algoritmo 1 o, una fórmula que va a estar especializada para las situaciones de picos en donde el cambio es tan rápido que intentamos seguir al pico, fijándonos solamente en los valores inmediatamente anteriores a nosotros.

| Trace# | Sender | Receiver |
| ------ | ------ | -------- |
| 1      | INRIA  | UMASS    |
| 2      | INRIA  | UMASS    |
| 3      | UCI    | UMASS    |
| 4      | UCI    | UMASS    |
| 5      | UCI    | INRIA    |
| 6      | OSAKA  | UMASS    |
| 7      | OSAKA  | UMASS    |