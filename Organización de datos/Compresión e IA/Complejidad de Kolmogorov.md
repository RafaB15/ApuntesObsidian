Sea $x$ un string, $k(x)$ es igual a la cantidad de bits mínimos que debe tener un programa que genera $x$.

![[Organización de datos/Compresión e IA/Complejidad de Kolmogorov/Untitled.png|Untitled]]

Si queremos representar ese número, lo imprimimos multiplicado por la cantidad de veces que aparece. Si tuviéramos un millón de ceros la complejidad de Kolmogorov sería la misma porque lo representamos con”0”.

![[Organización de datos/Compresión e IA/Complejidad de Kolmogorov/Untitled 1.png|Untitled]]

En este caso, si tuviéramos un millón de números, la complejidad de Kolmogorov también sería un millón.

Sea $x$ un string, se dice que x es un archivo aleatorio si y sólo si $k(x) = |x|$. Es decir, la complejidad del string es igual a la longitud del mismo.

## Propiedades

- $K(X) \ge 0$
- $K(X) \le |X|$
- $K(X) \le K(X)+K(Y)$
- $K(XY)\ge K(X),K(XY)\ge K(Y)$
- $K(XY) = K(YX)$
- $K(XX)=K(X)$
- $K(XY)+K(Z) \le K(XZ) + K(YZ)$

## Distancia de Kolmogorov

$$
KD(x,y) = K(xy) - min\{K(x),K(y)\}
$$

$$
x = 543254 \\ y =4355432 \\ K(x) = 6 \\ K(y) = 7 \\ K(xy) = 13 \\ KD(x,y) = 13 - 6 = 7
$$

Distancia de Kolmogorov normalizada

$$
NKD(x,y) = (K(xy) - min\{K(x),K(y)\})/max\{K(x),K(y)\}
$$

## Distancia de Compresión

$$
NCD(x,y) = (C(xy) - min\{C(x),C(y)\})/max\{C(x),C(y)\}
$$

Entonces:

- La compresión está relacionada con la inteligencia del compresor y con la redundancia de las strings.
- La complejidad de Kolmogorov es el largo del programa más chico que genera una string.
- Un archivo aleatorio tiene una complejidad igual a su largo.
- La complejidad de Kolmogorov es intractable.
- La distancia de compresión nos ayuda a identificar elementos parecidos o relacionados entre sí.
- La mayoría de los archivos son aleatorios.