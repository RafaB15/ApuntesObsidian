- Es un protocolo de la [[Application Layer|capa de aplicación]] para la web.
- Está implementado en dos programas, un **cliente** y un **servidor**.
- Estos se comunican intercambiando mensajes HTTP.
- HTTP define la estructura de los mensajes que se mandan y como el cliente y servidor los intercambian.

# Página web

- También llamada documento.
- Consiste en **objetos**, que son simplemente archivos
	- Archivo HTML
	- Imagen JPEG
	- Java applet
	- Video clip
- Los objetos son identificables por un único **URL**. Estos tienen dos componentes
	- El hostname del servidor que guarda el objeto.
	- El pathname del objeto.
	- Ej: http://www.someschool.edu/someDepartment/picture.gif
		- Hostname: www.someschool.edu
		- Pathname: /someDepartment/picture.gif
- Los web browsers implementan el lado del cliente de http. Los servidores web implementan el lado del servidor, como Apache y Microsoft Internet Information Server.
- HTTP especifica como los clientes web le piden páginas a los servidores y como estos las transfieren a los clientes.

![[HTTP.png]]

- El protocolo HTTP hace uso de [[Transmission Control Protocol|TCP]] por debajo como protocolo de transporte.
- HTTP es un **stateless protocol** porque no tiene memoria de qué le pediste antes.
- La web usa la [[Arquitectura Cliente-Servidor|arquitectura cliente-servidor]].
- Por default HTTP usa una [[Transmission Control Protocol#Conexión persistente|conexión persistente]].
- El número de puerto default es 80.

![[Handshake.png]]

# Mensaje

- El protocolo HTTP especifica dos tipos de mensajes: Requests y responses

## Requests

```
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu 
Connection: close 
User-agent: Mozilla/5.0 
Accept-language: fr

```

- Los mensajes se escriben en simple **ASCII**.
- La primera línea es la request line, luego siguen las header lines.
- La request line tiene 3 campos: El campo del método (GET, POST, HEAD, PUT, DELEATE), el campo del URL, y la versión de HTTP.

![[HTTP request.png]]

## Response

```
HTTP/1.1 200 OK 
Connection: close 
Date: Tue, 18 Aug 2015 15:44:04 GMT 
Server: Apache/2.2.3 (CentOS) 
Last-Modified: Tue, 18 Aug 2015 15:11:03 GMT 
Content-Length: 6821 
Content-Type: text/html 

(data data data data data ...)
```

- Tenemos una línea de status, seis header lines, y el entity body, que es la respuesta a nuestra request.

![[HTTP response.png]]


# Cookies

- Le permiten a los sitios web retener información acerca de usuarios.
- Tiene 4 componentes:
	- Un header line cookie en la response html.
	- Un header line cookie en la request html.
	- Un archivo de cookies mantenido en el end system del usuario y manejado por su navegador.
	- Una base de datos back-end en el sitio web.

![[Cookies.png]]

# Web caching

- Nuestros browsers a veces guardan las respuestas a requests que hacemos, por lo que cuando hacemos una nueva request primero pasa por un **proxy server** que se fija si la tenemos en el cache para devolverla mucho más rápido, y sino, la manda al servidor real. Al recibir la respuesta la guarda por si se la piden en el futuro.
- El cache es uns ervidor y cliente al mismo tiempo.

![[Web cache.png]]