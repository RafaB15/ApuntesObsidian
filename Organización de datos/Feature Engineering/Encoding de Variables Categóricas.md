# One Hot Encoding

El más popular, pero probablemente de los peores

![[Organización de datos/Feature Engineering/Encoding de Variables Categóricas/Untitled.png|Untitled]]

La ciudad es una variable categórica porque las variables pueden ser varias y no son números.

Creamos una columna por cada variable categórica

![[Organización de datos/Feature Engineering/Encoding de Variables Categóricas/Untitled 1.png|Untitled]]

Esto puede ser muy ineficiente si tenemos demasiadas categorías, por tener que agregar demasiadas columnas.

Si tengo una columna con solo dos opciones de qué puede estar ahí (ej :género) sirve bastante.

# Binary encoding

![[Organización de datos/Feature Engineering/Encoding de Variables Categóricas/Untitled 2.png|Untitled]]

Asignamos un valor binario a cada categoría y el número de nuevas columnas dependerá de la cantidad de categorías que quiera representar. Si tengo 7 categorías, agrego 3 columnas, porque en binario necesito tres bits para contar hasta 7.