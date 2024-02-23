- Es una de las formas fundamentales en que nosotros, como humanos, enfrentamos la complejidad. 
- Surge del reconocimiento de similitudes entre ciertos objetos del mundo real, y la decisión de concentrarse en estas similitudes e ignorar por el momento las diferencias. 
- Una buena abstracción enfatiza los detalles que son significativos para el usuario y suprime los detalles que son, al menos por el momento, irrelevantes.
![[Abstracción.png]]

# Principios

Una abstracción se enfoca en la vista exterior de un objeto y sirve para separar su comportamiento esencial de su implementación

## Principio del mínimo compromiso

- La interfaz de un [[Objeto|objeto]] proporciona su comportamiento esencial, y nada más.
- No hay que hacer públicas las funciones que no deberían ser públicas y solo se usan internamente.

## Principio del menor asombro

- Una abstracción captura todo el comportamiento de algún objeto, ni más ni menos, y no ofrece sorpresas ni efectos secundarios que vayan más allá del alcance de la abstracción.