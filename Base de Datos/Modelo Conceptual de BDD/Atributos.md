- Dependen de la [[Base de Datos/Modelo Conceptual de BDD/Entidades|entidad]]
    - País(nombre, población, superficie)
- El **dominio** de un atributo es el conjunto de valores que el mismo puede tomar
    - nombre → Cadena de caracteres
    - población → Número entero positivo
    - superficie → Número real positivo
- En ciertos casos un valor puede ser nulo por si no se sabe el valor o no se tiene. Hay que representarlo con algo.

## Atributos compuestos vs simples:

Un atributo compuesto es un atributo que tiene muchos tipos de información dentro suyo.

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 2.png|Untitled]]

## Atributos multivaluados vs monovaluados

Una entidad a veces puede tener muchos valores en un mismo atributo

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 1 1.png|Untitled]]

### Atributos almacenados vs derivados

El atributo derivado es un atributo que podemos obtener a partir de operaciones con los atributos que sí tenemos almacenados.

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 2 1.png|Untitled]]
# Atributo primo
Es aquel que es parte de alguna clave candidata de la [[Base de Datos/Modelo Lógico Relacional/Modelo Relacional#Relación|relación]].