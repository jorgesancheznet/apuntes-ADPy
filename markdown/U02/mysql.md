# Uso de MySQL
## Índice
- [Características principales](#características-principales)
- [Instalación de MySQL](#instalación-de-mysql)
  - [Descarga](#descarga)
  - [Instalación de la versión ZIP](#instalación-de-la-versión-zip)
  - [Conectar con MySQL](#conectar-con-mysql)
  - [Crear usuarios](#crear-usuarios)
- [Librerías de Python para MySQL](#librerías-de-python-para-mysql)
- [Conexión con MySQL desde Python](#conexión-con-mysql-desde-python)
  - [Ejecución de instrucciones](#ejecución-de-instrucciones)


## Características principales
MySQL es un Sistema Gestor de Bases de Datos completo. Es uno de los más utilizados en el mundo del desarrollo de aplicaciones por su versatilidad, velocidad y facilidad de aprendizaje.

Se trata de un software multiplataforma, creado en 1995 con **licencia de software libre** y gratuita, lo que le ha hecho muy popular en entornos educativos y profesionales.

Es un sistema de bases de datos relacionales que utiliza **SQL** como lenguaje de trabajo (aunque hay diferencias entre su versión SQL y el estándar).

Posee compatibilidad con transacciones (si se usan motores compatibles, como **InnoDB**) y aporta capacidad de trabajar en modo distribuido.

## Instalación de MySQL
### Descarga
MySQL se debe de descargar desde la página oficial de la versión **Community**, que es la versión gratuita y sin soporte. Esta página está disponible en [https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

Desde ahí elegimos la versión y descargamos el instalador apropiado. En Windows, si no somos administradores, deberemos descargar la versión ZIP.

### Instalación de la versión ZIP
1. Debemos descargar la instalación en formato ZIP y descomprimir el paquete. Después podemos moverlo a nuestra ubicación deseada.
2. Debemos añadir la ruta al directorio `bin` al PATh del sistema.
3. Debemos crear una carpeta llamada `data`en la raíz de MySQL
4. Debemos crear el archivo de configuración `my.ini`en la raíz de MySQL, con este contenido:
```
[mysqld]
basedir = "directorio_raíz_de_MySQL"
datadir = "directorio_raíz_de_MySQL/data"
port = 3306
character-set-server=utf8mb4
```
5.Lanzamos MySQL con el comando:

```
mysqld --defaults-file="ruta_a_my.ini" --initilize-insecure --console
```

6. Luego bastará ejecutar:
```
msqld --console
```

### Conectar con MySQL
Cuando se crea MySQL con contraseña insegura se accede con:

```
mysql -u root
```

Aparece el prompt `mysql>`en el que podremos ejecutar comandos SQL

### Crear usuarios
Ejemplo:
```
CREATE USER prueba@localhost IDENTIFIED BY '12345';
CREATE DATABASE prueba;
GRANT ALL ON prueba.* TO prueba@localhost;
FLUSH PRIVILEGES;
```
Con esto se crea un usuario local llamado prueba que puede conectar y hacer lo que quiera con la base de datos que hemos creado y que también se llama prueba.

Para conectar con ese usuario se escribe en la consola:
```
mysql -u prueba -p
```
Y después escribiremos la contraseña

## Librerías de Python para MySQL
En análisis de datos se utiliza principalmente `pandas` para cargar datos desde MySQL, pero existen otras librerías que permiten conectar con MySQL desde Python. Pero se usan también librerías de Python para gestionar las conexiones.

En todo caso las librerías más utilizadas son:
* `mysql-connector-python`: Librería oficial de MySQL para Python. Permite conectar y ejecutar consultas SQL.
* `PyMySQL`: Librería pura de Python para conectar con MySQL. Es fácil de usar y no requiere dependencias externas.
* `SQLAlchemy`: Librería ORM que soporta MySQL. Permite trabajar con bases de datos de forma más abstracta y orientada a objetos.

Estas tres librerías se deben instala mediante `pip` o bien instalarse en un entorno virtual generado por `conda`.

Lo normal para usar `pandas`con MySQL es utilizar `SQLAlchemy` y `PyMySQL` porque `pandas` no tiene soporte nativo para MySQL.

## Conexión con MySQL desde Python
Necesiotamos importar la librería `pymysql` y utilizar el método `connect`. Este método requiere estos parámetros:
* **host**. Que sirve para indicar el nombre del servidor donde está la base de datos. Si es local se indica `localhost`.
* **user**. Nombre del usuario con el que se conecta a la base de datos.
* **password**. Contraseña del usuario.
* **database**. Nombre de la base de datos a la que se conecta.
* **port**. Puerto de conexión. Por defecto es el 3306.

Ejemplo de conexión con PyMySQL


```python
import pymysql
# Hay que usar el usuario y contraseña dsel que dispongamos en MySQL
connection = pymysql.connect(host='localhost', user='prueba`', password='A12345', database='prueba')
```


### Ejecución de instrucciones
Se realiza creando un cursor y utilizando el método `execute` del cursor. Por ejemplo:


```python
# Hay que usar las tablas que tengamos en MySQL
cursor = connection.cursor()
cursor.execute("SELECT * FROM tabla")
results = cursor.fetchall()
for row in results:
    print(row)
```
