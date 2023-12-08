Es un conjunto de programas que gestiona y controla la creación, manipulación y acceso a la [[Base de Datos/Introducción/Base de Datos|base de datos]].

Este provee un nivel de abstracción entre los programas o sistemas de información y los datos, resolviendo el problema conocido como *dependencia de datos*.

### Independencia de datos

Es la propiedad del SGBD consistente en que cambios en la estructura de la base de datos no repercutan en los programas o sistemas de información que la utilizan.

![[Base de Datos/Introducción/images/Untitled 1.png|Untitled]]

# Funciones

## Almacenamiento y Consulta

- Ofrecer estructuras eficientes.
- Ofrecer un lenguaje de consulta (aumenta la productividad).

# Integridad

- Asegurar la integridad de datos a través de restricciones.

# Seguridad

- Evitar accesos no autorizados.
- Pueden haber diferentes roles
    - ***Admin →*** Puede hacer todo
    - ***Solo lector →*** No puede editar los datos

# Concurrencia

- Permitir el acceso en simultáneo de muchos usuarios.

# Recuperación

- Ofrecer herramientas para la recuperación ante fallas.

# Soporte transaccional

- Capacidad de administrar operaciones como agregar, actualizar y eliminar datos en unidades separadas llamadas transacciones.
- Garantiza que las operaciones se lleven a cabo correctamente o se deshagan por completo en caso de que surja un problema.