# Ejercicio 1

- Artículos(nro art, nombre art, color) 
- Proveedores(nro prov, apellido) 
- Pedidos(nro prov, nro art, cantidad)

a) Obtener los números de aquellos proveedores que suministran el producto 34.
$$\displaystyle \huge \pi_{nro\_prov}(\sigma_{nro\_art = 34} Pedidos)$$
b) Obtener el número y el apellido de aquellos proveedores que suministran el producto 34 o el producto 12.
$$\displaystyle \huge numero\_prov = \pi_{nro\_prov}(\sigma_{nro\_art = 34 \ \vee \ nro\_art = 12} Pedidos)$$
Alt1
$$\displaystyle \huge  proveedores \bowtie_{proveedores.nro\_prov = numero\_prov.nro\_prov} numero\_prov $$
Alt2
$$\displaystyle \huge  proveedores * numero\_prov $$
Alt3 
$$\displaystyle \huge  proveedores \div numero\_prov $$

c) Obtener los números de los productos que son tuercas o que son suministrados por el proveedor números 328.
$$\displaystyle \large tuercas = \pi_{nro\_art}(\sigma_{nombre\_art = tuercas}(articulos))$$
$$\displaystyle \large proveidos = \pi_{nro\_art}(\sigma_{nombre\_prov = 328}(pedidos))$$
$$\displaystyle \large tuercas \cup proveidos$$
*La unión no deja repetidos*

d) Obtener los números de los productos que son tuercas y que son suministrados por el proveedor número 328.
$$\displaystyle \large proveidos = \pi_{nro\_art}(\sigma_{nombre\_prov = 328}(pedidos))$$
$$\displaystyle \large \pi_{nro\_art}(proveidos \bowtie_{proveidos.nro\_art=articulos.nro\_art \wedge articulos.nombre\_art = tuerca}articulos)$$
e) Obtener los apellidos de aquellos proveedores que suministran al menos un producto que no sea el producto 33.
$$\displaystyle \large \sigma_{apellido}(pedidos \bowtie_{pedidos.nro\_prov=proveedores.nro\_prov\wedge pedidos.nro\_art != 33}proveedores)$$
f ) Obtener los apellidos de aquellos proveedores que no suministran el producto 33
$$\displaystyle \huge pedido\_33 = \pi_{nro\_prov}(\sigma_{nro\_art = 33}(pedidos))$$
$$\displaystyle \large \pi_{nro\_prov}(proveedores) - pedido\_33$$
g) Obtener los apellidos de aquellos proveedores que suministran al menos un producto y que no suministran el producto 33.
same con e pero con un twist

h) Obtener el número y el apellido de aquellos proveedores que suministran más de 100 tuercas en algún pedido.
$$\displaystyle \large tuercas = \pi_{nro\_art}(\sigma_{nombre\_art = tuerca}(articulos))$$
$$\displaystyle \large p\_tuercas =pedidos * tuercas$$
$$\displaystyle \large \pi_{nro\_prov, apellido}(proveedores \bowtie_{p\_tuercas.cantidad>100 \wedge p_tuercas.nro\_prov = proveedores.nro\_prov} p\_tuercas)$$

i) Obtener los números de aquellos proveedores que suministran todos los productos.
$$\displaystyle \huge \pi_{nro\_prov, nro\_art}pedidos\div\pi_{nro\_art}articulos$$
j) Obtener los apellidos de aquellos proveedores que suministran todos los productos menos el 12.
$$\displaystyle \large $$