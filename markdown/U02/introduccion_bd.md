# Conceptos esenciales sobre sistemas de bases de datos
## Índice
- [Introducción](#Introducción)
- [Funciones principales de un SGBD](#Funciones-principales-de-un-SGBD)
- [Tipos de sistemas de bases de datos](#Tipos-de-sistemas-de-bases-de-datos)
- [Modelo relacional](#Modelo-relacional)
- [SQLite y MySQL/Maria DB](#SQLite-y-MySQL/Maria-DB)
- [El lenguaje SQL](#El-lenguaje-SQL)
- [Acceso desde Python](#Acceso-desde-Python)
- [Papel de las bases de datos en el análisis de datos](#Papel-de-las-bases-de-datos-en-el-análisis-de-datos)

## Introducción
Los sistemas de bases de datos (SGBD) son herramientas fundamentales para la gestión y organización de grandes volúmenes de datos. Se trata de un software que facilita el almacenamiento, la recuperación y la manipulación de datos de manera eficiente y segura. A continuación, se presentan algunos conceptos esenciales sobre los sistemas de bases de datos.
## Funciones principales de un SGBD
1. **Almacenamiento de datos**: Los SGBD permiten almacenar datos de manera estructurada, facilitando su acceso y gestión de forma eficiente.
2. **Garantía de integridad**: Aseguran que los datos almacenados sean consistentes y válidos, aplicando reglas de integridad.
3. **Seguridad**: Proveen mecanismos para controlar el acceso a los datos, protegiéndolos contra accesos no autorizados.
4. **Recuperación de datos**: Permiten la recuperación de datos en caso de fallos del sistema, asegurando la continuidad del servicio.
5. **Consultas y manipulación de datos**: Facilitan la realización de consultas complejas y la manipulación de datos mediante lenguajes específicos como SQL.
6. **Optimización del rendimiento**: Implementan técnicas para mejorar la velocidad de acceso y procesamiento de datos.
## Tipos de sistemas de bases de datos
1. **Bases de datos relacionales**: Organizan los datos en tablas con filas y columnas, utilizando claves primarias y foráneas para establecer relaciones entre ellas. El lenguaje, estandarizado, SQL, es comúnmente utilizado para gestionar estas bases de datos.
2. **Bases de datos NoSQL**: Diseñadas para manejar grandes volúmenes de datos no estructurados o semi-estructurados. Como ventajas sobre los sistemas relacionales se encuentran su escalabilidad y flexibilidad. Entre los ejemplos más habituales se incluyen bases de datos documentales, de tipo clave-valor, basadas en columnas y las bases de datos basadas en grafos.

## Modelo relacional
Es el modelo, todavía a día de hoy, más utilizado en los sistemas de bases de datos. Han sido tan influyentes que incluso los sistemas NoSQL han adoptado ciertos conceptos del modelo relacional.
Este modelo tiene como características principales:
- **Uso de tablas** como estructura básica para almacenar datos. Las tablas están compuestas por filas (registros) y columnas (atributos).
- **Filas o registros** representan entidades individuales dentro de la tabla. Es decir, en una tabla de "Clientes", cada fila representaría un cliente específico. En las tablas relacionales, cada fila debe ser única, lo que se logra mediante el uso de claves primarias.
- **Columnas o atributos** representan las propiedades o características de las entidades. En la tabla de "Clientes", las columnas podrían incluir "Nombre", "Dirección", "Teléfono", etc.
- **Claves primarias** se trata de una columna o un conjunto de columnas que identifican de manera única cada fila en una tabla. Por ejemplo, en una tabla de "Clientes", el atributo "id_cliente" podría ser la clave primaria, ya que no habrá dos clientes con el mismo "id_cliente".
- **Claves foráneas o secundarias** son columnas que establecen relaciones entre tablas. Las claves foráneas las forman una o más columnas cuyos valores coinciden con los valores de la clave primaria en otra tabla. Por ejemplo, en una tabla de "Pedidos", podría haber una columna "id_cliente" que contendrá identificadores de clientes que hacen referencia a la tabla "Clientes", de esa forma podremos saber cada pedido a qué cliente se refiere.
- **Índices** son estructuras que mejoran la velocidad de las consultas en una tabla. Funcionan como índices en un libro, permitiendo un acceso rápido a los datos sin tener que escanear toda la tabla. Las claves primarias y foráneas suelen estar indexadas automáticamente por el SGBD.
- **Restricciones de obligatoriedad (*NOT NULL*)** se utilizan para garantizar que una columna no pueda contener valores nulos. Esto es importante para asegurar que ciertos datos esenciales siempre estén presentes en los registros. Por ejemplo, en una tabla de "Clientes", podríamos establecer que la columna "Nombre" no puede ser nula, ya que cada cliente debe tener un nombre.
- **Restricciones de unicidad (*UNIQUE*)** aseguran que los valores en una columna o conjunto de columnas no se repiten en la tabla. Esto es útil para atributos que deben ser únicos, como direcciones de correo electrónico o números de identificación. Por ejemplo, en una tabla de "Usuarios", podríamos establecer que la columna "email" debe ser única para evitar que dos usuarios tengan la misma dirección de correo electrónico.
- **Claves alternativas** son columnas o conjuntos de columnas que podrían servir como clave primaria, puesto que no pueden repetir valores y no contienen valores nulos, pero no se han seleccionado como clave primaria, ya que se dispondrá de una mejor opción como clave primaria. En todo caso son fundamentales para garantizar la integridad de los datos. Las claves alternativas poseen restricciones de unicidad y de obligatoriedad.

## SQLite y MySQL/Maria DB
Ambos son sistemas de gestión de bases de datos relacionales (RDBMS) que utilizan SQL como lenguaje para gestionar y manipular datos. Sin embargo, tienen diferencias significativas en términos de arquitectura, uso y características.
En esta tabla se describen algunas de las diferencias clave entre SQLite y MySQL/MariaDB:
| Característica          | SQLite                                      | MySQL/MariaDB                             |
|------------------------|---------------------------------------------|-------------------------------------------|
| Arquitectura           | Embebido, no requiere servidor              | Cliente-servidor, requiere un servidor dedicado |
| Instalación            | Muy fácil, solo un archivo                  | Requiere instalación y configuración del servidor |
| Escalabilidad          | Adecuado para aplicaciones pequeñas a medianas | Adecuado para aplicaciones grandes y de alta concurrencia |
| Rendimiento            || Bueno para operaciones de lectura y escritura ligeras | Mejor rendimiento en operaciones complejas y de alta concurrencia |
| Soporte de concurrencia| Limitado, no maneja múltiples conexiones simultáneas bien | Excelente, maneja múltiples conexiones simultáneas eficientemente |
| Características avanzadas | Limitadas, no soporta procedimientos almacenados, vistas complejas, etc. | Soporta características avanzadas como procedimientos almacenados, vistas, triggers, etc. |
| Uso típico             | Aplicaciones móviles, aplicaciones de escritorio, prototipos | Aplicaciones web, sistemas empresariales, aplicaciones de gran escala |
| Mantenimiento          | Bajo, no requiere administración del servidor | Requiere administración y mantenimiento del servidor |

## El lenguaje SQL
SQL (Structured Query Language) es el lenguaje estándar utilizado para gestionar y manipular bases de datos relacionales. Permite realizar diversas operaciones sobre los datos almacenados en las tablas de una base de datos. A continuación, se describen algunas de las operaciones más comunes que se pueden realizar con SQL:
1. **DDL (Data Definition Language)**: Estas operaciones se utilizan para definir y modificar la estructura de las tablas y otros objetos de la base de datos. Algunos comandos DDL comunes incluyen:
   - `CREATE TABLE`: Crea una nueva tabla en la base de datos.
   - `ALTER TABLE`: Modifica la estructura de una tabla existente (por ejemplo, agregar o eliminar columnas).
   - `DROP TABLE`: Elimina una tabla de la base de datos.
2. **DML (Data Manipulation Language)**: Estas operaciones se utilizan para manipular los datos dentro de las tablas. Algunos comandos DML comunes incluyen:
   - `INSERT INTO`: Agrega nuevos registros a una tabla.
   - `UPDATE`: Modifica los datos existentes en una tabla.
   - `DELETE`: Elimina registros de una tabla.
3. **DQL (Data Query Language)**: Estas operaciones se utilizan para consultar y recuperar datos de las tablas. El comando DQL más común es:
   - `SELECT`: Recupera datos de una o más tablas, permitiendo especificar qué columnas y filas se desean obtener.
4. **DCL (Data Control Language)**: Estas operaciones se utilizan para controlar el acceso a los datos y gestionar permisos. Algunos comandos DCL comunes incluyen:
   - `GRANT`: Otorga permisos a los usuarios para realizar ciertas operaciones en la base de datos.
   - `REVOKE`: Revoca permisos previamente otorgados a los usuarios.
5. **TCL (Transaction Control Language)**: Estas operaciones se utilizan para gestionar transacciones en la base de datos, asegurando la integridad de los datos. Algunos comandos TCL comunes incluyen:
   - `COMMIT`: Confirma una transacción, haciendo permanentes los cambios realizados.
   - `ROLLBACK`: Revierte una transacción, deshaciendo los cambios realizados desde el último COMMIT.
Estos son solo algunos ejemplos de las operaciones que se pueden realizar con SQL. El lenguaje SQL es muy poderoso y versátil, y es fundamental para trabajar con bases de datos relacionales.

## Acceso desde Python
Python ofrece varias bibliotecas para interactuar con bases de datos relacionales utilizando SQL. Algunas de las bibliotecas más populares incluyen:
1. **SQLite3**: Esta biblioteca está incluida en la biblioteca estándar de Python y permite trabajar con bases de datos SQLite. Es ideal para aplicaciones pequeñas y medianas debido a su simplicidad y facilidad de uso. Su módulo estándar es `sqlite3`.
2. **MySQL Connector/Python**: Esta biblioteca oficial de MySQL permite conectar aplicaciones Python con bases de datos MySQL o MariaDB. Proporciona una interfaz sencilla para ejecutar consultas SQL y manejar resultados. Su módulo es `mysql.connector` o `pymysql`.

Desde **Pandas** se facilita el acceso a bases de datos relacionales utilizando las funciones `read_sql_query()` y `to_sql()`. Estas funciones permiten ejecutar consultas SQL y cargar los resultados directamente en DataFrames de Pandas, así como guardar DataFrames en tablas de bases de datos. Para utilizar estas funciones, es necesario tener una conexión activa a la base de datos mediante una biblioteca compatible, como SQLite3 o MySQL Connector/Python.

## Papel de las bases de datos en el análisis de datos
Las bases de datos se integran en distintos puntos del ciclo de análisis:
* **Obtención de datos** (lectura directa de tablas).
* **Preparación** (filtrado, transformación, limpieza mediante SQL).
* **Almacenamiento de resultados intermedios**.
* **Validación de información**.
* **Integración con herramientas de visualización y modelado**.


