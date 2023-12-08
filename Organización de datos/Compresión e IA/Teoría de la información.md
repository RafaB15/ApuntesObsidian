![[Organización de datos/Compresión e IA/Teoría de la información/Untitled.png|Untitled]]

### Bits de información:

Es cuanta información estoy dando en bits.

Esto depende de la probabilidad de un evento

Ej: “¿Cual es la probabilidad de que mañana salga el Sol?

Por Laplace

$$
P(\text{sale el sol)} = \frac{\text{\# días que salió el sol}}{\# días totales} = 1
$$

Pero como queremos también ver la probabilidad de que eventos que nunca pasaron puedan pasar utilizamos el ajuste de Laplace

$$
P(\text{sale el sol)} = \frac{\text{\# días que salió el sol} +1}{\text{\# días totales} + 2} = 0-99999999...
$$

$$
P(\text{no sale el sol}) = 6.0318... * 10^{-13}
$$

¿Cual es la menor cantidad de bits que necesito para mandar esta información?

$$
\text{bits} = -\log_2(P(\text{algo})) 
$$

Si usábamos que la probabilidad de que salga el Sol es uno me da 0 bits, debido a que siempre ocurre por lo que no tiene sentido tener que comunicarlo.

Usando la probabilidad obtenida con el ajuste de Laplace entonces tenemos

$$
\text{bits}_{\text{ sale sol}} = 8.7014 * 10^{-13}
$$

Es muy baja porque pasa mucho, es algo común por lo que no gastamos muchos bits.

$$
\text{bits}_{\text{ no sale sol}} = 40.5926
$$

Como esto no pasa mucho no me importa usar muchos bits, como casi nunca sucede es mucha información. 

![[Organización de datos/Compresión e IA/Teoría de la información/Untitled 1.png|Untitled]]

### Entropía de Shannon

Son los bits promedio que voy a gastar por cada mensaje que mande.

Para las monedas

$$
H = -\frac{1}{2}*\log_2(\frac{1}{2})-\frac{1}{2}*\log(\frac{1}{2}) \\  = \frac{1}{2}*1 + \frac{1}{2}*1 = 1
$$

La formula es

$$
H = -\sum_i P_i*\log_2(P_i)
$$

 

### Entropía cruzada

  Si tengo el sistema 

![[Organización de datos/Compresión e IA/Teoría de la información/Untitled 2.png|Untitled]]

Calculo la entropía de shannon y me da $1.9219$. Pero me doy cuenta que calculé mal las probabilidades y en realidad eran.

![[Organización de datos/Compresión e IA/Teoría de la información/Untitled 3.png|Untitled]]

Su entropía de shannon me da exactamente igual, sin embargo por el cambio en las probabilidades estaré mandando diferentes cantidades de bits en diferentes frecuencias.

Para calcular este error utilizamos la entropía cruzada. 

![[Organización de datos/Compresión e IA/Teoría de la información/Untitled 4.png|Untitled]]

Usamos las probabilidades reales (de la tabla P) con los bits de la tabla Q.

La fórmula general es

$$
H(p,q) =-\sum_{i=1}^nP_i*\log_2(Q_i)
$$

### Divergencia de Kullback-Leiber

$$
H(p,q) =-\sum_{i=1}^nP_i*\log_2(Q_i) = H_P + D_{KL(p||q)}
$$

La divergencia de Kullback-Leiber es el precio que estoy pagando por el error

$$
D_{KL(p||q)} = \sum_sP(s)\ln\frac{P(s)}{Q(s)}
$$

Entonces:

- El ajuste de Laplace se usa para calcular la probabilidad de eventos que nunca sucedieron.
- Los bits de un mensaje nos permiten saber cuál es la mejor cantidad posible de bits a gastar en el mismo.
- La entropía de Shannon nos indica qué tan impredecible es un fenómeno.
- La entropía cruzada nos da una mediad de qué tan distintas son dos distribuciones de probabilidad.
- La divergencia de KL nos da otra métrica de lo mismo.