- Una [[Base de Datos/Modelo Lógico Relacional/Modelo Relacional#Relación|relación]] está en forma normal Boyce-Codd (FNBC) cuando no existen [[Base de Datos/Diseño Relacional/Dependencia Funcional#Transitiva|dependencias transitivas]] $CK \to Y$, con *CK* clave candidata.
	- Es decir, eliminamos la posibilidad de tener dependencias transitivas $X \to Y$ en las que *Y* es un atributo primo.
- Dicho de otra forma, una relación está en FNBC cuando para toda dependencia funcional no trivial $X \to Y$, *X* es superclave.
- El problema que resuelve FNBC se da cuando en una relación existen varias claves candidatas que se solapan.
- Si tenemos 3 atributos *A, B,* y *C*, siendo A, B y A, C claves candidatas, entonces si existe la dependencia funcional $B \to C$, es una transitiva, pues $A, B \to B \to C$, con lo que no cumple con FNBC. 
- Para normalizar a FNBC, se tiene que extraer el atributo que puede ser deducido a partir de otra llave candidata a otra tabla con la *CK* como llave primaria.

# Algoritmo de descomposición a FNBC

Algoritmo para descomponer una relación de forma que cumpla con FNBC.

**Input**: Una relación universal *R* y un conjunto de [[Base de Datos/Diseño Relacional/Dependencia Funcional|dependencias funcionales]] *F*.
**Output**: Una [[Base de Datos/Diseño Relacional/Descomposición|descomposición]] de *R*, $D = (R_1, R_2, \dots, R_n)$ que preserva la información, y está en FNBC.
![[Base de Datos/Diseño Relacional/images/Algoritmo FNBC.png]]

- No preserva las dependencias funcionales, pero preserva la información.