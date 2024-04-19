# Modelo conceptual, de objetos y relacional

Todo esto en Domain Driven Design.
- Modelo Conceptual
	- Surge del dominio en el que estoy trabajando
	- Surge del lenguaje universal
	- Se traduce a un modelo de objetos
![[Pasted image 20240415002902.png]]
- Modelo de Objeto
	- Surge de un modelo conceptual
![[Pasted image 20240415003104.png]]
- Modelo Relacional
	- Para dar persistencia al modelo de objetos utilizamos una base de datos relacional.
![[Pasted image 20240415003156.png]]

- Objetos Repositorios y Tablas

![[Pasted image 20240415003324.png]]

# Persistencia de objetos en BDD relacionales

- Modelado de objetos con Almacenamiento relacional
	- Cuando hay problemas con guardar objetos en tablas se llama **Impedance mismatch**.
	- Se podría llevar a los atributos de la bdd los atributos de los objetos como un registro en la tabla, pero eso no funciona para la herencia de manera nativa.
	- Si tenemos objetos que tienen atributos que apuntan a otros objetos y viceversa, con una relación muchos a muchos, si queremos tener una tabla para cada tipo de objeto, luego necesitaremos una tercera para modelar la relación entre estos.
- Patrones:
	- **Active record**: Cada clase tiene métodos para manejar la persistencia. Ruby on rails	![[Pasted image 20240415004803.png]]
	- **Repository**: Por cada clase (entidad fuerte) existe una clase Repository que maneja la persistencia. Spring Framework
![[Pasted image 20240415004950.png]]

# Implementación de repositorios para persistencia relacional

## Consideraciones

- Intrusivas vs Transparentes
	- Intrusivas en cuando los frameworks utilizan alguno de los patrones ya antes discutidos y tienen que crear clases solo para que funcionen.
	- Transparente: Usar un framework pero que eso no impacte en nuestro modelo. No heredarán ninguna clase de persistencia.
- Incumbencias: SQL statements & Mapping
	- Mapping es saber qué tabla se convierte en qué clase y qué atributos se mapean a qué.
- Migrations
- Validaciones
	- A veces se delegan las validaciones en la base de datos.
	- Eso funciona pero no es del todo correcto. Debería estar en la aplicación pues es parte del modelo de negocio. Los tenemos que poner en ambos.
- Optimizaciones: lazy loading, caching, etc.