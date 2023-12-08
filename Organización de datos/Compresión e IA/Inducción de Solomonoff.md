## Sistematizar el conocimiento

### Inducción

Si todos los objetos observados de tipo X tienen la propiedad Y entonces todos los objetos de tipo X tienen la propiedad Y.

Si siempre sucede X en el contexto Y, X siempre sucederá en el contexto Y.

La inducción en la teoría puede parecer una manera muy simple y poco efectiva de ver datos, si veo tres cisnes blancos no significa que todos sean blancos. Sin embargo, en la práctica, y sobre todo en machine learning, es una herramienta poderosísima.

**Epicúreo →** “if more than one theory is consistent with the data, keep them all”

**Navaja de Ockam →** “keep the simples theory consistent with the observations”

Teorema de Bayes:

$$
P(H|E) = \frac{P(E|H)P(H)}{P(E)}
$$

P(H|E): Probabilidad de que la hipótesis sea cierta dad la evidencia E.

P(E|H): Probabilidad de que suceda la evidencia E dado la hipótesis H,

P(H): Probabilidad de que la hipótesis sea cierta.

P(E): Probabilidad de que la evidencia ocurra.

## Inducción de Solomonoff - 1960

1. Recolectamos los datos y los ponemos en formato: entrada → salida.
2. Iteramos todos los programas
    1. Si terminan, miramos si su salida dado la entrada es lo que queríamos para el dato actual.
3. Actualizamos la probabilidad de que cada prograa sea el que explica el fenómeno.
4. Repetimos.

Redefinimos:

P(H|E): Probabilidad de que el programa H explique los datos E.

P(E|H): Probabilidad de ver la evidencia E dado que corremos el programa H.

P(H): Probabilidad del programa H

P(E): Probabilidad de que exista la evidencia E.