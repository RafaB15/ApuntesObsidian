## Longitud de una curva:

Supongamos que tenemos en el espacio tridimensional una curva **C**, parametrizada regularmente.

                                        $\displaystyle C: \overrightarrow{X}(t) = (x(t), y(t), z(t))$   para $\displaystyle t$ ∈ $[a,b]$

Solicitamos que se cumpla la hipótesis adicional de que la función que corresponde al vector derivado $\displaystyle \overrightarrow{X}'(t)$ varíe con continuidad en el intervalo $(a,b)$.

![[Análisis Matemático A/7 - Integrales curvilíneas/PDF - Integrales curvilíneas/Untitled.png|PDF%20-%20Integrales%20curvili%CC%81neas%202df39308060e44068347f6971a5945d3/Untitled.png]]

Llamaremos **longitud de arco de curva C** a la siguiente integral:

                                               $\displaystyle Long(C) = \int_c ds = \int_a^b ||\overrightarrow{X}'(t)|| dt$

## Masas, centros de masa y otras magnitudes físicas:

### Densidad:

La densidad la calculamos como

                                                                      $\displaystyle \delta = \frac{M}{V}$

Cuando la longitud es la magnitud predominante (como en cables y sogas), es común que se defina la **densidad lineal**.

Si el material es homogéneo, la densidad lineal se calcula 

                                                                      $\displaystyle \delta = \frac{M}{L}$

por lo que para averiguar la masa, solo necesitaríamos calcular la longitud y multiplicarla por la densidad.

                                                                      $M = \delta L$

Si el material no es homogéneo, la densidad será una función que puede cambiar punto a punto.

Si la densidad del material es una función $\delta(x, y, z)$ que cambia punto a punto, su masa se puede calcular así:

                                              $\displaystyle M = \int_C \delta ds = \int_b^a \delta(\overrightarrow{X}(t))||\overrightarrow{X}'(t)||dt$

Para calcular la densidad media usamos

                                                               $\displaystyle \delta_{media} = \frac{M_{total}}{l_{total}}$

### Centro de masa:

Recordemos que para calcular el centro de masa usamos

                                       $\displaystyle x_{cm} = \frac{\sum_{i = 1}^n x_i m_i}{\sum_{i = 1}^nm_i}$

                                       $\displaystyle y_{cm} = \frac{\sum_{i = 1}^n y_i m_i}{\sum_{i = 1}^nm_i}$

                                       $\displaystyle z_{cm} = \frac{\sum_{i = 1}^n z_i m_i}{\sum_{i = 1}^nm_i}$

Aunque para nuestros propósitos nos será más útil usar 

                                                  $\displaystyle x_{cm} = \frac{\int_cxdm}{\int_cdm}= \frac{\int_cx\delta ds}{\int_c\delta ds}$

                                                  $\displaystyle y_{cm} = \frac{\int_cydm}{\int_cdm}= \frac{\int_cy\delta ds}{\int_c\delta ds}$

                                                  $\displaystyle z_{cm} = \frac{\int_czdm}{\int_cdm}= \frac{\int_cz\delta ds}{\int_c\delta ds}$

recordar que $m = \delta l$ → $dm = \delta ds$.

### Momento de inercia:

Para calcular el momento de inercia de un sistema de masas con respecto a un eje, se debe multiplicar cada masa por el cuadrado de su distancia al eje considerado y sumar luego todos esos productos. 

Lo calculamos para un alambre para cualquier eje de la siguiente manera

                       $\displaystyle I_e = \int_c d^2dm = \int_cd^2\delta ds = \int_a^bd^2(\overrightarrow{X}(t))\delta (\overrightarrow{X}(t))||\overrightarrow{X}'(t)||dt$ 

## Invariancia de la integral de curvilínea respecto de la parametrización:

Las magnitudes físicas escalares que puedan evaluarse sobre curvas responden a la forma

                                              $\displaystyle \int_C f ds = \int_b^a f(\overrightarrow{X}(t))||\overrightarrow{X}'(t)||dt$

donde la magnitud física escalar $f(x, y, z)$ se evalúa sobre los puntos de la curva y luego se integra  a lo largo de ella.

Esa magnitud es la función constante 1 en el caso de la longitud, es la densidad del material en el caso de la masa, es la densidad por la distancia a un eje al cuadrado en el caso del momento de inercia, etc.

Se puede demostrar que el valor de  $\int_C f ds$ no depende de la parametrización de la curva $C$.

## Cambiar de sentido una curva:

Si tenemos una curva  $C :(x(t), y(t), z(t))$ con t perteneciente a $[a,b]$, podemos parametrizarla cambiándole el sentido intercambiando $t$ por **-**$u$ y que el intervalo sea $[-b,-a]$.

## Integral curvilínea de campos vectoriales:

Tenemos una curva suave $\overrightarrow{X}(a)$  y un campo vectorial continuo $\overrightarrow{f} (x, y, z)$: 

![[Análisis Matemático A/7 - Integrales curvilíneas/PDF - Integrales curvilíneas/Untitled 1.png|PDF%20-%20Integrales%20curvili%CC%81neas%202df39308060e44068347f6971a5945d3/Untitled%201.png]]

El trabajo total de la fuerza, cuando la partícula se desplaza desde el punto inicial $\overrightarrow{X}(a)$ al punto final $\overrightarrow{X}(b)$, estará dado por la expresión.

                                     $\displaystyle L_c (\overrightarrow{f}) = \int_c \overrightarrow{f}.\overrightarrow{ds} = \int_a^b\overrightarrow{f}(\overrightarrow{X}(t)).\overrightarrow{X}'(t)dt$

El valor de  $\int_c \overrightarrow{f}.\overrightarrow{ds}$ no depende de la parametrización de la curva C, sin embargo cambia de signo si le cambiás el sentido a la curva.

## Función potencial y Campos de gradiente:

Sea $\overrightarrow{F}: H \subset R^{m} \to R^m$. Se dice que $\overrightarrow{F}$ en un campo de gradiente en $H$ si existe una función $\phi: H \subset R^{m} \to R, \phi \in Dif(H)$ tal que

                                                                         $\overrightarrow{F} = \nabla\phi$

Si $\overrightarrow{F} = \nabla\phi$ también se dice que la función $\phi$ es el potencial del campo $\overrightarrow{F}$.

## Independencia del camino en integral de línea de campo vectorial:

Sea $\overrightarrow{F}$ un campo de gradiente entonces la circulación de $\overrightarrow{F}$ desde $\overrightarrow{A}$ hasta $\overrightarrow{B}$ a lo largo de cualquier curva suave a trozos $C \subset H$ no depende de la curva que se utilice

                                                           $\displaystyle \int_{C1}\overrightarrow{F}.\overrightarrow{ds} = \int_{C2}\overrightarrow{F}.\overrightarrow{ds}$

 y además

                                                          $\displaystyle \int_{C_{AB}} \overrightarrow{F}\overrightarrow{ds} = \phi (\overrightarrow{B}) - \phi(\overrightarrow{A})$

Si se cumple esto, también se cumple que

- La integral a lo largo de todo camino cerrado es cero.
- Si $\overrightarrow{F} = \nabla \phi$ tenemos que si $\phi(\overrightarrow{B}) = \phi(\overrightarrow{A})$ entonces

                                                         $\displaystyle \int_{C_{AB}} \overrightarrow{F}\overrightarrow{ds} = \phi (\overrightarrow{B}) - \phi(\overrightarrow{A}) = 0$

por lo que se cumple que 

                                                                 $\displaystyle \oint_C \overrightarrow{F}.\overrightarrow{ds} = 0$

cualquiera sea la curva cerrada C contenida en D.

## Campos conservativos:

Si $\overrightarrow{F}$ es un campo de fuerza y $\overrightarrow{F} = \nabla\phi$ se dice que $\overrightarrow{F}$ es un campo conservativo.

El trabajo de un campo conservativo es nulo a lo largo de cualquier curva cerrada y entre puntos de igual potencial.

Que la matriz jacobiana de $\overrightarrow{F}$  sea simétrica y el que dominio de esta sea simplemente conexo son condiciones necesarias y suficientes para que $\overrightarrow{F}$  sea conservativa.

## Calcular funciones potenciales:

![[Análisis Matemático A/7 - Integrales curvilíneas/PDF - Integrales curvilíneas/Untitled 2.png|PDF%20-%20Integrales%20curvili%CC%81neas%202df39308060e44068347f6971a5945d3/Untitled%202.png]]