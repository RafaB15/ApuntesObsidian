## Ondas Estacionarias:

Superposición de ondas de igual frecuencia que viajan en sentidos opuestos.

**Nodo                       →** Punto cuya posición **y** es siempre 0. 

**Antinodo / Vientre →** Punto cuya posición **y** es la amplitud.

Onda 1:    $\xi_1=Asen(kx-wt)$

Onda 2:    $\xi_2=Asen(kx+wt)$

                $\xi_{total}=\xi_1+\xi_2=Asen(kx-wt)+Asen(kx+wt)$

                                                     $\boxed{\xi_{total}=\underbrace{2Asen(kx+(\frac{\varphi_1+\varphi_2}{2}))}_{\text{A(x)}}cos(wt+(\frac{\varphi_1-\varphi_2}{2}))}$

La amplitud será cero en los nodos y $2A$ en los vientres.

### En cuerdas:

- **Ambos extremos fijos**
    
    Si ponemos el origen en un extremo de la cuerda
    
    ![[Física I/Ondas/Superposición de ondas/Untitled.png|Superposicio%CC%81n%20de%20ondas%20944d9661f4a4457ab50e847bc19ebe56/Untitled.png]]
    
    $\xi_t(x=0)=2Asen(k0)cos(wt)=0$
    
    $\xi_t(x=L)=2Asen(kL)cos(wt)=0$
    
    Se podrán logran ondas estacionarias solo para ciertas frecuencias que cumplan que
    
                                                                     $sen(KL)=0$
    
    - $\displaystyle KL=n\pi\implies\frac{2\pi}{\lambda_n}L=n\pi$            $(n=1,2,3,...)$
    - $\displaystyle L = n\frac{\lambda_n}{2} \implies \frac{2L}{n}= \lambda_n$
    - $\displaystyle f_n=\frac{v}{\lambda_n}=\frac{n}{2L}v=\frac{n}{2L}\sqrt{\frac{T}{\mu}}$     (con $n$ representando el número de vientres)
    
    ![[Física I/Ondas/Superposición de ondas/Untitled 1.png|Superposicio%CC%81n%20de%20ondas%20944d9661f4a4457ab50e847bc19ebe56/Untitled%201.png]]
    
- **Un extremo fijo y el otro suelto**
    
    En uno de los extremos habrá un nodo y en el otro un máximo (vientre).
    
    $\xi_t(x=0)=2Asen(k0)cos(wt)=0$
    
    $\xi_t(x=L)=2Asen(kL)cos(wt)=\text{Máximo}$
    
                                                                $sen(KL)=\pm1$
    
    - $\displaystyle KL=(2n+1)\frac{\pi}{2} \implies \frac{2\pi}{\lambda_n}L=(2n+1)\frac{\pi}{2}$        $(n=1,2,3,...)$
    - $\displaystyle L = (2n+1)\frac{\lambda_n}{4}$
    - $\displaystyle f_n = \frac{v}{\lambda_m}=(2n+1)\frac{v}{4L}$
    
    ![[Física I/Ondas/Superposición de ondas/Untitled 2.png|Superposicio%CC%81n%20de%20ondas%20944d9661f4a4457ab50e847bc19ebe56/Untitled%202.png]]
    

### En tubos:

- **Ambos extremos abiertos**
    
    Si ponemos el origen en un extremo
    
    ![[Física I/Ondas/Superposición de ondas/Untitled 3.png|Superposicio%CC%81n%20de%20ondas%20944d9661f4a4457ab50e847bc19ebe56/Untitled%203.png]]
    
    $p_t=p_1+p_2=2Asen(kx)cos(wt)$
    
    $p_t(x=0)=2Asen(k0)cos(wt)=0$
    
    $p_t(x=L)=2Asen(kL)cos(wt)=0$
    
    Se podrán logran ondas estacionarias solo para ciertas frecuencias que cumplan que
    
                                                                     $sen(KL)=0$
    
    - $\displaystyle KL=n\pi\implies\frac{2\pi}{\lambda_n}L=n\pi$            $(n=1,2,3,...)$
    - $\displaystyle L = n\frac{\lambda_n}{2}$
    - $\displaystyle f_n=\frac{v}{\lambda_n}=\frac{n}{2L}v$
- **Ambos extremos abiertos con onda de desplazamiento**
    
    ![[Física I/Ondas/Superposición de ondas/Untitled 4.png|Superposicio%CC%81n%20de%20ondas%20944d9661f4a4457ab50e847bc19ebe56/Untitled%204.png]]
    
    $\xi_1(x,t)= Acos(kx-wt)$
    
    $\xi_2(x,t)= Acos(kx+wt)$
    
    $\xi_t=2Acos(kx)cos(wt)$
    
    Usamos la función coseno porque $cos(0)=\text{Máximo}$
    
     $\xi_{total}(x=0)=2Acos(k0)cos(wt)=Máximo$
    
     $\xi_{total}(x=L)=2Acos(kL)cos(wt)=Máximo$
    
                                    $cos(KL) = \pm1$
    
    - $\displaystyle KL=n\pi\implies\frac{2\pi}{\lambda_n}L=n\pi$            $(n=1,2,3,...)$
    - $\displaystyle L = n\frac{\lambda_n}{2}$
    - $\displaystyle f_n=\frac{v}{\lambda_n}=\frac{n}{2L}v$
    
    ![[Física I/Ondas/Superposición de ondas/Untitled 5.png|Superposicio%CC%81n%20de%20ondas%20944d9661f4a4457ab50e847bc19ebe56/Untitled%205.png]]
    
- **Un extremo abierto y el otro cerrado**
    
    ![[Física I/Ondas/Superposición de ondas/Untitled 6.png|Superposicio%CC%81n%20de%20ondas%20944d9661f4a4457ab50e847bc19ebe56/Untitled%206.png]]
    
    $p_t(x=0)=2Asen(k0)cos(wt)=0$
    
    $p_t(x=L)=2Asen(kL)cos(wt)=\text{Máximo}$
    
                                                                $sen(KL)=\pm1$
    
    - $\displaystyle KL=(2n+1)\frac{\pi}{2} \implies \frac{2\pi}{\lambda_n}L=(2n+1)\frac{\pi}{2}$        $(n=1,2,3,...)$
    - $\displaystyle L = (2n+1)\frac{\lambda_n}{4}$
    - $\displaystyle f_n = \frac{v}{\lambda_m}=(2n+1)\frac{v}{4L}$

## Batidos o pulsaciones:

Superposición de ondas de frecuencias parecidas que viajan en el mismo sentido.

Para dos ondas armónicas de igual amplitud, pero de frecuencias distintas que se propagan en el mismo medio:

$\displaystyle \xi_1(x,t)=Acos(k_1x-w_1t)=\boxed{Acos(k_1x-2\pi f_1t)}=Acos(w_1(\frac{x}{v}-t))$

$\displaystyle \xi_2(x,t)=Acos(k_2x-w_2t)=\boxed{Acos(k_2x-2\pi f_2t)}=Acos(w_2(\frac{x}{v}-t))$

$\xi_{total}=\xi_1+\xi_2$

Si ubicamos el detector en $x=0$.

                                                   $\displaystyle \boxed{\xi_{total}=2Acos(\frac{w_1-w_2}{2}t)cos(\frac{w_1+w_2}{2}t)}$

                                              $\displaystyle \boxed{\xi_{total}=2Acos(\frac{f_1-f_2}{2}t)cos(kx-2\pi\frac{f_1+f_2}{2}t)}$

Si ubicamos el detector en x genérico:

$\displaystyle \xi_{total}=2Acos(\frac{w_1-w_2}{2}(\frac{x}{v}-t))cos(\frac{w_1+w_2}{2}(\frac{x}{v}-t))$

- $\displaystyle w_{onda\space modularizadora}=\frac{w_2-w_1}{2}$
- $\displaystyle f_{onda\space modularizadora}=\frac{f_2-f_1}{2}$
- $\displaystyle T_{onda\space modularizadora}=\frac{2}{f_2-f_1}$
- $\displaystyle T_{pulso}=\frac{1}{f_2-f_1}$
- $\displaystyle\boxed{ f_{pulso\space(batido)}=|f_2-f_1|}$