- Ruby no se compila. Es un lenguaje interpretado.
- Sirve para scripting como python, pero es orientado a objetos de la misma forma que smalltalk o java.

# Convenciones

- Convención sobre configuración.
- Clases en Camel Case
- Métodos en snake case.
- Archiovos .xxxx para configurar herramientas.
- Todo código viene con tests.

# Características

- Tipado dinámico.
- Multi paradigma y de propósito general.
- Smalltalk-like (todo es un objeto)
- 100% Command-line friendly
- No tiene backwards compatibility.

# Herramientas

- RVM
	- Ruby Verion Manager
	- Nos ayuda a administrar las diferentes versiones de ruby que tenemos instaladas.
	- Como Ruby no es retrocompatible entre versiones siempre, RVM nos ayuda a tener diferentes versiones y trabajar con ellas.
- IRB
	- Consola interactiva.
- RubyGems
	- Gem permite instalar librerías. Las librerías se llaman gemas.
	- Algunas librerías tienen código C. En ese caso ya no se pueden interpretar, sino que tenés que tener compialda la parte de C.
	- Ponemos las diferentes gemas en un archivo Gemfile.
- Bundler
	- Bundler nos permite especificar las librerías que queremos utilizar y este las descarga. 
	- Enfocado en la resolución de dependencias. Como maven.
	- Teniendo un Gemfile, al hacer bundler install me las instala.
- Rake
	- Es para compilar y correr pruebas.
	- También ver errores del linter.
	- Ponemos en el rakefile lo que necesitamos ejecutar y si hacemos bundle exec rake corre rake en el contexto de bundler, se asegura de que las dependencias estén bien y corre todos los comandos. Se parece a makefile.

-  RubyTest, Minitest, Rspec
	- Framework de test automatizado
	- Ruby test ya viene en la biblioteca estándar. 

# Runtime

- El más conocido se llama mri y está escrito en C.
- Si hay algún código en C, tendremos que tener instalado también algún compilador de C o librerías específicas.

# Estructura

- Depende del framework.
- Carpeta model ponemos las clases.
- Si usamos rspec library par alas pruebas, ponemos las pruebas en una carpeta spec.

# Sintaxis básica

- En vez de print pondríamos  `puts`. Puts siempre devuelve `nil`
```Ruby
puts "hello world
```
- Declarar una función. 
```Ruby
def funcion
	puts "Hello World!"
end

def funcion2(name)
	puts "Hello #{name}!"
end
```
- Al llamar a una función, si esta no tiene parámetros, entonces podemos poner únicamente el nombre. Si tiene un parámetro se lo podemos pasar después del nombre sin paréntesis.
- Para crear una clase hacemos
```Ruby
class Greeter
	def initialize(name = "World")
		@name = name # Variables de instancia/ atributos
	end
	def say_hi
		puts "Hi #{@name}!"
	end
	def say_bye
		puts "Bye #{@name}, come back soon."
	end
end
```
- Para crear una instancia de la clase usamos
```Ruby
greeter = Greeter.new("Pat")
```
- Si queremos que una variable de instancia se pueda consultar y modificar ponemos:
```Ruby
class Greeter
	attr_accessor :name

	def initialize(name = "World")
		@name = name # Variables de instancia/ atributos
	end
end
```
- Usamos if
```Ruby
if @names.nil?
```
- En vez de for podemos usar
```
numeros = [1,2,3]

numeros.each { |numero| puts numero} 
```
o 
```
numeros = [1,2,3]

numeros.each do |numero| {
	puts numero
}
end
```
- Template
```Ruby
Template
```
# Pruebas

- 