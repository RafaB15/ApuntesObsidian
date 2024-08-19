- Tenemos que poner toda la lógica de comunicación con el servicio externo en un objeto aparte. Ports and apadters.
- Parar testear la aplicación nuestra podemos usar un mock, pero tendremos que acompañarlo con pruebas sobre el objeto que interactúa con el servicio. Si el servicio cambia no cambiarán las pruebas con el mock pero sí las pruebas con el servicio pueden cambiar.
- **end to end:** De punta a punta y tiene dependencia del servicio externo.
- **end to edge**: De punta a punta pero cambiamos el servicio externo por un mock **externo**. Se testea el código del conector verdadero que interactúa con el negocio. La aplicación piensa que está interactuando con el servicio real, pero atrapamos esa request nosotros.
- **edge to edge**: no tiene dependencia de arquitectura. Se evita la interacción con el servicio externo usando un mock de bajo nivel en la librería de conexión y voy a saltearme la capa de input interactuando directamente con el objeto de negocio.
![[Pasted image 20240519161804.png]]
![[Pasted image 20240519161928.png]]