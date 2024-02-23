- Es una técnica para escribir código que recae mucho en las [[Pruebas]].
- *Tdd denomina pruebas a las [[Pruebas de Verificación|pruebas unitarias]]
- Incluye 3 subprácticas:
	- **Automatización:** las pruebas del programa deben ser hechas en código (general- mente siguiendo las reglas .arrange, act, assert.o "given, when, then"), y con la sola ejecución del código de pruebas debemos saber si lo que estamos probando funciona bien o mal.
	- **Test-First:** las pruebas se escriben antes del propio código a probar.
	- **Refactorización posterior:** para mantener la calidad del código, se lo cambia sin cambiar la funcionalidad, manteniendo las pruebas como reaseguro.
- Ventajas:
	- Las pruebas en código sirven como documentación del uso esperado de lo que se está probando, sin ambigüedades. 
	- Las pruebas escritas con anterioridad ayudan a entender mejor lo que se está por desarrollar. 
	- Las pruebas escritas con anterioridad suelen incluir más casos de pruebas negativas que las que escribimos a posteriori. 
	- Escribir las pruebas antes del código a probar minimiza el condicionamiento del autor por lo ya construido. 
	- También da más confianza al programador sobre el hecho de que el código que escribe siempre funciona. 
	- Escribir las pruebas antes del código a probar permite especificar el comportamiento sin restringirse a una única implementación. 
	- La automatización permite independizarse del factor humano y facilita la repetición de las mismas pruebas a un costo menor. 
	- La refactorización constante facilita el mantenimiento de un buen diseño a pesar de los cambios que, en caso de no hacerla, lo degradarían.

![[Pasted image 20240131163252.png]]

![[Pasted image 20240131163316.png]]