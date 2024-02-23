- Capacidad de contener valores de distintos tipos (en el caso de las variables polimórficas) o a la capacidad de recibir argumentos de diferentes tipos (en el caso de los métodos polimórficos).
- **Polimorfismo ad-hoc:** Funciona con un número limitado y conocido de tipos, no necesariamente relacionados entre sí.
- **Polimorfismo universal:** Funciona con un número prácticamente infinito de tipos relacionados entre sí.
![[Pasted image 20240129192046.png]]
# Polimorfismo por sobrecarga

- Dentro de una misma clase, es posible escribir dos o más métodos con el mismo nombre pero diferente firma (signature). 
- El resultado es un polimorfismo aparente, ya que no se trata de un método que puede recibir muchos tipos de argumentos, sino que hay varios métodos con el mismo nombre, y durante el proceso de compilación se elije cuál usar según el o los argumento(s) pasado(s).

![[Polimorfismo por sobrecarga.png]]

# Polimorfismo por coerción

- Aplicar coerción sobre alguien significa forzar su voluntad o su conducta.
- En programación, significa forzar a que un dato de un tipo sea tratado como si fuera de otro tipo. 
- Por ejemplo, coerción es la operación realizada para convertir (de manera implícita) un argumento al tipo del parámetro correspondiente. 
- En este caso, también se trata de un polimorfismo aparente, ya que la conversión que ocurre no cambia el hecho de que el método, en realidad, trabaja con un único tipo.

![[Polimorfismo coerción.png]]

# Polimorfismo paramétrico

- Cuando se escribe código genérico, es decir, sin mencionar ningún tipo de datos específico, para que pueda ser usado con datos que serán tratados de manera idéntica independientemente de su tipo, se está aprovechando el polimorfismo paramétrico. 
- En Java, a esta variante de polimorfismo se la conoce como ``Generics``. 
![[Polimorfismo paramétrico.png]]

# Polimorfismo por inclusión

- El polimorfismo por inclusión, también conocido como polimorfismo por herencia o polimorfismo de subclases (o de subtipos), es la variante más común encontrada en la [[Programación Orientada a Objetos|POO]] y, por ello, la mayoría de las veces se lo denomina polimorfismo a secas. 
- Se basa en el hecho de que las superclases incluyen a todas las instancias de sus subclases o, dicho de otra forma, todos los objetos de una subclase son también objetos de las superclases de esta. 
- Por ello, aunque se declare un atributo, una variable local, un parámetro o el contenido de una colección como siendo de una superclase, en realidad puede referirse a cualquier instancia de esa clase o de alguna sus subclases.
- Los objetos no pierden sus características (estado y comportamiento) al ser referenciados de esta manera, por lo que es posible invocar los métodos que estos hayan sobrescrito, y su comportamiento será el esperado.