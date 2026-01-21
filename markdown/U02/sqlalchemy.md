# SQLAlchemy
## Índice
- [Introducción a SQLAlchemy](#Introducción-a-SQLAlchemy)
- [Realizar conexiones con SQLAlchemy](#Realizar-conexiones-con-SQLAlchemy)
  - [Método `create_engine`](#Método-create_engine)
  - [Conexión a una base de datos SQLite](#Conexión-a-una-base-de-datos-SQLite)
  - [Conexión a una base de datos MySQL](#Conexión-a-una-base-de-datos-MySQL)
- [Ejecutar instrucciones SQL](#Ejecutar-instrucciones-SQL)
  - [Función `text()`](#Función-text())
  - [Método `connect()`](#Método-connect())
  - [Ejecución de instrucciones SQL de tipo DDL y DML](#Ejecución-de-instrucciones-SQL-de-tipo-DDL-y-DML)
    - [Confirmar y anular transacciones](#Confirmar-y-anular-transacciones)
    - [Uso de transacciones automáticas](#Uso-de-transacciones-automáticas)
  - [Ejecutar consultas SQL de tipo SELECT](#Ejecutar-consultas-SQL-de-tipo-SELECT)
- [Usar pandas con SQLAlchemy](#Usar-pandas-con-SQLAlchemy)
  - [Leer datos con `read_sql()`](#Leer-datos-con-read_sql())
    - [Uso de índices al leer datos](#Uso-de-índices-al-leer-datos)
    - [Otros parámetros de `read_sql()`](#Otros-parámetros-de-read_sql())
      - [`chunksize`](#chunksize)
      - [`dtype`](#dtype)
      - [`coerce_float`](#coerce_float)
  - [Escribir datos con `to_sql()`](#Escribir-datos-con-to_sql())
    - [Problemas de conversión de tipos](#Problemas-de-conversión-de-tipos)
        -

## Introducción a SQLAlchemy
SQLAlchemy es una biblioteca de Python que proporciona un conjunto completo de herramientas para trabajar con bases de datos relacionales. Ofrece una abstracción de alto nivel para interactuar con bases de datos utilizando SQL, así como un ORM (Object-Relational Mapping) que permite mapear clases de Python a tablas de bases de datos.

Esta librería facilita la conexión a diferentes sistemas de gestión de bases de datos (DBMS) como MySQL, PostgreSQL, SQLite, entre otros, y permite ejecutar consultas SQL de manera eficiente y segura.

Es la conexión habitual a bases de datos en proyectos de análisis de datos y desarrollo web en Python.

## Características principales de SQLAlchemy:
- **ORM (Object-Relational Mapping)**: Permite mapear clases de Python a tablas de bases de datos, facilitando la manipulación de datos como objetos.
- **Core SQL Expression Language**: Proporciona una forma de construir consultas SQL de manera programática utilizando expresiones de Python.
- **Soporte para múltiples DBMS**: Permite conectarse a diferentes sistemas de gestión de bases de datos utilizando un conjunto común de herramientas.
- **Gestión de conexiones**: Facilita la gestión de conexiones a bases de datos, incluyendo el manejo de transacciones.
- **Migraciones de esquemas**: A través de herramientas como Alembic, permite gestionar cambios en el esquema de la base de datos de manera controlada.

## Realizar conexiones con SQLAlchemy
### Método `create_engine`
Para conectarse a una base de datos utilizando SQLAlchemy, se utiliza el método `create_engine()`, que crea un objeto de motor de base de datos. Este objeto se utiliza para establecer conexiones y ejecutar consultas SQL.
Este método requiere una cadena de conexión, mediante la cual se especifica el motor de basde de datos que vamos a utilizar y los datos que se requieren para conectarnos a la base de datos (host, usuario, contraseña, etc.).

### Conexión a una base de datos SQLite
Basta con indicar el motor de base de datos SQLite y el nombre del archivo de base de datos que se va a utilizar:



```python
from sqlalchemy import create_engine
engine = create_engine('sqlite:///ejemplo.db')
```

### Conexión a una base de datos MySQL

La conexión se realiza con una cadena de conexión la cual comienza con mysql+pymysql://. (indicando que usamos la librería **pymysql** para la conexión, se podría usar otras como por ejemplo `mysql_connector_db`) y después se indica el usuario y la contraseña (separados por `:`), después se indica el símbolo "@" y el host (normalmente localhost). Seguido al nombre del host se puede indicar el puerto de conexión (se haría usando dos puntos y después el puerto). Finalmente se indica el nombre de la base de datos a la que se conecta (separada por una barra inclinada `/`).

Ejemplo de conexión:


```python
from sqlalchemy import create_engine
import pymysql
# Conexión a MySQL en el servidor local usando el usuario prueba, contraseña A12345 y la base de datos prueba
# se usa el puerto 3306 por defecto
# engine = create_engine('mysql+pymysql://prueba:A12345@localhost/prueba')
engine = create_engine('mysql+pymysql://prueba:A12345@localhost/prueba')
```

## Ejecutar instrucciones SQL
### Función `text()`
En SQLAlchemy, no todo string es una sentencia SQL ejecutable.
La función text() existe para convertir una cadena de texto en un objeto SQL entendible y seguro para SQLAlchemy.

Lo que hace es convertir un texto (string) normal en un obeto SQL que SQLAlchemy puede ejecutar de forma más segura, evitando problemas como inyecciones SQL.

Ese objeto:
* Puede ejecutarse
* Puede recibir parámetros
* Puede ser validado por SQLAlchemy


```python
from sqlalchemy import text
```

### Método `connect()`
Este método crea una conexión a la base de datos que se puede usar para ejecutar instrucciones SQL. Se utiliza junto con el método `execute()` para ejecutar sentencias SQL.
Requiere cerrar la conexión una vez que se ha terminado de usar y además capturar posibles excepciones.
Su forma de uso es la siguiente:
```python
conn = engine.connect()
try:
    conn.execute(...instrucción SQL...)
    ....procesar los resultados...
finally:
    conn.close()
```

Sin embargo, una forma más sencilla de usarlo es mediante el uso de un bloque `with`, que se encarga automáticamente de cerrar la conexión al finalizar el bloque:
```python
with engine.connect() as conn:
    conn.execute(...instrucción SQL...)
    ....procesar los resultados...
```

### Ejecución de instrucciones SQL de tipo DDL y DML
Una vez que tenemos el motor de conexión, podemos ejecutar instrucciones SQL utilizando el método `execute()` del objeto de conexión. Por ejemplo, para crear una tabla:


```python
sql_create =  text("""
        CREATE TABLE IF NOT EXISTS clientes (
            id_cliente INT PRIMARY KEY AUTO_INCREMENT,
            nombre VARCHAR(50) NOT NULL,
            apellidos VARCHAR(50) NOT NULL
        )
    """)
with engine.connect() as conn:
    conn.execute(sql_create)
```

Para añadir datos podemos utilizar parámetros en la función text() y pasar los valores como un diccionario al método `execute()`:


```python
sql_insert = text("""
        INSERT INTO clientes (nombre, apellidos)
        VALUES (:nombre, :apellidos)
    """)
with engine.connect() as conn:
    conn.execute(sql_insert, {"nombre": "Ana", "apellidos": "García"})
    conn.execute(sql_insert, {"nombre": "Luis", "apellidos": "Martínez"})
```

Esta es la forma más recomendable por su limpieza, seguridad y facilidad de uso.

Se puede incluso añadir múltiples filas a la vez pasando una lista de diccionarios:


```python
clientes = [
    {"nombre": "Marta", "apellidos": "López"},
    {"nombre": "Carlos", "apellidos": "Sánchez"},
    {"nombre": "Elena", "apellidos": "Fernández"},
    {"nombre": "Mateo", "apellidos": "Villanueva"}
]
with engine.connect() as conn:
    conn.execute(sql_insert, clientes)
```

Para actualizar datos, se obra de la misma forma:


```python
sql_update = text("""
        UPDATE clientes
        SET apellidos = :apellidos
        WHERE nombre = :nombre
    """)
# Modifica el apellido de Ana
with engine.connect() as conn:
    conn.execute(sql_update, {"nombre": "Ana", "apellidos": "Gómez"})
```

La misma idea para eliminar datos:


```python
sql_delete = text("""
        DELETE FROM clientes
        WHERE nombre = :nombre
    """)
with engine.connect() as conn:
    conn.execute(sql_delete, {"nombre": "Mateo"})
```

### Confirmar y anular transacciones
Para que los datos se guarden de forma permanente en la base de datos, es necesario confirmar la transacción utilizando el método `commit()`.

Para ello disponemos del método `commit` en la conexión:


```python
clientes = [
    {"nombre": "Marta", "apellidos": "López"},
    {"nombre": "Carlos", "apellidos": "Sánchez"},
    {"nombre": "Elena", "apellidos": "Fernández"},
    {"nombre": "Mateo", "apellidos": "Villanueva"}
]
with engine.connect() as conn:
    conn.execute(sql_insert, clientes)
    conn.commit()
```

De no ejecutar el método `commit()`, los cambios realizados no se guardarán en la base de datos.

Por supuesto, también es posible anular una transacción utilizando el método `rollback()` en caso de que lo estimemos necesario.

### Uso de transacciones automáticas
Otra forma de gestionar las transacciones es utilizando el método `begin()` en un bloque `with`. Esto crea una transacción automática que se confirma al finalizar el bloque si no se produce ninguna excepción, o se anula si ocurre alguna excepción.

Ejemplo:


```python
clientes = [
    {"nombre": "Sofía", "apellidos": "Ruiz"},
    {"nombre": "Diego", "apellidos": "Morales"}
]
with engine.begin() as conn:
    conn.execute(sql_insert, clientes)
```

En este caso, se añaden estos dos clientes de forma definitiva (salvo que ocurra alguna excepción durante la ejecución del bloque).

### Ejecutar consultas SQL de tipo SELECT
Para ejecutar consultas SQL que devuelven resultados, como las sentencias SELECT, se utiliza el mismo método `execute()`, pero luego se deben procesar los resultados, ya que en este caso se devuelve un objeto de resultados que se puede iterar para obtener las filas devueltas por la consulta.

Ejemplo:


```python
sql_select = text("""
        SELECT id_cliente, nombre, apellidos
        FROM clientes
    """)
with engine.connect() as conn:
    result = conn.execute(sql_select)
    for fila in result:
        print(f"id_cliente: {fila.id_cliente}, Nombre: {fila.nombre}, Apellidos: {fila.apellidos}")
```

    ID: 7, Nombre: Marta, Apellidos: López
    ID: 8, Nombre: Carlos, Apellidos: Sánchez
    ID: 9, Nombre: Elena, Apellidos: Fernández
    ID: 10, Nombre: Mateo, Apellidos: Villanueva
    

Disponemos de métodos en el objeto de resultado para personalizar la manipulación de los datos devueltos. Son:
* `fetchone()`: Devuelve la siguiente fila del conjunto de resultados como una tupla. Si no hay más filas, devuelve `None`.
* `fetchall()`: Devuelve todas las filas restantes del conjunto de resultados como una lista de tuplas.
* `first()`: Devuelve la primera fila del conjunto de resultados o `None` si no hay filas.

No obstante, lo normal es iterar directamente sobre el objeto de resultados como se ha hecho en el ejemplo anterior.

## Usar pandas con SQLAlchemy
Pandas proporciona una forma sencilla de interactuar con bases de datos utilizando SQLAlchemy. Podemos utilizar las funciones `read_sql()` y `to_sql()` para leer y escribir datos en bases de datos compatibles con SQLAlchemy.
### Leer datos con `read_sql()`
La función `read_sql()` permite ejecutar una consulta SQL y cargar los resultados directamente en un DataFrame de pandas.

Ejemplo:


```python
import pandas as pd
dfClientes = pd.read_sql("""
        SELECT id_cliente, nombre, apellidos
        FROM clientes
    """, con=engine)
print(dfClientes)
```

       id_cliente  nombre   apellidos
    0           7   Marta       López
    1           8  Carlos     Sánchez
    2           9   Elena   Fernández
    3          10   Mateo  Villanueva
    4          11   Sofía        Ruiz
    5          12   Diego     Morales
    

### Uso de índices al leer datos
Es posible especificar una columna para que actúe como índice del DataFrame utilizando el parámetro `index_col` de la función `read_sql()`.


```python
dfClientes = pd.read_sql("""
        SELECT id_cliente, nombre, apellidos
        FROM clientes
    """, con=engine, index_col="id_cliente")
print(dfClientes)
```

                nombre   apellidos
    id_cliente                    
    7            Marta       López
    8           Carlos     Sánchez
    9            Elena   Fernández
    10           Mateo  Villanueva
    11           Sofía        Ruiz
    12           Diego     Morales
    

En el caso de que haya varias columnas que formen el índice, se puede pasar una lista de nombres de columnas al parámetro `index_col`.

Por ejemplo, vamos a crear una tabla de pedidos donde la clave primaria esté formada por dos columnas: `n_pedido` e `id_cliente`.

Añadiremos datos de pedidos para clientes con índices 7, 8 y 9 (que suponemos que los que tenemos en la tabla `clientes`).


```python
sqlCreacion = text("""
        CREATE TABLE IF NOT EXISTS pedidos (
            n_pedido INT,
            id_cliente INT,
            producto VARCHAR(100) NOT NULL,
            cantidad INT NOT NULL,
            FOREIGN KEY (id_cliente) REFERENCES clientes(id_cliente),
            PRIMARY KEY (n_pedido, id_cliente)
        )
    """)

sqlInsert = text("""
        INSERT INTO pedidos (n_pedido, id_cliente, producto, cantidad)
        VALUES (:n_pedido, :id_cliente, :producto, :cantidad)
    """)
with engine.connect() as conn:
    conn.execute(sqlCreacion)
    pedidos = [
        {"n_pedido": 1, "id_cliente": 7, "producto": "Portátil", "cantidad": 2},
        {"n_pedido": 2, "id_cliente": 7, "producto": "Ratón", "cantidad": 5},
        {"n_pedido": 1, "id_cliente": 8, "producto": "Teclado", "cantidad": 3},
        {"n_pedido": 1, "id_cliente": 9, "producto": "Monitor", "cantidad": 1}
    ]
    conn.execute(sqlInsert, pedidos)
    conn.commit()
```

Ahora recogemos los datos indicando el índice de dos columnas:


```python
sqlSelectPedidos = """
        SELECT n_pedido, id_cliente, producto, cantidad
        FROM pedidos
    """
dfPedidos = pd.read_sql(sqlSelectPedidos, con=engine, index_col=["n_pedido", "id_cliente"])
print(dfPedidos)
```

                         producto  cantidad
    n_pedido id_cliente                    
    1        7           Portátil         2
             8            Teclado         3
             9            Monitor         1
    2        7              Ratón         5
    

### Otros parámetros de `read_sql()`
#### `chunksize`
El parámetro `chunksize` permite leer los datos en fragmentos (chunks) de un tamaño específico. Esto es útil cuando se trabaja con conjuntos de datos grandes que no caben en memoria.

En este ejemplo tomaremos un tamaño de fragmento de 2 filas:


```python
sqlSelectLarge = """
        SELECT *
        FROM clientes
    """
for chunk in pd.read_sql(sqlSelectLarge, con=engine, chunksize=2):
    print("Chunk:")
    print(chunk)
```

    Chunk:
       id_cliente  nombre apellidos
    0           7   Marta     López
    1           8  Carlos   Sánchez
    Chunk:
       id_cliente nombre   apellidos
    0           9  Elena   Fernández
    1          10  Mateo  Villanueva
    Chunk:
       id_cliente nombre apellidos
    0          11  Sofía      Ruiz
    1          12  Diego   Morales
    

#### `dtype`
El parámetro `dtype` permite especificar el tipo de datos para las columnas del DataFrame resultante. Se puede pasar un diccionario donde las claves son los nombres de las columnas y los valores son los tipos de datos deseados.


```python
sqlSelect = """
        SELECT id_cliente, nombre, apellidos
        FROM clientes
    """
dfClientes = pd.read_sql(sqlSelect, con=engine, dtype={"id_cliente": "string"})
print(dfClientes.dtypes)
print(dfClientes)
```

    id_cliente    string[python]
    nombre                object
    apellidos             object
    dtype: object
      id_cliente  nombre   apellidos
    0          7   Marta       López
    1          8  Carlos     Sánchez
    2          9   Elena   Fernández
    3         10   Mateo  Villanueva
    4         11   Sofía        Ruiz
    5         12   Diego     Morales
    

### `coerce_float`
El parámetro `coerce_float` permite convertir automáticamente las columnas numéricas a tipo float. Por defecto, este parámetro está establecido en `True`.

### Escribir datos con `to_sql()`
El método `to_sql()`, perteneciente a la clase DataFrame de pandas, permite escribir un DataFrame de pandas directamente en una tabla de la base de datos compatible con SQLAlchemy.
Este método recibe como argumentos:
- El nombre de la tabla
- La conexión a la base de datos
- Parámetros opcionales:
    -
    - `if_exists` para especificar qué hacer si la tabla ya existe. Posibilidades:
        - `fail`: No se puede crear la tabla (valor predeterminado)
        - `replace`: Se elimina la tabla existente y se crea una nueva
        - `append`: Se añaden los datos a la tabla existente
    - `index` para indicar si se debe escribir el índice del DataFrame como una columna separada en la tabla. Sus valores posibles son `True` (valor predeterminado) y `False`.
    - `index_label` permite especificar el nombre de la columna en la que se colocará el índice del DataFrame (solo en caso de que `index` sea `True`). Si no se especifica, se utilizará el nombre del índice del DataFrame.
    - `schema` permite indicar el esquema de la base de datos, en motores de bases de datos que lo admitan como por ejemplo Oracle o PostgreSQL.
    - `dtype` para especificar el tipo de datos de las columnas de la tabla.

Ejemplo:


```python
# Sring permite hacer conversiones de tipos para valores de texto
from sqlalchemy import String
df = pd.DataFrame({
    "matricula": ["0031VCD", "4356WDF", "6789UHY"],
    "marca":["Toyota", "Honda", "Nissan"],
    "modelo":["Camry", "Civic", "Accord"],
})
df.set_index("matricula", inplace =True)
df.to_sql("vehiculos",
          engine,
          if_exists="replace",
          index=True,
          dtype = {"matricula": String(10),
                   "marca": String(20),
                   "modelo": String(20)}
)

```




    3



### Problemas de conversión de tipos
Al escribir datos en una base de datos, pueden surgir problemas de conversión de tipos entre los tipos de datos de pandas y los tipos de datos de la base de datos.

Si en el ejemplo anterior no hubiéramos especificado el tipo de datos de las columnas mediante el parámetro `dtype`, pandas habría intentado inferir los tipos de datos automáticamente, lo que podría haber llevado a errores o conversiones incorrectas.

Para evitar estos problemas, es recomendable utilizar el parámetro `dtype` para especificar explícitamente los tipos de datos de las columnas al escribir datos en la base de datos.

SQLAlchemy proporciona tipos de datos específicos que se pueden utilizar para este propósito. Entre ellas:
- `String(length)`: Para cadenas de texto con una longitud máxima especificada. Se suele traducir a `VARCHAR(length)` en la base de datos.
- `Integer`: Para números enteros. Se suele traducir a `INT` en la base de datos.
- `Float`: Para números de punto flotante. Se suele traducir a `FLOAT` o `DOUBLE` en la base de datos.
- `Boolean`: Para valores booleanos (`True` o `False`). Se suele traducir a `BOOLEAN` o `TINYINT(1)` en la base de datos.
- `Date`: Para fechas. Se suele traducir a `DATE` en la base de datos.
- `DateTime`: Para fechas y horas. Se suele traducir a `DATETIME` en la base de datos.
- `TIMESTAMP`: Para marcas de tiempo. Se suele traducir a `TIMESTAMP` en la base de datos.
- `Text`: Para textos largos. Se suele traducir a `TEXT` en la base de datos (o LONGTEXT en Oracle).
- `Numeric`: Permite indicar números decimales de coma fija. Por ejemplo `Numeric(5, 2)`, que se puede traducir a `DECIMAL(5, 2)` en la base de datos (o NUMBER(5,2) en Oracle).

