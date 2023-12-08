## **Teorema Fubini-Tonelli:**

Si la función $f(x,y)$ es integrable Riemann en el rectángulo $[a,b] x [c,d]$, entonces para cada $y$, $f(x,.)$ es integrable con respecto a $x$ en $[a,b]$ y para cada $x$, $f(.,y)$ es integrable con respecto a $y$ en $[c,d]$.

Además

                     $\displaystyle \iint_Rf(x,y)dxdy=\int_c^d[\int_a^bf(x,y)dx]dy=\int_a^b[\int_c^df(x,y)dy]dx$

## Integrales dobles sobre regiones generales:

Regiones más generales se descompondrán en varias regiones simples que no se solapen; se recurrirá luego a la propiedad de aditividad de la integral doble

                    $\displaystyle\iint_{R_1UR_2}f(x,y)dxdy=\iint_{R_1}f(x,y)dxdy+\iint_{R_2}f(x,y)dxdy$

### Regiones tipo 1:

![[Análisis Matemático A/8 - Integrales múltiples/PDF - Integrales dobles/Untitled.png|PDF%20-%20Integrales%20dobles%200c8086f372aa47c3a8b4e8480eb4134d/Untitled.png]]

Para integrar $f(x,y)$ sobre la región $R$, suponiendo que es integrable, sobre un rectángulo que contenga a R, se calcula

                                 $\displaystyle\iint_Rf(x,y)dxdy=\int_a^b[\int_{\psi_1(x)}^{\psi_2(x)}f(x,y)dy]dx$

Puede leerse del siguiente modo: Para cada valor de $x$ entre $a$ y $b$, la $y$ se mueve entre $y = \psi_1(x)$ e $y = \psi_2(x)$.

### Regiones tipo 2:

![[Análisis Matemático A/8 - Integrales múltiples/PDF - Integrales dobles/Untitled 1.png|PDF%20-%20Integrales%20dobles%200c8086f372aa47c3a8b4e8480eb4134d/Untitled%201.png]]

Para integrar $f(x,y)$ sobre la región $R$, suponiendo que es integrable, sobre un rectángulo que contenga a R, se calcula

                                 $\displaystyle\iint_Rf(x,y)dxdy=\int_c^d[\int_{\psi_1(y)}^{\psi_2(y)}f(x,y)dx]dy$

Puede leerse del siguiente modo: Para cada valor de $y$ entre $c$ y $d$, la $x$ se mueve entre $x = \psi_1(y)$ y $x = \psi_2(y)$.

## Aplicaciones físicas de las integrales dobles:

### Masa de una chapa:

**Densidad superficial del material →** El espesor se considera despreciable y se calcula cuantas unidades de masa corresponden a una unidad de área de la chapa.

Si la densidad es constante calculamos la masa multiplicando la densidad por el área

                                              $\displaystyle M = \delta.Área(R)=\delta\iint_R1dxdy$

Si la densidad varía con cada punto, siendo esta una función $\delta (x,y)$, calculamos la masa

                                                   $\displaystyle M=\iint_R\delta(x,y)dxdy$

### Centro de masa de una chapa:

                   $\displaystyle x_{cm}=\frac{\iint_Rx.\delta(x,y)dxdy}{\iint_R\delta(x,y)dxdy}$      $\displaystyle y_{cm}=\frac{\iint_Ry.\delta(x,y)dxdy}{\iint_R\delta(x,y)dxdy}$    

### Momento de inercia de una chapa con respecto a un eje:

Si la distancia de cada punto de la chapa al eje E es $d_{_E}(x,y)$, entonces el momento de inercia de la chapa completa respecto del eje E es

                                               $\displaystyle I_{_E} = \iint_Rd_{_E}^2(x,y).\delta(x,y)dxdy$

El momento de inercia respecto del eje $y$ es

                                               $\displaystyle I_{_Y} = \iint_Rx^2\delta(x,y)dxdy$

El momento de inercia respecto del eje $x$ es

                                               $\displaystyle I_{_X} = \iint_Ry^2\delta(x,y)dxdy$

## Valor medio de una función:

Si $f(x,y)$ es cualquier función continua definida en $D$ entonces

                                           $\displaystyle f_{med} = \frac{1}{Área(D)}\iint_Df(x,y)dxdy$

## Cambio de coordenadas en integrales dobles:

![[Análisis Matemático A/8 - Integrales múltiples/PDF - Integrales dobles/Untitled 2.png|PDF%20-%20Integrales%20dobles%200c8086f372aa47c3a8b4e8480eb4134d/Untitled%202.png]]

La función $\vec{X}(u,v)=(x(u,v),y(u,v))$ realiza el cambio de coordenadas.

El cambio de coordenadas en una integral doble se expresa en una ecuación que incluye al módulo del jacobiano

               $\displaystyle \iint_Rf(x,y)dxdy=\iint_{R^{*}}f(x(u,v),y(u,v))\begin{Vmatrix}{x'_u}&{x'_u}\\{y'_v}&{y'_u}\end{Vmatrix}dudv$

### Caso especial: Cambiar a coordenadas polares:

Un cambio muy común es a coordenadas polares.

Para pasar de coordenadas cartesianas a polares usamos:

                                                         $\displaystyle \begin{cases}x=rcos(\theta)\\y=rsen(\theta)\end{cases}$

Para pasar de coordenadas polares a cartesianas:

                                                         $\displaystyle \begin{cases}r=\sqrt{x^2+y^3}\\ \theta=tan^{-1}\frac{x}{y}\end{cases}$

Con lo cual la fórmula del cambio de variable sería:

                           $\displaystyle \iint_Rf(x,y)dxdy=\iint_{R^*}f(rcos(\theta),rsen(\theta))rdrd\theta$

Si estamos en el caso de una elipse de eje mayor y menor a y b el jacobiano es abr