# Uso de SQLite
## Características principales
SQLite es uno de los sistemas de gestión de bases de datos relacionales (RDBMS) más populares y ampliamente utilizados en el mundo.
Es una base de datos embebida y eso facilita su portabilidad y falta de requerimientos de configuración compleja. A continuación, se presentan algunas de sus características principales.
### Bases de datos embebida
Lo que redunda en:
- No requiere un servidor separado para funcionar.
- La base de datos se almacena en un solo archivo en el sistema de archivos con extensión .sqlite o .db.
- En Python, se puede utilizar el módulo `sqlite3` que viene incluido en la biblioteca estándar para interactuar con bases de datos SQLite sin necesidad de instalar software adicional.
### Sistema autocontenido
- Todo el motor de SQL está contenido en una sola biblioteca
- Todas las funcionalidades necesarias para gestionar la base de datos están integradas en la biblioteca SQLite sin necesidad de dependencias externas.
- Es fácil de distribuir y desplegar aplicaciones que utilizan SQLite, ya que no se requieren instalaciones adicionales.
### Cumplimiento del estándar SQL
- SQLite soporta una gran parte del estándar SQL-92
- Soporta las instrucciones DDL `CREATE`, `ALTER` y `DROP`.
- Soporta las instrucciones DML `SELECT`, `INSERT`, `UPDATE` y `DELETE`.
- Soporta transacciones ACID (Atomicidad, Consistencia, Aislamiento y Durabilidad), que es el estándar de manejo de transacciones en bases de datos. Las instrucciones  `COMMIT` y `ROLLBACK` son compatibles.

## Conexión a una base de datos SQLite en Python
### Creación automática de la base de datos
En SQLite, si intentas conectarte a una base de datos que no existe, SQLite la creará automáticamente. Esto facilita la creación y gestión de bases de datos sin necesidad de pasos adicionales.
Para ello necesitamos importar la librería y crear una conexión a la base de datos mediante la función `sqlite3.connect()`, que recibe como argumento el nombre del archivo de la base de datos. Si el archivo no existe, SQLite lo creará automáticamente.

```python
import sqlite3

# Crear una conexión a la base de datos (se crea si no existe)
conexion = sqlite3.connect("../../jupyter/U02/prueba.db")
```

### Apertura de una base de datos existente
Si el archivo de la base de datos ya existe, SQLite simplemente abrirá la conexión a esa base de datos sin crear un nuevo archivo.


```python
conexion = sqlite3.connect("prueba.db")  # Abre la base de datos existente
```

### Conexión en memoria
SQLite también permite crear bases de datos en memoria. Estas bases de datos son temporales y se almacenan en la RAM, lo que las hace muy rápidas pero volátiles (se pierden al cerrar la conexión).
Se utilizan para pruebas o situaciones donde no se necesita persistencia de datos.


```python
conexion = sqlite3.connect(":memory:")  # Crea una base de datos en memoria
```

### Cierre de la conexión
Después de terminar de trabajar con la base de datos, es importante cerrar la conexión utilizando el método `close()`.


```python
conexion.close()
```

# Uso de cursores para ejecutar consultas SQL
Para ejecutar consultas SQL en SQLite, se utiliza un objeto cursor. El cursor permite ejecutar comandos SQL y recuperar resultados.
## Creación de un cursor
Después de establecer una conexión a la base de datos, se debe crear un cursor utilizando el método `cursor()` de la conexión.Ese cursor actuará como intermediario para ejecutar las consultas SQL.


```python
conexion = sqlite3.connect("empresas.db")
cursor = conexion.cursor()
```

# Ejecución de instrucciones SQL
Una vez que se tiene un cursor, se pueden ejecutar instrucciones SQL utilizando el método `execute()` del cursor. Este método recibe como argumento una cadena que contiene la consulta SQL.


```python
cursor.execute("CREATE TABLE IF NOT EXISTS clientes(" +
               "id_cliente INTEGER PRIMARY KEY, "+
               "nombre TEXT, apellidos TEXT)")
```




    <sqlite3.Cursor at 0x10458d1c0>



La coletilla `IF NOT EXISTS` en la instrucción `CREATE TABLE` asegura que la tabla solo se cree si no existe previamente, evitando errores si se intenta crear una tabla con el mismo nombre.
Si la tabla ya existe, y no utilizamos `IF NOT EXISTS`, SQLite generará un error indicando que la tabla ya existe.
Podemos capturar el error utilizando un bloque `try-except` para manejar la excepción y evitar que el programa se detenga abruptamente.


```python
try:
    cursor.execute("CREATE TABLE clientes(" +
               "id_cliente INTEGER PRIMARY KEY, "+
               "nombre TEXT, apellidos TEXT)")
    print("Tabla creada correctamente")
except sqlite3.OperationalError as e:
    print("Error al crear la tabla:", e) # Muestra el mensaje de error usando el objeto de excepción 'e'
```

    Error al crear la tabla: table clientes already exists


## Inserción de datos
Después de crear una tabla, se pueden insertar datos utilizando la instrucción `INSERT INTO`.


```python
cursor.execute("INSERT INTO clientes (nombre,apellidos) VALUES ('Juan', 'Perez')")
cursor.execute("INSERT INTO clientes (nombre,apellidos) VALUES ('Ana', 'Gómez')")
```




    <sqlite3.Cursor at 0x10458d1c0>




Para saber si la inserción fue exitosa, se puede utilizar el atributo `rowcount` del cursor, que indica el número de filas afectadas por la última operación ejecutada.


```python
cursor.execute("INSERT INTO clientes (nombre,apellidos) VALUES ('Luis', 'Martín')")
print("Número de filas afectadas:", cursor.rowcount)
```

    Número de filas afectadas: 1


También se puede utilizar un diccionario para mapear los nombres de las columnas a los valores correspondientes, lo que mejora la legibilidad del código y reduce el riesgo de errores al insertar datos en tablas con muchas columnas.


```python
dic = {'nombre': 'María', 'apellidos': 'López'}
cursor.execute("INSERT INTO clientes (nombre, apellidos) VALUES (:nombre, :apellidos)", dic)
```




    <sqlite3.Cursor at 0x10458d1c0>



Podemos insertar múltiples filas utilizando `executemany()`. Es método es útil para insertar grandes cantidades de datos de manera eficiente. Funciona de manera similar a `execute()`, pero recibe una lista de tuplas, como segundo parámetro, con los valores a insertar.


```python
cursor.executemany("INSERT INTO clientes (nombre,apellidos) VALUES (?,?)",
                   [("Luis", "Martínez"),
                    ("Marta", "Reol"),
                    ("Carlos", "Bañes")])
```




    <sqlite3.Cursor at 0x10458d1c0>



En este caso podemos utilizar también un diccionario para cada fila a insertar, utilizando una lista de diccionarios como segundo parámetro de `executemany()`.


```python
datos = [
    {'nombre': 'Sofía', 'apellidos': 'Ramírez'},
    {'nombre': 'Diego', 'apellidos': 'Torres'},
    {'nombre': 'Elena', 'apellidos': 'Vega'}
]
cursor.executemany("INSERT INTO clientes (nombre, apellidos) VALUES (:nombre, :apellidos)", datos)
```




    <sqlite3.Cursor at 0x10458d1c0>



Esa instrucción utiliza un marcador de posición `?` para los valores que se van a insertar, y una lista de tuplas con los valores correspondientes.

## Modificación de datos
Para modificar datos existentes, se utiliza la instrucción `UPDATE`.


```python
conexion.execute("UPDATE clientes SET apellidos = 'López' WHERE apellidos = 'Reol'")
```




    <sqlite3.Cursor at 0x104329240>



## Eliminación de datos
Para eliminar datos, se utiliza la instrucción `DELETE`.


```python
conexion.execute("DELETE FROM clientes WHERE apellidos = 'Bañes'")
```




    <sqlite3.Cursor at 0x10432b540>



### Commit y rollback
Después de realizar operaciones que modifican la base de datos (como `INSERT`, `UPDATE` o `DELETE`), es necesario confirmar los cambios utilizando el método `commit()` de la conexión. Si se desea deshacer los cambios realizados desde la última confirmación, se puede utilizar el método `rollback()`.
Tanto `commit()` como `rollback()` aceptan o anulan las instrucciones ejecutadas desde el inicio de la actual transacción. Una transacción comienza automáticamente cuando se ejecuta la primera instrucción que modifica la base de datos después de una confirmación o anulación.


```python
cursor.execute("INSERT INTO clientes (nombre,apellidos) VALUES ('Andrés', 'Rojo')")
conexion.commit()
```

## Consulta de datos
Para leer datos de la base de datos, se utiliza la instrucción `SELECT`.
Después de ejecutar una consulta `SELECT`, se pueden recuperar los resultados utilizando métodos como `fetchall()` o `fetchone()`.
### Recuperar todos los resultados
El método `fetchall()` recupera todos los resultados de la consulta y los devuelve como una lista de tuplas.


```python
filas = cursor.execute("SELECT * FROM clientes").fetchall()
for fila in filas:
    print(fila)
```

    (1, 'Juan', 'Perez')
    (2, 'Ana', 'Gómez')
    (3, 'Laura', 'Ramírez')
    (4, 'Sergio', 'Torres')
    (5, 'Juan', 'Perez')
    (6, 'Ana', 'Gómez')
    (7, 'Luis', 'Martín')
    (8, 'Luis', 'Martín')
    (9, 'Juan', 'Perez')
    (10, 'Ana', 'Gómez')
    (11, 'Luis', 'Martín')
    (12, 'María', 'López')
    (13, 'Luis', 'Martínez')
    (14, 'Marta', 'López')
    (16, 'Sofía', 'Ramírez')
    (17, 'Diego', 'Torres')
    (18, 'Elena', 'Vega')
    (19, 'Andrés', 'Rojo')


### Obtener un solo resultado
El método `fetchone()` recupera una sola fila a la vez. SI ya no hay más filas, devuelve `None`.


```python
# Bucle para recuperar una fila a la vez
cursor.execute("SELECT * FROM clientes")
fila = cursor.fetchone()
while fila is not None:
    print(fila)
    fila = cursor.fetchone()
```

    (1, 'Juan', 'Perez')
    (2, 'Ana', 'Gómez')
    (3, 'Laura', 'Ramírez')
    (4, 'Sergio', 'Torres')
    (5, 'Juan', 'Perez')
    (6, 'Ana', 'Gómez')
    (7, 'Luis', 'Martín')
    (8, 'Luis', 'Martín')
    (9, 'Juan', 'Perez')
    (10, 'Ana', 'Gómez')
    (11, 'Luis', 'Martín')
    (12, 'María', 'López')
    (13, 'Luis', 'Martínez')
    (14, 'Marta', 'López')
    (16, 'Sofía', 'Ramírez')
    (17, 'Diego', 'Torres')
    (18, 'Elena', 'Vega')
    (19, 'Andrés', 'Rojo')


### Iteración directa sobre el cursor de resultados
También se puede iterar directamente sobre el cursor después de ejecutar una consulta `SELECT`.


```python
for fila in cursor.execute("SELECT * FROM clientes"):
    print(fila)
```

    (1, 'Juan', 'Perez')
    (2, 'Ana', 'Gómez')
    (3, 'Laura', 'Ramírez')
    (4, 'Sergio', 'Torres')
    (5, 'Juan', 'Perez')
    (6, 'Ana', 'Gómez')
    (7, 'Luis', 'Martín')
    (8, 'Luis', 'Martín')
    (9, 'Juan', 'Perez')
    (10, 'Ana', 'Gómez')
    (11, 'Luis', 'Martín')
    (12, 'María', 'López')
    (13, 'Luis', 'Martínez')
    (14, 'Marta', 'López')
    (16, 'Sofía', 'Ramírez')
    (17, 'Diego', 'Torres')
    (18, 'Elena', 'Vega')
    (19, 'Andrés', 'Rojo')


Es fácil transoformar los resultados en un formato más legible, como diccionarios, listas de listas, DataFrames de pandas, etc.

## Transacciones
SQLite soporta transacciones ACID, lo que garantiza la integridad de los datos durante las operaciones de modificación.
### Commit
Después de realizar operaciones de inserción, actualización o eliminación, es importante confirmar los cambios utilizando el método `commit()` de la conexión.


```python
conexion.commit()
```

### Rollback
Si percibimos que hemos cometido un error durante una transacción, se pueden revertir los cambios utilizando el método `rollback()`.


```python
conexion.rollback()
```

## Gestión de errores
Es importante manejar los errores al trabajar con bases de datos. Se pueden utilizar bloques `try-except` para capturar excepciones y manejar errores de manera adecuada.
Entre las clases de excepciones más comunes en SQLite se encuentran:
- `sqlite3.OperationalError`: errores relacionados con la operación de la base de datos, como problemas de conexión o errores en las consultas SQL.
- `sqlite3.IntegrityError`: errores de integridad, como violaciones de claves primarias o restricciones únicas.
- `sqlite3.DatabaseError`: errores generales de la base de datos.
- `sqlite3.ProgrammingError`: errores relacionados con la programación, como el uso incorrecto de cursores o conexiones.
- `sqlite3.DataError`: errores relacionados con los datos, como valores fuera de rango o tipos de datos incorrectos.

Ejemplo de manejo de errores:


```python
try:
    cursor.execute("INSERT INTO clientes (id_cliente, nombre) VALUES (1, 'Pedro')")
    conexion.commit()
except sqlite3.IntegrityError:
    print("Error: Clave duplicada")
except sqlite3.Error as e:
    print("Error:", e)
    conexion.rollback()
```

    Error: Clave duplicada


# Integración básica con pandas
Pandas proporciona una forma sencilla de interactuar con bases de datos SQLite utilizando la función `read_sql_query()` para leer datos y el método `to_sql()` para escribir datos.
## Leer datos
El método `read_sql_query()` permite ejecutar una consulta SQL y cargar los resultados directamente en un DataFrame de pandas.


```python
import pandas as pd
dfClientes = pd.read_sql_query("SELECT * FROM clientes", conexion)
print(dfClientes)
```

        id_cliente  nombre apellidos
    0            1    Juan     Perez
    1            2     Ana     Gómez
    2            3   Laura   Ramírez
    3            4  Sergio    Torres
    4            5    Juan     Perez
    5            6     Ana     Gómez
    6            7    Luis    Martín
    7            8    Luis    Martín
    8            9    Juan     Perez
    9           10     Ana     Gómez
    10          11    Luis    Martín
    11          12   María     López
    12          13    Luis  Martínez
    13          14   Marta     López
    14          16   Sofía   Ramírez
    15          17   Diego    Torres
    16          18   Elena      Vega
    17          19  Andrés      Rojo


### Indicar índices al leer datos
Al utilizar `read_sql_query()`, se puede especificar una columna para que actúe como índice del DataFrame utilizando el parámetro `index_col`.


```python
dfClientes = pd.read_sql_query("SELECT * FROM clientes", conexion, index_col="id_cliente")
print(dfClientes)
```

                nombre apellidos
    id_cliente                  
    1             Juan     Perez
    2              Ana     Gómez
    3            Laura   Ramírez
    4           Sergio    Torres
    5             Juan     Perez
    6              Ana     Gómez
    7             Luis    Martín
    8             Luis    Martín
    9             Juan     Perez
    10             Ana     Gómez
    11            Luis    Martín
    12           María     López
    13            Luis  Martínez
    14           Marta     López
    16           Sofía   Ramírez
    17           Diego    Torres
    18           Elena      Vega
    19          Andrés      Rojo
    20           Laura   Ramírez
    21          Sergio    Torres


## Escribir datos
El método `to_sql()` permite escribir un DataFrame de pandas directamente en una tabla de la base de datos SQLite.
Este método recibe como argumentos:
- El nombre de la tabla
- La conexión a la base de datos
- Parámetros opcionales:
  - `if_exists` para especificar qué hacer si la tabla ya existe (por ejemplo, 'fail', 'replace', 'append')
  - `index` para indicar si se debe escribir el índice del DataFrame como una columna separada en la tabla.


```python
df = pd.DataFrame({
    'nombre': ['Laura', 'Sergio'],
    'apellidos': ['Ramírez', 'Torres']
})
df.to_sql('clientes', conexion, if_exists='append', index=False)
```




    2




```python

```
