## Integrales de superficie de tipo escalar:

Suponiendo que se tiene una superficie **S** con una parametrización suave $\vec{\sigma}(u,v)$

                                  $\displaystyle Área (S) = \iint_Sd\sigma = \iint_D ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv$

El resultado de esta integral no depende de la parametrización que se haya elegido para la superficie.

Si la densidad del material en cada punto es $\delta(x,y,z)$, podemos calcular la masa de la siguiente forma

          $\displaystyle M=\iint_S\delta d\sigma = \iint_D \delta(x(u,v),y(u,v),z(u,v)) ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv$

Las correspondientes coordenadas del centro de masa estarán dadas por

    $\displaystyle x_{cm} = \frac{\iint_Sx\delta d\sigma}{\iint_S\delta d\sigma} =\frac{ \iint_D x(u,v)\delta(x(u,v),y(u,v),z(u,v)) ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv}{\iint_D \delta(x(u,v),y(u,v),z(u,v)) ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv}$

    $\displaystyle y_{cm} = \frac{\iint_Sy\delta d\sigma}{\iint_S\delta d\sigma} =\frac{ \iint_D y(u,v)\delta(x(u,v),y(u,v),z(u,v)) ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv}{\iint_D \delta(x(u,v),y(u,v),z(u,v)) ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv}$

    $\displaystyle z_{cm} = \frac{\iint_Sz\delta d\sigma}{\iint_S\delta d\sigma} =\frac{ \iint_D z(u,v)\delta(x(u,v),y(u,v),z(u,v)) ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv}{\iint_D \delta(x(u,v),y(u,v),z(u,v)) ||\vec{\sigma}'_u(u,v)X\vec{\sigma}'_v(u,v)||dudv}$

## Integrales de superficie de tipo vectorial:

Suponiendo que se tiene una superficie **S** con una parametrización suave

                                    $\vec{\sigma}(u,v)=(x(u,v),y(u,v),z(u,v))$  

con $(u,v) \in D \subset R^2$ el calculo del flujo adquiere la forma:

          $\displaystyle \varPhi_S(\vec{f})=\iint_S\vec{f}|_s.d\vec{\sigma}=\iint_S\vec{f}(x(u,v),y(u,v),z(u,v)).(\vec{\sigma}'_u(u,v)X(\vec{\sigma}'_v(u,v))dudv$

Es posible seleccionar, con un simple cambio de signo, el sentido de la normal a la superficie que deseamos considerar.