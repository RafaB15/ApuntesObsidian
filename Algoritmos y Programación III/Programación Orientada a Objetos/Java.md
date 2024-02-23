# Características

- Orientado a objetos 
- Simple 
- Seguro 
- Independiente de la plataforma 
- Robusto 
- Portable 
- Arquitectónicamente neutro
- Dinámico 
- Interpretado 
- Alto desempeño 
- Multihilo 
- Distribuido

# Interfaces

- Un objeto puede ser subclase de un único objeto, pero puede implementar diferentes interfaces.
- Las interfaces son como un contrato a través del cual te comprometés a implementar las funciones incluidas en este.
- Se parecen a los traits de Rust.
- Al definir un atributo de un objeto podemos poner una interfaz en vez de un tipo, para así decir que ahí habrá algún objeto que implemente la interfaz. Por ejemplo, si declaramos Map, que esuna interfaz, podemos ponerle un HashMap, que es un objeto que implementa Map.
# Funcionamiento

- Tiene una clase Main (opcional) que como punto de entrada tiene una función main (tiene que estar en alguna clase).
- **New** instancia un nuevo objeto a partir de una clase.
- Una clase tiene un constructor que tiene como nombre el nombre de la misma clase.
- Los nombres de las clases se ponen en Upper Camel Case.
- Los métodos en Lower Camel Case.
- Es mejor usar tipo.equals(tipo) para comparar porque == compara direcciones de memoria.

# Packages

- En java los packages son como los módulos en Rust. Hacés una carpeta con el nombre del package y dentro ponés `package nombre` primero. 
- Luego si se quiere acceder a algo en otro packages se importa.

# Tipos de datos

- List
- ArrayList
- LinkedList
- Map
- HashMap