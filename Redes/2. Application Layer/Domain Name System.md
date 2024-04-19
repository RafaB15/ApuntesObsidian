- El DNS es tanto una base de datos distribuida implementada en una jerarquía de servidores DNS, como un protocolo de la [[Application Layer|capa de aplicación]] que le permite a los [[End System|hosts]] hacer queries a la base de datos distribuida.
- El protocolo DNS corre en [[User Datagram Protocol|USP]] y usa el puerto 53. Si el mensaje no llega a su destino entonces lo reenvía o prueba otro servidor.
- Este servicio se encarga de traducir el [[Hostname|hostname]] de una página que las personas podemos fácilmente leer, a una dirección IP que nos diga como llegar a un [[End System|end system]] en la [[Red|red]].
- Se suele utilizar DNS en otros protocolos de la [[Application Layer|capa de aplicación]] como [[HyperText Transfer Protocol|HTTP]] y [[Simple Mail Transfer Protocol|SMTP]] para traducir los hostnames brindados por usuarios.
- Aparte de la traducción de hostnames, otros servicios proveídos por el protocolo DNS son:
	- **Host aliasing:** Un host con un [[Hostname|hostname]] complicado puede tener alias por los cuales referirse a este.
	- **Mail server aliasing**: Se pueden tener aliases para los servidores de mail (lo que va después del @).
	- **Load distribution:** Para páginas muy visitadas se puede tener diferentes servidores con la misma información y ser dirigido a uno de ellos.

# Base de datos distribuida y jerárquica

- El DNS usa un gran número de servidores para lidiar con el problema de la escalabilidad, organizados en una jerarquía y distribuidos alrededor del mundo.
- Los mapeos de hostname a dirección IP están distribuidos a través de los servidores DNS.

![[Jerarquía DNS.png]]

- El cliente primero contacta a uno de los **root DNS servers** que le da una dirección IP de un **TLD (top level domain) server**, los cuales se encargan de las diferentes extensiones (.com, .org, .edu).
- El cliente contacta a este TDL server y este le devuelve la dirección IP de un **authoritative server** para la dirección completa. Estos servidores deben ser proveídos por las organizaciones que tengan [[End System|host]] que se puedan acceder públicamente.
- Finalmente el cliente contacta a este servidor autoritativo, el cual le devuelve la dirección IP del hostname.

![[DNS root servers por país.png]]

- También existen servidores DNS locales, los cuales sirven como un proxy para redirigir las queries a la jerarquía de servidores DNS, obteniendo direcciones de cada nivel y haciendo nuevos requests. 

![[Local dns server.png]]

# DNS caching

- En toda cadena de queries, cuando un servidor DNS recibe una respuesta DNS, puede cachear la respuesta (el mapeo) en su memoria local.

![[Cache DNS.png]]

# Resource Records

- Los servidores DNS que juntos implementan la base distribuida DNS guardan lo que se conoce como **resource records (RRs)** (*registro de recurso*), incluyendo RRs que proveen mapeo de direcciones de hostname a IP.
- Un resource record es una tupla de cuatro valores que contiene los siguientes campos 

```
[Name, Value, Type, TTL]
```

- **TTL** es *time to live* del recurso y especifica en qué momento este recurso debería se removido de un cache.
- El significado de *Name* y *Value* depende del *Type*.
	- Si `Type = A`, entonces *Name* es un [[Hostname|hostname]] y *Value* es un **dirección IP para el hostname**.
	- Si `Type = NS`, entonces *Name* es un **dominio** (como .com) y *Value* es el [[Hostname|hostname]] del **authoritative DNS server** que sabe como obtener las direcciones IP de los [[End System|hosts]] con ese dominio.
	- Si `Type = CNAME`, entonces *Value* es un hostname **canónico** para el hostname **alias** *Name*.
	- Si `Type = MX`, entonces *Value* es el nombre **canónico** de un servidor de mail que tiene un hostname **alias** *Name*.

# Mensajes DNS

- Hay dos tipos de mensajes, los de respuesta y los de query, sin embargo estos comparten formato.

![[DSN message.png]]

# Agregar registros a un servidor DNS

- Se le paga a un **registar**, que es una entidad comercial que verifica la unicidad de nombre de dominio y lo ingresa a la base de datos DNS.
- Al registrar una dirección con un registar, tenés que proveer los nombres y direcciones IP de tus servidores DNS authoritative primarios y secundarios.