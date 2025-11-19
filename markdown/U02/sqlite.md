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
conexion = sqlite3.connect("prueba.db")
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

## Uso de cursores para ejecutar consultas SQL
Para ejecutar consultas SQL en SQLite, se utiliza un objeto cursor. El cursor permite ejecutar comandos SQL y recuperar resultados.
### Creación de un cursor
Después de establecer una conexión a la base de datos, se debe crear un cursor utilizando el método `cursor()` de la conexión.Ese cursor actuará como intermediario para ejecutar las consultas SQL.


```python
conexion = sqlite3.connect("empresas.db")
cursor = conexion.cursor()
```

### Ejecución de consultas SQL
Una vez que se tiene un cursor, se pueden ejecutar consultas SQL utilizando el método `execute()` del cursor. Este método recibe como argumento una cadena que contiene la consulta SQL.


```python
cursor.execute("CREATE TABLE IF NOT EXISTS clientes(" +
               "id_cliente INTEGER PRIMARY KEY, "+
               "nombre TEXT, apellidos TEXT)")
```




    <sqlite3.Cursor at 0x224c5f449c0>



La coletilla `IF NOT EXISTS` en la instrucción `CREATE TABLE` asegura que la tabla solo se cree si no existe previamente, evitando errores si se intenta crear una tabla con el mismo nombre.

### Inserción de datos
Después de crear una tabla, se pueden insertar datos utilizando la instrucción `INSERT INTO`.


```python
cursor.execute("INSERT INTO clientes (nombre,apellidos) VALUES ('Juan', 'Perez')")
cursor.execute("INSERT INTO clientes (nombre,apellidos) VALUES ('Ana', 'Gómez')")
```




    <sqlite3.Cursor at 0x224c5f449c0>



Podemos insertar múltiples filas utilizando `executemany()`.


```python
cursor.executemany("INSERT INTO clientes (nombre,apellidos) VALUES (?,?)",
                   [("Luis", "Martínez",),
                    ("Marta", "Reol",),
                    ("Carlos", "Bañes",)])
```




    <sqlite3.Cursor at 0x224c5f449c0>



Esa instrucción utiliza un marcador de posición `?` para los valores que se van a insertar, y una lista de tuplas con los valores correspondientes.

### Modificación de datos
Para modificar datos existentes, se utiliza la instrucción `UPDATE`.


```python
conexion.execute("UPDATE clientes SET apellidos = 'López' WHERE apellidos = 'Reol'")
```




    <sqlite3.Cursor at 0x224ced274c0>



### Eliminación de datos
Para eliminar datos, se utiliza la instrucción `DELETE`.


```python
conexion.execute("DELETE FROM clientes WHERE apellidos = 'Bañes'")
```




    <sqlite3.Cursor at 0x224ced27a40>



## Lectura de datos
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
    (3, 'Luis', 'Martínez')
    (4, 'Marta', 'López')


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
    (3, 'Luis', 'Martínez')
    (4, 'Marta', 'López')


### Iteración directa sobre el cursor
También se puede iterar directamente sobre el cursor después de ejecutar una consulta `SELECT`.


```python
for fila in cursor.execute("SELECT * FROM clientes"):
    print(fila)
```

    (1, 'Juan', 'Perez')
    (2, 'Ana', 'Gómez')
    (3, 'Luis', 'Martínez')
    (4, 'Marta', 'López')


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


## Integración básica con pandas
Pandas proporciona una forma sencilla de interactuar con bases de datos SQLite utilizando la función `read_sql_query()` para leer datos y el método `to_sql()` para escribir datos.
### Leer datos
El método `read_sql_query()` permite ejecutar una consulta SQL y cargar los resultados directamente en un DataFrame de pandas.


```python
import pandas as pd
dfClientes = pd.read_sql_query("SELECT * FROM clientes", conexion)
print(dfClientes)
```

       id_cliente nombre apellidos
    0           1   Juan     Perez
    1           2    Ana     Gómez
    2           3   Luis  Martínez
    3           4  Marta     López


### Escribir datos
El método `to_sql()` permite escribir un DataFrame de pandas directamente en una tabla de la base de datos SQLite.
Este método recibe como argumentos el nombre de la tabla, la conexión a la base de datos, y otros parámetros opcionales como `if_exists` para especificar qué hacer si la tabla ya existe (por ejemplo, 'fail', 'replace', 'append') y el parámetro `index` para indicar si se debe escribir el índice del DataFrame como una columna en la tabla.


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
