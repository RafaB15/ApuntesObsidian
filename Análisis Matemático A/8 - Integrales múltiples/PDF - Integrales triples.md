La integral triple es de la forma

                                                         $\displaystyle \iiint_Vf(x,y,z)dxdydz$

## Teorema Fubini-Tonelli:

Si la función $f(x,y,z)$ es integrable Riemann en el paralelepípedo [a,b] X [c,d] X [e,g], entonces f(x, y, .) es integrable en [𝑎, 𝑏] × [𝑐, 𝑑] , 𝑓(𝑥, . , 𝑧) lo es en [𝑎, 𝑏] × [𝑒, 𝑔] y 𝑓(. , 𝑦, 𝑧) lo es en [𝑐, 𝑑] × [𝑒, 𝑔].

Además,

                            $\displaystyle\iiint_Vf(x,y,z)dxdydz=\iint_{[a.b]x[c,d]}[\int_e^gf(x,y,z)dz]dxdy$

                            $\displaystyle=\iint_{[a,b]x[e,g]}[\int_c^df(x,y,z)dy]dxdz=\iint_{[c,d]x[e,g]}[\int_a^bf(x,y,z)dx]dydz$

## Integrales triples sobre regiones más generales:

![[Análisis Matemático A/8 - Integrales múltiples/PDF - Integrales triples/Untitled.png|PDF%20-%20Integrales%20triples%200ebe628947c74a8282c3c2e2f84e80b9/Untitled.png]]

Se trata de lo que llamaremos “cuerpo proyectable sobre un plano coordenado”: considerando la proyección $P_{xy}(V)$ del cuerpo $V$, cada punto $(x,y)$ de esa proyección tiene la propiedad de que una recta ortogonal al plano de la proyección en ese punto atraviesa a la frontera del sólido únicamente en dos puntos $(x,y,\varphi_{_1}(x,y))$ y $(x,y,\varphi_{_2}(x,y))$, con las $\varphi_i$ funciones continuas o continuas a trozos sobre $P_{xy}(V)$.

La integral se calculará del siguiente modo:

                             $\displaystyle\iiint_Vf(x,y,z)dxdydz = \iint_{P_{xy}(V)}[\int^{\varphi_2(x,y)}_{\varphi_1(x,y)}f(x,y,z)dz]dxdy$

Regiones más generales se descompondrán en varias regiones proyectables que no se solapen y se sumarán.

- Si $f(x,y,z) = 1$    $\forall(x,y,z)\in D$ entonces

                                                  $\displaystyle \text{Volumen(D)} = \iiint_Ddxdydz$

- Si $\delta(x,y,z)$ = "densidad volumétrica de masa" entonces

                                                         $\displaystyle \text{Masa(D)}= \iiint_D\delta(x,y,z)dxdydz$

- Si $f(x,y,z)$ es cualquier función continua definida en D entonces

                                          $\displaystyle f_{med}=\frac{1}{\text{Volumen D}}\iiint_Df(x,y,z)dxdydz$

## Centro de masa:

                   $\displaystyle x_{cm}=\frac{\iiint_Dx.\delta(x,y,z)dxdydz}{\iiint_D\delta(x,y,z)dxdydz}$      $\displaystyle y_{cm}=\frac{\iiint_Dy.\delta(x,y,z)dxdydz}{\iiint_D\delta(x,y,z)dxdydz}$    

                                            $\displaystyle z_{cm}=\frac{\iiint_Dz.\delta(x,y,z)dxdydz}{\iiint_D\delta(x,y,z)dxdydz}$

## Cambio de coordenadas en integrales triples:

### Cartesianas → Cilíndricas:

Serán útiles en el caso de simetría circular alrededor de un eje.

Si el eje de rotación fuera el **z**.

                               $\displaystyle\begin{cases}x=rcos(\theta)\\ y=rsen(\theta)\\z=z\end{cases}$                                          $\text{Jacobiana} = r$

                                                           $dx\,dy\,dz\to r\,d\theta\, dr\,dz$

![[Análisis Matemático A/8 - Integrales múltiples/PDF - Integrales triples/Untitled 1.png|PDF%20-%20Integrales%20triples%200ebe628947c74a8282c3c2e2f84e80b9/Untitled%201.png]]

## Cartesianas → Esféricas:

Serán útiles cuando los recintos de integración involucren esferas y/o conos, o cuando el integrando presente simetría de carácter esférico.

![[Análisis Matemático A/8 - Integrales múltiples/PDF - Integrales triples/Untitled 2.png|PDF%20-%20Integrales%20triples%200ebe628947c74a8282c3c2e2f84e80b9/Untitled%202.png]]

                      $\displaystyle P: \begin{cases}x=\rho sen(\varphi)cos(\theta)\\ y=\rho sen(\varphi)sen(\theta)\\z=\rho cos(\varphi)\end{cases}$                         $\text{Jacobiana}=\rho^2sen(\varphi)$

                                                      $dx\, dy\,dz\to \rho sen^2(\varphi)\,dp\,d\varphi\, d\theta$

![[Análisis Matemático A/8 - Integrales múltiples/PDF - Integrales triples/Untitled 3.png|PDF%20-%20Integrales%20triples%200ebe628947c74a8282c3c2e2f84e80b9/Untitled%203.png]]