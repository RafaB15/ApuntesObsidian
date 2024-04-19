- Los segmentos de la [[Transport Layer|capa de transporte]] son mensajes que la [[Application Layer|capa de aplicación]] le mandan a la capa de transporte, que luego esta fragmenta en pedazos más pequeños, a los cuales les agrega un header de la capa de transporte antes de enviarlos a la [[Network Layer|capa de red]].
- Tienen campos especiales en el heder que ayudan a identificar los [[Socket|sockets]] a los que van dirigidos, específicamente hay información acerca de sus [[Puerto|puertos]].

![[Segmento.png]]