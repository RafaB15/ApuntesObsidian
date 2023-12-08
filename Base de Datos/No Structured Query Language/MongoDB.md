- [[Sistemas de gestión de bases de datos]] [[No SQL|no SQL]] de tipo [[Bases de datos orientadas a documentos|orientada a documentos]].
- Basada en hashes para identificar a los objetos. 
- No utiliza esquemas (schema-free). No tienen que tener las mismas columnas todos los objetos.
- No existe un [[Lenguajes para BDD#Lenguajes de definición de datos|DDL]]. 
- Los documentos tienen un formato [[JSON]]. Almacena por clave/valor. 
- Su implementación de la operación de junta es limitada.
- Organiza los datos de una base de datos en colecciones que contienen documentos.

| Modelo Relacional | Mongo DB |
| --- | --- |
| Esquema | Base de datos |
| Relación | Colección |
| Tupla | Documento |
| Atributo | Campo| 

- Su atributos pueden ser multivaluados.
- Los documentos dentro de una colección se identifican a través de un *campo_id*.
- Si no se especifica nada, MongoDB asignará como *_id* un hash de 12 bytes. La función `ObjectId(h)` convierte un hash en una referencia al documento que dicho hash identifica.
- El *hash* también asegura que no se pueda insertar dos veces el mismo documento en una colección.

# Comandos

## Creación de documentos

```python
from pymongo import MongoClient
conn = MongoClient() 

conn.database_names() 

# Creamos una nueva base de datos 
bd_empresa = conn.base_empresa 

#Le agregamos una colección 
col_clientes = bd_empresa.clientes 

# Y le agregamos un documento a la colección
cliente1 = { 
	"nombre": "Mario", 
	"apellido": "Wilkerson", 
	"domicilio": "Av. Entre Ríos 1560" } 

id_cliente1 = col_clientes.insert_one(cliente1 ).inserted_id

# Como no hay un esquema definido, no es necesario que los documentos tengan los mismos campos

# Insertamos tres clientes más 

cliente2 = { 
		"nombre": "Horacio", 
		"apellido": "Fonseca", 
		"localidad": "Morón" } 
id_cliente2 = col_clientes.insert_one(cliente2 ).inserted_id 

cliente3 = { 
		"apellido": "Gandría", 
		"localidad": "Caballito" }
id_cliente3 = col_clientes.insert_one(cliente3 ).inserted_id 

cliente4 = { 
		"apellido": "Findo", 
		"nombre": "Diego", 
		"localidad": "Morón" } 
id_cliente4 = col_clientes.insert_one(cliente4).inserted_id
```

- Si insertamos objetos con campos iguales, se diferencian por su hash id. Si especificamos un hash igual a uno que ya existe nos dará error.
## Consultas básicas

### find

```python
#Buscamos todos los clientes que son de Morón 
respuesta_query = col_clientes.find({"localidad": "Morón"}) 

for c in respuesta_query:
	pprint.pprint(c)
```

- Todo find se escribe como documento json.
- En python find te devuelve un cursor que hay que ir iterando. Es lazy, por lo que solo va a buscar el valor cuando se lo pidamos.
- Si hacemos solamente `col_clientes.find()` nos dará todos los documentos.
- Para poner condiciones de relación usamos 
```python

# Mayor a algo
col_clientes.find({"cuota" : {$gt: 2}})

# Que un atributo no exista
col_clientes.find({"cuota" : {$exists: false}})
```

## Documentos Embebidos vs Referenciados

- **Documentos Embebidos:** Se pone un documento en el campo de otro documento.
- **Documento Referenciado:** Se pone el object id de un objeto en el campo de otro objeto. No es como una llave foránea porque no se chequea que siga existiendo el objeto si se borra.

```python
pedido1 = { 
	   "cod_pedido" : 78303 , 
	   "cliente" : id_cliente2 , # Referenciado 
	   "productos" : [ {
		   "producto": id_producto2, 
		   "cantidad": 3}], # Embebido
	   "fecha_entrega_limite": datetime.datetime (2017 , 6, 18),
	   "entregado" : False }
```

- Para hacer consultas con estos valores usamos
 ```python
result = col_pedidos.find({"productos.producto": id_producto3 }) 

for cliente_id in result.distinct("cliente"): 
	result2 = col_clientes.find({"_id": cliente_id})
	for cliente in result2: 
		pprint.pprint(cliente)
```

- Es convenientes tener las cosas embebidas más que referenciadas por un tema de performance. Lo que sufre es la integridad. pues hay redundancia de datos.
- MongoDB no está pensado para realizar operaciones de junta en forma eficiente.
- Las juntas se suelen hacer a mano, como en el documento anterior.
- Si necesitamos acceder muchas veces al resultado de una junta, hay que evaluar si no sería conveniente tenerla directamente en la tabla.
- Sacrificamos la no redundancia de datos y la normalización, ya que se rompe con el paradigma relacional.
- La idea es resignar un poco de normalización para ganar velocidad en el procesamiento de los datos.
- Hay un comando lookup que permite hacer juntas, pero es recomendado utilizarla con cautela por su baja eficiencia.

## Pipeline

- MongoDB implementa la agregación a través de un pipeline secuencial que combina etapas de agrupamiento, selección, etc.
- La función *aggregate()* opera a partir de un vector de documentos JSON en donde cada documento describe una operación
```python
#Calculamos la cantidad de clientes que viven en cada localidad y mostramos sólo aquellas en que vive a lo sumo un cliente: 
result = col_clientes.aggregate( [ 
	  { "$group": {
		  "_id": "$localidad", 
		  "cantidad": {"$sum": 1 }}}, #los que tengan al menos 1 
	  { "$match": {
		  "cantidad": { "$lte": 1 }}} #lte less than or equal
	  ]) 
for cliente in result: 
	pprint.pprint(cliente)
```

- Si queremos que no nos muestre los nulls, agregamos al match `_id: {ne: null}`
- En las funciones de agregación podemos usar:
	- **match**: Filtrado de resultados. 
	- **group**: Agrupamiento de los resultados por uno o más atributos, aplicando funciones de agregación. 
	- **sort**: Ordenamiento de resultados. 
	- **limit**: Limitado de resultados. 
	- **sample**: Selección aleatoria de resultados. 
	- **unwind**: Deconstrucción de un atributo de tipo vector. Hace un documento por cada elemento del vector
- El conjunto de resultados que devuelve una operación será utilizado como entrada por la siguiente operación del pipeline. 
- Un mismo tipo de operación podría ser utilizado más de una vez dentro del pipeline.

## Sharding

- Es el modelo distribuido de procesamiento usado por Mongo.
- Se establece el criterio por el cual se va a dividir la base de datos (un nodo que va a tener a ciertos documentos)