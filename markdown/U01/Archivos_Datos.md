```python
# Importar las librerías necesarias, imprescindible para que el código de este cuaderno funcione
import pandas as pd
import numpy as np
from pandas import read_csv
```

# Manejo de archivos de datos
## Introducción
### Fuentes de datos
El trabajo con datos requiere obtener datos por vías externas. Estas vías pueden ser fundamentalmente:
- Archivos de datos locales
- Bases de datos
- Fuentes de datos en la nube

### Lectura de archivos de datos locales
Pandas permite leer archivos de datos en múltiples formatos. Los más comunes son:
- CSV (Comma Separated Values)
- Excel
- JSON (JavaScript Object Notation)
- HDF5 (Hierarchical Data Format)
- Parquet
- SQL (Structured Query Language)

# Archivos CSV
## Lectura de archivos CSV
### Formato CSV
Los archivos CSV son uno de los formatos más comunes para almacenar datos tabulares.

En un archivo CSV, cada línea representa una fila de datos y los valores dentro de cada fila están separados por comas (u otros delimitadores como punto y coma, tabulaciones, etc.).

Puede haber una fila de encabezado al principio del archivo que contiene los nombres de las columnas.

### Instrucción básica para leer archivos CSV
Pandas proporciona la función `read_csv()` para leer archivos CSV y convertirlos en DataFrames de Pandas.


```python
df = pd.read_csv("datos/notas.csv")
print(df.head()) # Muestra las 5 primeras filas
```

       cod_alumno    Nombre y Apellidos  Lenguaje  Matemáticas  Inglés  Ciencias  \
    0      482913      Ana López García         7            8       6         7   
    1      619427     Luis Martín Pérez         5            9       7         6   
    2      735802    María Sánchez Ruiz         8            6       8         9   
    3      582194  Jorge Díaz Hernández         6            7       5         6   
    4      908376    Lucía Gómez Ortega         9            9       9         8   
    
       Sociales  
    0         8  
    1         7  
    2         9  
    3         5  
    4         9  
    

#### Indicar columna como índice
Se puede marcar que una columna específica del archivo CSV debe ser utilizada como índice del DataFrame utilizando el parámetro `index_col`.

Para ello se debe proporcionar el nombre de la columna o su posición (empezando desde 0).


```python
# Indicamos que la primera columna actúa como índice
df = pd.read_csv("datos/notas.csv",index_col=0)
print(df.head())
print("_"*40)
# Lo hacemos ahora por el nombre de la columna
df = pd.read_csv("datos/notas.csv",index_col='cod_alumno')
print(df.head())
```

                  Nombre y Apellidos  Lenguaje  Matemáticas  Inglés  Ciencias  \
    cod_alumno                                                                  
    482913          Ana López García         7            8       6         7   
    619427         Luis Martín Pérez         5            9       7         6   
    735802        María Sánchez Ruiz         8            6       8         9   
    582194      Jorge Díaz Hernández         6            7       5         6   
    908376        Lucía Gómez Ortega         9            9       9         8   
    
                Sociales  
    cod_alumno            
    482913             8  
    619427             7  
    735802             9  
    582194             5  
    908376             9  
    ________________________________________
                  Nombre y Apellidos  Lenguaje  Matemáticas  Inglés  Ciencias  \
    cod_alumno                                                                  
    482913          Ana López García         7            8       6         7   
    619427         Luis Martín Pérez         5            9       7         6   
    735802        María Sánchez Ruiz         8            6       8         9   
    582194      Jorge Díaz Hernández         6            7       5         6   
    908376        Lucía Gómez Ortega         9            9       9         8   
    
                Sociales  
    cod_alumno            
    482913             8  
    619427             7  
    735802             9  
    582194             5  
    908376             9  
    

#### Leer columnas concretas
Se puede seleccionar un subconjunto de columnas para leer utilizando el parámetro `usecols`, proporcionando una lista con los nombres o posiciones de las columnas a leer.


```python
# usamos el nombre de las columnas
df = pd.read_csv("datos/notas.csv",usecols=['cod_alumno','Nombre y Apellidos','Sociales'],index_col='cod_alumno')
print(df.head())
```

                  Nombre y Apellidos  Sociales
    cod_alumno                                
    482913          Ana López García         8
    619427         Luis Martín Pérez         7
    735802        María Sánchez Ruiz         9
    582194      Jorge Díaz Hernández         5
    908376        Lucía Gómez Ortega         9
    


```python
# usamos el número de las columnas
df = pd.read_csv("datos/notas.csv",usecols=[0,1,6],index_col='cod_alumno')
print(df.head())
```

                  Nombre y Apellidos  Sociales
    cod_alumno                                
    482913          Ana López García         8
    619427         Luis Martín Pérez         7
    735802        María Sánchez Ruiz         9
    582194      Jorge Díaz Hernández         5
    908376        Lucía Gómez Ortega         9
    

#### Modificar el delimitador
Si el archivo CSV utiliza un delimitador diferente a la coma, se puede especificar utilizando el parámetro `delimiter` o `sep`.


```python
# Leer un archivo CSV con punto y coma como delimitador
df = pd.read_csv('datos/vino-corta.csv', delimiter=";")
print(df)
```

          País   Vino  Aceite de oliva (virgen) Trigo  Unnamed: 4
    0   España   3780                      3147  62,5         NaN
    1   Italia   8730                      1886  75,7         NaN
    2   Grecia   99,4                      1151   232         NaN
    3  Francia  13600                        90   301         NaN
    

#### Determinar la fila de cabecera
Por defecto Pandas asume que la primera fila del archivo CSV contiene los nombres de las columnas. Si los nombres de las columnas están en una fila diferente, se puede especificar utilizando el parámetro `header`.

Si no hay ninguna fila de cabecera, entonces se indica el valor `None`. En ese caso la cabecera de columna utilizará números del 0 en adelante


```python
# Leer datos sin cabecera
df = pd.read_csv("datos/notas-sin-cab.csv",header=None,index_col=0)
print(df.head())
```

                               1  2  3  4  5  6
    0                                          
    482913      Ana López García  7  8  6  7  8
    619427     Luis Martín Pérez  5  9  7  6  7
    735802    María Sánchez Ruiz  8  6  8  9  9
    582194  Jorge Díaz Hernández  6  7  5  6  5
    908376    Lucía Gómez Ortega  9  9  9  8  9
    

#### Parámetro `dtype`
Se puede especificar el tipo de datos de las columnas utilizando el parámetro `dtype`, proporcionando un diccionario donde las claves son los nombres de las columnas y los valores son los tipos de datos deseados.

Si en lugar de un diccionario se proporciona un solo tipo de dato, ese tipo se aplicará a todas las columnas.


```python
# leemos todos los datos como si fueran texto, no podremos hacer
# operaciones numéricas directamente
df = pd.read_csv("datos/notas.csv",dtype='str',index_col='cod_alumno')
print(df.head())
```

                  Nombre y Apellidos Lenguaje Matemáticas Inglés Ciencias Sociales
    cod_alumno                                                                    
    482913          Ana López García        7           8      6        7        8
    619427         Luis Martín Pérez        5           9      7        6        7
    735802        María Sánchez Ruiz        8           6      8        9        9
    582194      Jorge Díaz Hernández        6           7      5        6        5
    908376        Lucía Gómez Ortega        9           9      9        8        9
    


```python
# Leemos especificando los tipos de cada columna
dtype_dict = {
    'Nombre y Apellidos': 'str',
    'Lenguaje': 'int8',
    'Matemáticas': 'int8',
    'Inglés': 'int8',
    'Sociales': 'int8',
    'Ciencias': 'int8'
}
df = pd.read_csv("datos/notas.csv",dtype=dtype_dict,index_col='cod_alumno')
print(df.head())
```

                  Nombre y Apellidos  Lenguaje  Matemáticas  Inglés  Ciencias  \
    cod_alumno                                                                  
    482913          Ana López García         7            8       6         7   
    619427         Luis Martín Pérez         5            9       7         6   
    735802        María Sánchez Ruiz         8            6       8         9   
    582194      Jorge Díaz Hernández         6            7       5         6   
    908376        Lucía Gómez Ortega         9            9       9         8   
    
                Sociales  
    cod_alumno            
    482913             8  
    619427             7  
    735802             9  
    582194             5  
    908376             9  
    

## Escritura de archivos CSV a partir de un DataFrame
Pandas proporciona la función `to_csv()` para escribir un DataFrame en un archivo CSV.



```python
df = pd.DataFrame ({
    'Nombre': ['Ana', 'Luis', 'María','Pedro','Sofía'],
    'Edad': [23, 34, 29, 45, 31],
    'Ciudad': ['Madrid', 'Valladolid', 'Zaragoza', 'Valladolid', 'Zaragoza']
})
# Escribir el DataFrame en un archivo CSV
df.to_csv('datos/alumnos_back.csv', index=False)
```

### Parámetros comunes de `to_csv()`
- `sep`: Especifica el carácter delimitador utilizado para separar los valores (por defecto es una coma).
- `index`: Valor booleano que indica si se debe escribir el índice del DataFrame en el archivo CSV (por defecto es `True`).
- `header`: Valor booleano que indica si se deben escribir los nombres de las columnas en el archivo CSV (por defecto es `True`).
- `columns`: Permite indicar la lista de columnas concretas que se desean escribir en el archivo CSV.
- `mode`: Especifica el modo de apertura del archivo (por defecto es `'w'` para escritura). Se puede usar `'a'` para añadir datos al final del archivo existente.
- `encoding`: Permite especificar la codificación del archivo (por ejemplo, `'utf-8'`, `'latin-1'`, etc.). Por defecto es `'utf-8'`.
- `na_rep`: Permite especificar una cadena que se utilizará para representar los valores faltantes (NaN) en el archivo CSV.
- `float_format`: Permite especificar el formato para los números de punto flotante (por ejemplo, `'%.2f'` para dos decimales).


```python
codAlumnos = pd.Index(['A001','A002','A003','A004','A005'], name='cod_alumno')
df = pd.DataFrame ({
    'Nombre': ['Ana', 'Luis', 'María','Pedro','Sofía'],
    'Edad': [23, 34, 29, 45, 31],
    'Ciudad': ['Madrid', 'Valladolid', 'Zaragoza', 'Valladolid', 'Zaragoza']
},index=codAlumnos)
# Escribir el DataFrame en un archivo CSV con parámetros adicionales
df.to_csv('datos/alumnos_back2.csv', index=True, sep=';', encoding='utf-8')
df2 = pd.read_csv('datos/alumnos_back2.csv',delimiter=';',index_col='cod_alumno')
print(df2)
```

               Nombre  Edad      Ciudad
    cod_alumno                         
    A001          Ana    23      Madrid
    A002         Luis    34  Valladolid
    A003        María    29    Zaragoza
    A004        Pedro    45  Valladolid
    A005        Sofía    31    Zaragoza
    

# Archivos Excel
## Lectura de archivos Excel
### Sobre Excel
Microsoft Excel es una aplicación de hoja de cálculo ampliamente utilizada para almacenar y analizar datos tabulares. Los archivos de Excel pueden tener extensiones `.xls` (formato de las versiones anteriores a la 2000) y `.xlsx` (formato moderno).

Para poder trabajar con archivos de Excel modernos, necesitamos instalar la librería `openpyxl`. Esto se puede hacer ejecutando el siguiente comando en la terminal o en una celda del cuaderno Jupyter:
```
pip install openpyxl
```

o bien desde un entorno de desarrollo como Anaconda:
```
conda install openpyxl
```

En el caso de utilizar un cuderno Jupyter, se puede ejecutar el siguiente comando en una celda:
```python
!pip install openpyxl
```



```python
# Instala el módulo openpyxl si no está ya instalado
!pip install openpyxl
```

    Requirement already satisfied: openpyxl in /opt/miniconda3/envs/ApuntesADPy/lib/python3.13/site-packages (3.1.5)
    Requirement already satisfied: et-xmlfile in /opt/miniconda3/envs/ApuntesADPy/lib/python3.13/site-packages (from openpyxl) (2.0.0)
    
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m A new release of pip is available: [0m[31;49m24.3.1[0m[39;49m -> [0m[32;49m25.3[0m
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m To update, run: [0m[32;49mpip install --upgrade pip[0m


### Instrucción básica para leer archivos Excel
Pandas proporciona la función `read_excel()` para leer archivos de Excel y convertirlos en DataFrames de Pandas.


```python
# Leer un archivo Excel
df = pd.read_excel("datos/vino-corta.xlsx",engine='openpyxl')
print(df)
```

          País     Vino  Aceite de oliva (virgen)  Trigo
    0   España   3780.0                      3147   62.5
    1   Italia   8730.0                      1886   75.7
    2   Grecia     99.4                      1151  232.0
    3  Francia  13600.0                        90  301.0
    

### Parámetros comunes de `read_excel()`
- `sheet_name`: Permite especificar el nombre o el índice de la hoja de cálculo que se desea leer. Por defecto, se lee la primera hoja.
- `header`: Permite especificar la fila que contiene los nombres de las columnas. Por defecto es 0 (la primera fila).
- `index_col`: Permite especificar la columna que se utilizará como índice del DataFrame.
- `usecols`: Permite seleccionar un subconjunto de columnas para leer.
- `dtype`: Permite especificar el tipo de datos de las columnas.
- `skiprows`: Permite omitir un número específico de filas al principio del archivo.
- `nrows`: Permite leer un número específico de filas desde el principio del archivo.
- `na_values`: Permite especificar valores adicionales que deben ser considerados como NaN (valores faltantes).
- `converters`: Permite especificar funciones de conversión para columnas específicas.
- `engine`: Permite especificar el motor a utilizar para leer el archivo de Excel (por ejemplo, `openpyxl` para archivos `.xlsx`).
- `parse_dates`: Permite especificar columnas que deben ser interpretadas como fechas.


```python
df = pd.read_excel('datos/notas.xlsx',
                   skiprows=5,           # Saltar las primeras 5 filas, (la cabecera está en la sexta)
                   usecols='D:K',
                   index_col='Cod_Alumno')       # Leer solo las columnas D a K
print(df.head())
```

               Nombre        Apellidos  Lenguaje  Matemáticas  Inglés  Ciencias  \
    Cod_Alumno                                                                    
    A203        Lucía   Fernández Ruiz       8.3          7.5     6.9       7.8   
    A204        Mario    Sánchez Gómez       7.1          6.8     7.9       8.2   
    A205        Paula  Rodríguez López       9.2          7.7     8.5       9.0   
    A206         Hugo    Martín García       6.4          8.3     5.7       7.2   
    A207         Alba       Pérez Díaz       7.5          8.0     7.3       6.9   
    
                Sociales  
    Cod_Alumno            
    A203             8.0  
    A204             6.5  
    A205             8.8  
    A206             7.5  
    A207             8.1  
    

## Escribir archivos Excel a partir de un DataFrame
Pandas proporciona la función `to_excel()` para escribir un DataFrame en un archivo Excel.


```python
# Escribir un DataFrame en un archivo Excel
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'María','Pedro','Sofía'],
    'Edad': [23, 34, 29, 45, 31],
    'Ciudad': ['Madrid', 'Valladolid', 'Zaragoza', 'Valladolid', 'Zaragoza']})
df.to_excel('datos/alumnos_back.xlsx', index=False, engine='openpyxl')
```

## Parámetros comunes de `to_excel()`
- `sheet_name`: Permite especificar el nombre de la hoja de cálculo donde se escribirán los datos. Por defecto es `'Sheet1'`.
- `index`: Valor booleano que indica si se debe escribir el índice del DataFrame en el archivo Excel (por defecto es `True`).
- `header`: Valor booleano que indica si se deben escribir los nombres de las columnas en el archivo Excel (por defecto es `True`).
- `columns`: Permite indicar la lista de columnas concretas que se desean escribir en el archivo Excel.
- `engine`: Permite especificar el motor a utilizar para escribir el archivo de Excel (por ejemplo, `openpyxl` para archivos `.xlsx`).
- `startrow` y `startcol`: Permiten especificar la fila y columna inicial donde se comenzarán a escribir los datos en la hoja de cálculo.
- `na_rep`: Permite especificar una cadena que se utilizará para representar los valores faltantes (NaN) en el archivo Excel.
- `float_format`: Permite especificar el formato para los números de punto flotante (por ejemplo, `'%.2f'` para dos decimales).


```python
df = pd.DataFrame ({
    'Nombre': ['Ana', 'Luis', 'María','Pedro','Sofía'],
    'Edad': [23, 34, 29, 45, 31],
    'Ciudad': ['Madrid', 'Valladolid', 'Zaragoza', 'Valladolid', 'Zaragoza']
})
# Escribir el DataFrame en un archivo Excel con parámetros adicionales
df.to_excel('datos/alumnos_back2.xlsx', index=False, sheet_name='Alumnos', engine='openpyxl', startrow=2, startcol=4)
```

# Archivos JSON
## Introducción
JSON (JavaScript Object Notation) es un formato ligero de intercambio de datos que es fácil de leer y escribir para los humanos, y fácil de parsear y generar para las máquinas. Es ampliamente utilizado para almacenar y transmitir datos estructurados.
Los datos en formato JSON se representan como pares clave-valor, donde las claves son cadenas y los valores pueden ser de varios tipos, incluyendo números, cadenas, booleanos, arreglos y objetos anidados.
Por ejemplo:
```json
{
    "nombre": "Juan",
    "edad": 30,
    "ciudad": "Madrid",
    "hobbies": ["fútbol", "lectura", "viajar"]
}
```
Los archivos JSON pueden comenzar con los siguientes tipos de estructuras:
- Objeto JSON: Comienza con una llave `{` y termina con una llave `}`
- Array JSON: Comienza con un corchete `[` y termina con un corchete `]`
- Valor JSON simple: Puede ser una cadena, número, booleano, nulo, etc (aunque no es común que un archivo JSON contenga solo un valor simple)

## Lectura de archivos JSON
### Instrucción básica para leer archivos JSON
Pandas proporciona la función `read_json()` para leer archivos JSON y convertirlos en DataFrames de Pandas.


```python
# Leer un archivo JSON
df = pd.read_json("datos/alumnos.json")
print(df)
```

          nombre        apellidos codigo  matematicas  lengua  ingles
    0        Ana     García López   A001            8       7       9
    1       Luis   Martínez Pérez   A002            6       8       7
    2      María     Sánchez Ruiz   A003            9       9       8
    3     Carlos  Fernández Gómez   A004            5       6       6
    4      Lucía      Romero Díaz   A005           10       9      10
    5      Jorge   Vargas Morales   A006            7       5       6
    6      Sofía    Núñez Herrera   A007            8       8       9
    7      Pablo   Ortiz Castillo   A008            4       6       5
    8      Elena     Prieto Ramos   A009            9      10       9
    9     Miguel      Blanco Soto   A010            6       7       6
    10    Carmen      Ibáñez Cruz   A011            7       9       8
    11    Daniel   Molina Fuentes   A012            5       4       6
    12    Isabel       Marín Peña   A013            8       8       7
    13      Raúl     Cordero Vega   A014            3       5       4
    14    Noelia   Caballero León   A015           10       9      10
    15   Alberto    Rivas Aguilar   A016            6       6       7
    16     Paula     Solana Muñoz   A017            9       8       8
    17    Víctor   Gallego Campos   A018            7       6       5
    18  Verónica   Herrera Lozano   A019            8      10       9
    19     Diego    Paredes Rubio   A020            5       7       6
    

### Parámetro orient
Indica la estructura esperada del JSON. Puede ser:
- `'split'`: El JSON contiene tres claves:`index`, `columns` y `data`.
Ejemplo:


```python
""" La estructura del archivo es esta:
{
    "index": [0, 1, 2],
    "columns": ["Nombre", "Apellido", "Edad"],
    "data": [
        ["Ana", "García", 23],
        ["Luis", "Martínez", 34],
        ["María", "López", 29]
    ]
}"""
df = pd.read_json("datos/datos_split.json",orient='split')
print(df)
```

      Nombre  Apellido  Edad
    0    Ana    García    23
    1   Luis  Martínez    34
    2  María     López    29
    


- `'records'`: El archivo JSON consta de un array de objetos. Es el formato habitual de un archivo JSON. Los nombres de las propiedades se obtienen de las propiedades de los objetos. Ejemplo:


```python
""" El archivo está en este formato
[
    {"Nombre": "Ana", "Apellido": "García", "Edad": 23},
    {"Nombre": "Luis", "Apellido": "Martínez", "Edad": 34},
    {"Nombre": "María", "Apellido": "López", "Edad": 29}
]
"""
df = pd.read_json("datos/datos_records.json",orient='records')
print(df)
```


 - `'index'`: El archivo JSON contiene un objeto cuyas propiedades son las claves de los índices y cada valor contiene una estructura tipo diccionario con pares columna/valor. Cada clave de índice formará una fila distinta. Ejemplo:


```python
""" El archivo está en este formato
{
    "0": {"Nombre": "Ana", "Apellido": "García", "Edad": 23},
    "1": {"Nombre": "Luis", "Apellido": "Martínez", "Edad": 34},
    "2": {"Nombre": "María", "Apellido": "López", "Edad": 29}
}
"""
df = pd.read_json("datos/datos_index.json",orient='index')
print(df)
```

      Nombre  Apellido  Edad
    0    Ana    García    23
    1   Luis  Martínez    34
    2  María     López    29
    


- `'columns'`: El archivo JSON contiene un objeto que forma un diccionario de listas, donde las claves son los nombres de las columnas. Es el valor por defecto. Ejemplo:
```json

```


```python
""" El archivo está en este formato
{
    "Nombre": ["Ana", "Luis", "María"],
    "Apellido": ["García", "Martínez", "López"],
    "Edad": [23, 34, 29]
}
"""
df = pd.read_json("datos/datos_columns.json",orient='columns')
print(df)
```

      Nombre  Apellido  Edad
    0    Ana    García    23
    1   Luis  Martínez    34
    2  María     López    29
    



- `'values'`: El JSON es una lista de listas, donde cada lista representa una fila. Ejemplo:
```json
[
    ["Ana", "García", 23],
    ["Luis", "Martínez", 34],
    ["María", "López", 29]
]
```



```python

```

### Otros parámetros comunes de `read_json()`

- `typ`. Permite especificar el tipo de objeto a devolver. Puede ser `'frame'` (DataFrame, valor por defecto) o `'series'` (Series). En el caso de que el valor sea `'series'`, se devuelve un objeto Series de Pandas. Solo es apto si el JSON representa una estructura compatible con una Serie de Pandas. Con valor `'series'`el valor por defecto de `'orientation'` es index, se entiende que los datos tienen como vlave el índice de cada fila. Ejemplo:


```python
"""" El archivo está en este formato
{
    "ID1": "Juan",
    "ID2": "Maria",
    "ID3": "Carlos",
    "ID4": "Luisa"
}
"""
serie = pd.read_json("datos/datos_col.json",typ='series')
print(serie)
```

    ID1      Juan
    ID2     Maria
    ID3    Carlos
    ID4     Luisa
    dtype: object
    


- `dtype`: Permite especificar el tipo de datos de las columnas.
- `convert_axes`: Valor booleano que indica si se deben convertir los ejes (índices y columnas) a sus tipos originales (por defecto es `True`).
- `convert_dates`: Permite especificar columnas que deben ser interpretadas como fechas.
- `lines`: Valor booleano que indica si el archivo JSON contiene múltiples líneas, cada una representando un objeto JSON separado (por defecto es `False`).


## Escritura de archivos JSON a partir de un DataFrame
Pandas proporciona la función `to_json()` para escribir un DataFrame en un archivo JSON.


```python
df = pd.DataFrame ({
    'Nombre': ['Ana', 'Luis', 'María','Pedro','Sofía'],
    'Edad': [23, 34, 29, 45, 31],
    'Ciudad': ['Madrid', 'Valladolid', 'Zaragoza', 'Valladolid', 'Zaragoza']
})
# Escribir el DataFrame en un archivo JSON
df.to_json('datos/alumnos_back.json', force_ascii=False)
```

El archivo JSOn resultante tendrá el siguiente formato (orientación por defecto 'columns'):
```json
{
  "Nombre": {
    "0": "Ana",
    "1": "Luis",
    "2": "María",
    "3": "Pedro",
    "4": "Sofía"
  },
  "Edad": {
    "0": 23,
    "1": 34,
    "2": 29,
    "3": 45,
    "4": 31
  },
  "Ciudad": {
    "0": "Madrid",
    "1": "Valladolid",
    "2": "Zaragoza",
    "3": "Valladolid",
    "4": "Zaragoza"
  }
}
```
Correspondiente a la orientación 'index'. Además, en realidad no se mostraría con indentaciones, sino en una sola línea (bse ha expuesto así para facilitar su lectura).

### Parámetros comunes de `to_json()`
- `force_ascii`: Valor booleano que indica si se deben forzar los caracteres ASCII en el archivo JSON (por defecto es `True` y no guardaría los caracteres en formato Unicode).
`orient`: Permite especificar la estructura del JSON resultante. imos sus posibilidades en el apartado anterior`
- `date_format`: Permite especificar el formato para las fechas (por ejemplo, `'iso' para formato ISO 8601).
- `double_precision`: Permite especificar el número de decimales para los números de punto flotante.
- `lines`: Valor booleano que indica si se debe escribir el archivo JSON en múltiples líneas, cada una representando un objeto JSON separado (por defecto es `False`).
- `indent`: Permite especificar el número de espacios para la indentación del archivo JSON. Por defecto es `None` (sin indentación).



```python
df = pd.DataFrame ({
    'Nombre': ['Ana', 'Luis', 'María','Pedro','Sofía'],
    'Edad': [23, 34, 29, 45, 31],
    'Ciudad': ['Madrid', 'Valladolid', 'Zaragoza', 'Valladolid', 'Zaragoza']
})
# Escribir el DataFrame en un archivo JSON con parámetros adicionales
df.to_json('datos/alumnos_back2.json', orient='records', force_ascii=False, indent=4)
```

El archivo JSON resultante tendrá el siguiente formato:
```json
[
    {
        "Nombre": "Ana",
        "Edad": 23,
        "Ciudad": "Madrid"
    },
    {
        "Nombre": "Luis",
        "Edad": 34,
        "Ciudad": "Valladolid"
    },
    {
        "Nombre": "María",
        "Edad": 29,
        "Ciudad": "Zaragoza"
    },
    {
        "Nombre": "Pedro",
        "Edad": 45,
        "Ciudad": "Valladolid"
    },
    {
        "Nombre": "Sofía",
        "Edad": 31,
        "Ciudad": "Zaragoza"
    }
]
```
