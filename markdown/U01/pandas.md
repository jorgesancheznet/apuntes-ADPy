# Pandas
## Contenido
# Índice

- [Contenido](#Contenido)

- [Introducción a la librería pandas](#Introducción-a-la-librería-pandas)
  - [Importación de la librería](#Importación-de-la-librería)

- [Creación de Series](#Creación-de-Series)
  - [¿Qué es una Serie?](#¿Qué-es-una-Serie?)
  - [Creación de una Serie a partir de una colección unidimensional de datos](#Creación-de-una-Serie-a-partir-de-una-colección-unidimensional-de-datos)
  - [Modificar índices durante la creación de una Serie](#Modificar-índices-durante-la-creación-de-una-Serie)
  - [Creación de una Serie a partir de un diccionario](#Creación-de-una-Serie-a-partir-de-un-diccionario)
  - [Creación de una Serie a partir de un valor escalar](#Creación-de-una-Serie-a-partir-de-un-valor-escalar)

- [Creación de DataFrames](#Creación-de-DataFrames)
  - [¿Qué es un DataFrame?](#¿Qué-es-un-DataFrame?)
  - [Creación de un DataFrame a partir de un diccionario](#Creación-de-un-DataFrame-a-partir-de-un-diccionario)
  - [Creación de un DataFrame a partir de varias listas](#Creación-de-un-DataFrame-a-partir-de-varias-listas)
  - [Creación de un DataFrame a partir de arrays de NumPy](#Creación-de-un-DataFrame-a-partir-de-arrays-de-NumPy)
  - [Creación de un DataFrame a partir de una lista de listas](#Creación-de-un-DataFrame-a-partir-de-una-lista-de-listas)
  - [Creación de un DataFrame utilizando diccionarios anidados](#Creación-de-un-DataFrame-utilizando-diccionarios-anidados)

- [Creación de Índices](#Creación-de-Índices)
  - [¿Qué es un índice?](#¿Qué-es-un-índice?)
  - [Creación de índices personalizados](#Creación-de-índices-personalizados)

- [Mostrar solo algunos datos de DataFrames y Series](#Mostrar-solo-algunos-datos-de-DataFrames-y-Series)

- [Propiedades de las Series y los DataFrames](#Propiedades-de-las-Series-y-los-DataFrames)
  - [Propiedad values](#Propiedad-values)
  - [Propiedad dtype](#Propiedad-dtype)
  - [Propiedad size](#Propiedad-size)
  - [Propiedad name](#Propiedad-name)
  - [Propiedad shape](#Propiedad-shape)
  - [Propiedad index](#Propiedad-index)
  - [Propiedad columns](#Propiedad-columns)
  - [Función len](#Función-len)

- [Selección de datos](#Selección-de-datos)
  - [Acceso a un elemento de una serie](#Acceso-a-un-elemento-de-una-serie)
  - [Indexaciones de series](#Indexaciones-de-series)
  - [Obtener columnas de un DataFrame en forma de Serie](#Obtener-columnas-de-un-DataFrame-en-forma-de-Serie)
  - [Obtener varias columnas de un DataFrame](#Obtener-varias-columnas-de-un-DataFrame)
  - [Acceso a filas de un DataFrame](#Acceso-a-filas-de-un-DataFrame)
  - [Acceso a filas y columnas con loc[]](#Acceso-a-filas-y-columnas-con-loc[])
  - [Acceso por posición con iloc[]](#Acceso-por-posición-con-iloc[])

- [Filtrar datos en un DataFrame](#Filtrar-datos-en-un-DataFrame)
  - [Filtrado lógico](#Filtrado-lógico)
  - [Método filter()](#Método-filter())
  - [Filtrado por tipo de datos](#Filtrado-por-tipo-de-datos)
  - [Filtrado con arrays booleanos](#Filtrado-con-arrays-booleanos)

- [Operar con DataFrames](#Operar-con-DataFrames)
  - [Eliminar columnas](#Eliminar-columnas)
  - [Añadir columnas a DataFrames](#Añadir-columnas-a-DataFrames)
  - [Eliminar filas](#Eliminar-filas)
  - [Trasponer un DataFrame](#Trasponer-un-DataFrame)
  - [Operaciones matemáticas](#Operaciones-matemáticas)
  - [Usar cálculos de totales](#Usar-cálculos-de-totales)
  - [Método **agg**](#Método-**agg**)
  - [Uso de funciones **callback** para cálculos de totales](#Uso-de-funciones-**callback**-para-cálculos-de-totales)
  - [Trasformaciones](#Trasformaciones)
  - [Método `map()`](#Método-`map()`)
  - [Método `unique()`](#Método-`unique()`)
  - [Método `value_counts()`](#Método-`value_counts()`)
  - [Método `describe()`](#Método-`describe()`)
  - [Método `astype()`](#Método-`astype()`)
  - [Método `sort_values()`](#Método-`sort_values()`)

- [Obtener información del DataFrame](#Obtener-información-del-DataFrame)
  - [Método info()](#Método-info())
  - [Propiedad columns](#Propiedad-columns)
  - [Propiedad shape](#Propiedad-shape)
  - [Propiedad dtypes](#Propiedad-dtypes)
  - [Propiedad index](#Propiedad-index)

## Introducción a la librería pandas
La librería pandas es una de las herramientas más poderosas y populares en Python para el análisis y manipulación de datos. La palabra "pandas" proviene de "panel data", que se refiere a conjuntos de datos multidimensionales. Pandas proporciona estructuras de datos flexibles y fáciles de usar. Concretamente sus estructuras son:
* **Series**. Es una estructura de datos unidimensional que puede almacenar datos de diferentes tipos (como enteros, cadenas, flotantes, etc.) y se utiliza para representar una sola columna o fila de datos.
* **DataFrame**.  Se trata de una estructura de datos bidimensional, similar a una tabla, que permite almacenar y manipular datos de manera eficiente.

* **Índice**. Es una estructura que se utiliza para etiquetar y organizar los datos en pandas, permitiendo un acceso rápido y eficiente a los datos.


### Importación de la librería
Para que funcione pandas, primero debemos importarla en nuestro entorno de trabajo. La convención común es importar pandas con el alias **pd**.
El código siguiente es imprescindible para comenzar a trabajar con pandas y, en el caso de este documento, para poder ejecutar las celdas que contienen código relacionado con pandas.


```python
import pandas as pd
import numpy as np ## Librería necesaria para crear arrays de NumPy
```

## Creación de Series
### ¿Qué es una Serie?
Se trata de la estructura básica para contener datos en pandas. Una Serie es una estructura de datos unidimensional cuyos datos están emparejados con un índice, que permite acceder a los datos de manera eficiente.

Cada elemento de una Serie tiene un valor y un índice asociado. El índice puede ser numérico (por defecto) o puede ser de otro tipo constituyendo etiquetas.

Las Series son similares a los arrays de NumPy, pero con funcionalidades adicionales proporcionadas por pandas, como la capacidad de manejar datos faltantes y realizar operaciones aritméticas y estadísticas de manera más sencilla.

### Creación de una Serie a partir de una colección unidimensional de datos
Podemos crear una Serie a partir de diversas fuentes, como listas, diccionarios, arrays de NumPy, entre otras posibilidades.

El método fundamental para crear series es `pd.Series()` el cual puede recibir como argumento una colección de valores, la cual puede estar contenida en una lista, un diccionario, un array de NumPy, etc.


```python
# Creación a partir de una lista
serie = pd.Series([10, 20, 30, 40, 50])
print("Serie a partir de una lista:\n",serie)
# Creación a partir de una tupla
serie = pd.Series((10, 20, 30, 40, 50))
print("\nSerie a partir de una tupla:\n",serie)
# Serie a partir de un rango
serie = pd.Series(range(10, 60, 10))
print("\nSerie a partir de un rango:\n",serie)
# Serie a partir de un array de NumPy
a = np.array([10, 20, 30, 40, 50])
serie = pd.Series(a)
print("\nSerie a partir de un array de NumPy:\n",serie)
```

    Serie a partir de una lista:
     0    10
    1    20
    2    30
    3    40
    4    50
    dtype: int64
    
    Serie a partir de una tupla:
     0    10
    1    20
    2    30
    3    40
    4    50
    dtype: int64
    
    Serie a partir de un rango:
     0    10
    1    20
    2    30
    3    40
    4    50
    dtype: int64
    
    Serie a partir de un array de NumPy:
     0    10
    1    20
    2    30
    3    40
    4    50
    dtype: int64
    

En todos los casos podemos especificar el tipo de dato de los elementos de la Serie utilizando el parámetro `dtype`.


```python
serie = pd.Series(range(1,11), dtype="float64")
print(serie)
```

    0     1.0
    1     2.0
    2     3.0
    3     4.0
    4     5.0
    5     6.0
    6     7.0
    7     8.0
    8     9.0
    9    10.0
    dtype: float64
    

### Modificar índices durante la creación de una Serie
Por defecto cada elemento de la Serie recibe un índice numérico que comienza en 0.
Podemos cambiar el índice especificando una lista de etiquetas al crear la Serie a través del parámetro `index`.


```python
bserie = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])
print(serie)
```

    a    10
    b    20
    c    30
    d    40
    e    50
    dtype: int64
    

### Creación de una Serie a partir de un diccionario
También podemos crear una Serie a partir de un diccionario, donde las claves del diccionario se convierten en los índices de la Serie y los valores asociados a cada clave se convierten en los valores de la Serie.


```python
dic = {'a': 10, 'b': 20, 'c': 30, 'd': 40, 'e': 50}
serie = pd.Series(dic)
print(serie)
```

    a    10
    b    20
    c    30
    d    40
    e    50
    dtype: int64
    

### Creación de una Serie a partir de un valor escalar
También podemos crear una Serie a partir de un valor escalar (un valor literal), especificando el valor y el número de elementos que queremos en la Serie.
Los índices se pueden generar explícitamente mediante el parámetro `index`.


```python
serie = pd.Series(100, index = [0,1,2,3,4,5])
print(serie)
serie = pd.Series(200, index = np.arange(0, 10))
print(serie)
```

    0    100
    1    100
    2    100
    3    100
    4    100
    5    100
    dtype: int64
    0    200
    1    200
    2    200
    3    200
    4    200
    5    200
    6    200
    7    200
    8    200
    9    200
    dtype: int64
    

## Creación de DataFrames
### ¿Qué es un DataFrame?
Un DataFrame es una estructura de datos bidimensional que puede almacenar datos de diferentes tipos (como enteros, cadenas, flotantes, etc.) en columnas. Es similar a una tabla en una base de datos o una hoja de cálculo en Excel.

Un DataFrame está compuesto por filas y columnas, donde cada columna puede tener un nombre y un tipo de dato específico.  Cada fila representa una entrada o un registro de datos.
Cada fila posee un índice que permite identificarla de manera única dentro del DataFrame.

Por lo tanto un DataFrame tiene una gran similitud con las tablas del modelo relacional de bases de datos.

Podemos crear un DataFrame a partir de diversas fuentes, como listas, diccionarios, archivos CSV, bases de datos, etc.

### Creación de un DataFrame a partir de un diccionario



```python
dic = {
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
}
df = pd.DataFrame(dic)
print(df)
```

       Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    3   Marta    42    Sevilla
    

Las claves de los datos del diccionario origen se convierten en los nombres de las columnas del DataFrame, y los valores asociados a cada clave se convierten en valores de cada fila. Se genera una fila por cada elemento de las listas asociadas a las claves del diccionario.

Los índices de cada fila, por defecto, son números enteros que comienzan en 0 y aumentan secuencialmente.
El resultado visual muestra una primera fila con las etiquetas de las columnas, seguida de los datos correspondientes a cada fila los cuales están identificadas por su índice numérico a la izquierda.

Durante la creación, se puede especificar un orden concreto de columnas si se desea. Es se realiza indicando los nombres de las columnas en una lista a través del parámetro `columns`.


```python
dic = {
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
}
df = pd.DataFrame(dic, columns=['Nombre', 'Ciudad', 'Edad'])
print(df)
```

       Nombre     Ciudad  Edad
    0     Ana     Madrid    28
    1    Luis  Barcelona    34
    2  Carlos   Valencia    29
    3   Marta    Sevilla    42
    

### Creación de un DataFrame a partir de varias listas
Otra forma común de crear un DataFrame es a partir de varias listas, donde cada lista representa una columna de datos.

A la hora de crear el DataFrame, se utiliza un diccionario para especificar un nombre de columna a cada lista.


```python
nombres = ['Ana', 'Luis', 'Carlos', 'Marta']
edades = [28, 34, 29, 42]
ciudades = ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
df = pd.DataFrame({
    'Nombre': nombres,
    'Edad': edades,
    'Ciudad': ciudades
})
print(df)
```

       Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    3   Marta    42    Sevilla
    

### Creación de un DataFrame a partir de arrays de NumPy
También podemos crear un DataFrame a partir de arrays de NumPy, lo que es útil cuando trabajamos con datos numéricos.


```python
a = np.array(['Ana', 'Luis', 'Carlos', 'Marta'])
b = np.array([28, 34, 29, 42])
c = np.array(['Madrid', 'Barcelona', 'Valencia', 'Sevilla'])
df = pd.DataFrame({'Nombre': a, 'Edad': b, 'Ciudad': c})
print(df)
```

       Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    3   Marta    42    Sevilla
    

Los arrays bidimensionales de NumPy también se pueden utilizar para crear DataFrames. En este caso, cada columna del array se convierte en una columna del DataFrame.

Se suele utilizar el parámetro `columns` para especificar los nombres de las columnas.


```python
temperaturas = np.array([[15, 20, 25],
                       [18, 22, 28],
                       [20, 24, 30],
                       [17, 21, 27]])
df = pd.DataFrame(temperaturas,
                  columns=['Mañana', 'Tarde', 'Noche'])
print(df)
```

       Mañana  Tarde  Noche
    0      15     20     25
    1      18     22     28
    2      20     24     30
    3      17     21     27
    

### Creación de un DataFrame a partir de una lista de listas
Otra forma común de crear un DataFrame es a partir de una lista de listas, donde cada sublista representa una fila de datos.


```python
lista = [
    ['Ana', 28, 'Madrid'],
    ['Luis', 34, 'Barcelona'],
    ['Carlos', 29, 'Valencia'],
    ['Marta', 42, 'Sevilla']
]
df = pd.DataFrame(lista, columns=['Nombre', 'Edad', 'Ciudad'])
print(df)
```

       Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    3   Marta    42    Sevilla
    

En lugar de listas podemos utilizar tuplas para representar cada fila de datos:


```python
lista = [
    ('Ana', 28, 'Madrid'),
    ('Luis', 34, 'Barcelona'),
    ('Carlos', 29, 'Valencia'),
    ('Marta', 42, 'Sevilla')
]
df = pd.DataFrame(lista, columns=['Nombre', 'Edad', 'Ciudad'])
print(df)
```

### Creación de un DataFrame utilizando diccionarios anidados
También podemos crear un DataFrame a partir de un diccionario anidado, donde cada clave del diccionario principal representa una columna y las claves de cada diccionario interno representan los índices de las filas.


```python
dic = {
    'Madrid':{2000:3_000_000, 2010:3_200_000, 2020:3_300_000},
    'Barcelona':{2000:1_500_000, 2010:1_600_000, 2020:1_650_000},
    'Valencia':{2010:820_000, 2020:850_000}
}
df = pd.DataFrame(dic)
print(df)
```

           Madrid  Barcelona  Valencia
    2000  3000000    1500000       NaN
    2010  3200000    1600000  820000.0
    2020  3300000    1650000  850000.0
    

## Creación de Índices
### ¿Qué es un índice?
Hemos podido observar como tanto en los DataFrames como en las Series, cada fila tiene un índice asociado que permite identificarla de manera única dentro de la estructura de datos.

El tipo de objeto responsible de gestionar estos índices en pandas es el objeto **Index**.

En el caso de los **DataFrames** no solo hay un índice para las filas (_row index_), sino que también existe un índice para las columnas (_column index_).

Como hemos visto, si no especificamos un índice durante la creación de una Serie o un DataFrame, pandas genera automáticamente un índice numérico (realmente es un objeto de tipo **RangeIndex**) que comienza en 0 y aumenta secuencialmente.

Podemos personalizar los índices de las filas y columnas durante la creación de un DataFrame utilizando los parámetros `index` y `columns`, respectivamente.


```python
serie = pd.Series([9.75,8.5,3.7], index=['Matemáticas','Física','Química'])
print("Serie con índices personalizados:\n",serie)
df = pd.DataFrame([
    [9.75, 8.5, 3.7],
    [7.0, 6.5, 5.0],
    [8.0, 9.0, 7.5]
], index=['Ana', 'Luis', 'Marta'], columns=['Matemáticas', 'Física', 'Química'])
print("\nDataFrame con índices personalizados:\n",df)
```

    Serie con índices personalizados:
     Matemáticas    9.75
    Física         8.50
    Química        3.70
    dtype: float64
    
    DataFrame con índices personalizados:
            Matemáticas  Física  Química
    Ana           9.75     8.5      3.7
    Luis          7.00     6.5      5.0
    Marta         8.00     9.0      7.5
    

### Creación de índices personalizados
Podemos crear un objeto de índice utilizando el constructor `pd.Index()`, que puede recibir como argumento una colección de etiquetas, como una lista o un array de NumPy.


```python
indice = pd.Index(['a', 'b', 'c', 'd', 'e'])
print("Índice creado a partir de una lista:\n",indice)
indices = pd.Index(np.array([1, 2, 3, 4, 5]))
print("\nÍndice creado a partir de un array de NumPy:\n",indices)
```

    Índice creado a partir de una lista:
     Index(['a', 'b', 'c', 'd', 'e'], dtype='object')
    
    Índice creado a partir de un array de NumPy:
     Index([1, 2, 3, 4, 5], dtype='int64')
    

Luego podemos usar estos índices al crear Series o DataFrames.


```python
indice = pd.Index(['Historia','Geografía','Lengua','Inglés','Arte'])
serie = pd.Series([8.75,9.3,7.5,6.0,5.5], index=indice)
print("Serie con índice personalizado:\n",serie)
df = pd.DataFrame({
    'Ana':[8.75,9.3,7.5,6.0,5.5],
    'Luis':[7.0,6.5,8.0,9.0,7.5]
}, index=indice)
print("\nDataFrame con índice personalizado:\n",df)
```

    Serie con índice personalizado:
     Historia     8.75
    Geografía    9.30
    Lengua       7.50
    Inglés       6.00
    Arte         5.50
    dtype: float64
    
    DataFrame con índice personalizado:
                 Ana  Luis
    Historia   8.75   7.0
    Geografía  9.30   6.5
    Lengua     7.50   8.0
    Inglés     6.00   9.0
    Arte       5.50   7.5
    

### Asignar un índice a un DataFrame existente
Podemos asignar un índice personalizado a un DataFrame existente utilizando la propiedad `index`.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
indice = pd.Index(['ID1', 'ID2', 'ID3', 'ID4'],name="codigo")
df.index = indice
print("DataFrame con índice personalizado:\n",df)
```

    DataFrame con índice personalizado:
             Nombre  Edad     Ciudad
    codigo                         
    ID1        Ana    28     Madrid
    ID2       Luis    34  Barcelona
    ID3     Carlos    29   Valencia
    ID4      Marta    42    Sevilla
    

también podemos convertir una columna existente en el índice del DataFrame utilizando el método `set_index()`.


```python
df = pd.DataFrame(
    {
        'Codigo': ['ID1', 'ID2', 'ID3', 'ID4'],
        'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
        'Edad': [28, 34, 29, 42],
        'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
    }
)
# Convertir la columna 'codigo' en índice
df = df.set_index('Codigo')
print(df)
```

            Nombre  Edad     Ciudad
    Codigo                         
    ID1        Ana    28     Madrid
    ID2       Luis    34  Barcelona
    ID3     Carlos    29   Valencia
    ID4      Marta    42    Sevilla
    

## Mostrar solo algunos datos de DataFrames y Series
Para visualizar solo las primeras o las últimas filas de un DataFrame, podemos utilizar los métodos `head()` y `tail()`, respectivamente.
Son especialmente útiles cuando tenemos DataFrames grandes y queremos echar un vistazo rápido a los datos sin imprimir todo el conjunto.
El método `head(n)` muestra las primeras `n` filas del DataFrame (por defecto 5), mientras que el método `tail(n)` muestra las últimas `n` filas (por defecto 5).


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta', 'Sofía', 'Javier', 'Lucía', 'Diego'],
    'Edad': [28, 34, 29, 42, 31, 27, 36, 30],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla', 'Bilbao', 'Granada', 'Zaragoza', 'Málaga']
})
print("Primeras 5 filas:")
print(df.head())  # Muestra las primeras 5 filas por defecto
print("\nÚltimas 3 filas:")
print(df.tail(3))  # Muestra las últimas 3 filas
```

    Primeras 5 filas:
       Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    3   Marta    42    Sevilla
    4   Sofía    31     Bilbao
    
    Últimas 3 filas:
       Nombre  Edad    Ciudad
    5  Javier    27   Granada
    6   Lucía    36  Zaragoza
    7   Diego    30    Málaga
    

Ambos métodos funcionan también con Series.


```python
serie = pd.Series(range(1, 21))
print("Primeras 5 elementos de la Serie:")
print(serie.head())  # Muestra los primeros 5 elementos por defecto
print("\nÚltimos 4 elementos de la Serie:")
print(serie.tail(4))  # Muestra los últimos 4 elementos
```

    Primeras 5 elementos de la Serie:
    0    1
    1    2
    2    3
    3    4
    4    5
    dtype: int64
    
    Últimos 4 elementos de la Serie:
    16    17
    17    18
    18    19
    19    20
    dtype: int64
    

## Propiedades de las Series y los DataFrames
Tanto las Series como los DataFrames tienen varias propiedades útiles que nos permiten obtener información sobre su estructura y contenido.
### Propiedad values
La propiedad `values` devuelve los datos contenidos en una Serie o DataFrame en forma de array de NumPy.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Datos del DataFrame como array de NumPy:\n",df.values)
serie = pd.Series([10, 20, 30, 40, 50])
print("\nDatos de la Serie como array de NumPy:\n",serie.values)
indice = pd.Index(['a', 'b', 'c', 'd', 'e'])
print("\nDatos del Índice como array de NumPy:\n",indice.values)
```

    Datos del DataFrame como array de NumPy:
     [['Ana' 28 'Madrid']
     ['Luis' 34 'Barcelona']
     ['Carlos' 29 'Valencia']
     ['Marta' 42 'Sevilla']]
    
    Datos de la Serie como array de NumPy:
     [10 20 30 40 50]
    
    Datos del Índice como array de NumPy:
     ['a' 'b' 'c' 'd' 'e']
    

### Propiedad dtype
La propiedad `dtype` devuelve el tipo de dato de los elementos contenidos en una Serie, índice o DataFrame.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Tipos de datos de las columnas del DataFrame:\n",df.dtypes)
serie = pd.Series([10, 20, 30, 40, 50])
print("\nTipo de dato de los elementos de la Serie:\n",serie.dtype)
indice = pd.Index(['a', 'b', 'c', 'd', 'e'])
print("\nTipo de dato de los elementos del Índice:\n",indice.dtype)
```

    Tipos de datos de las columnas del DataFrame:
     Nombre    object
    Edad       int64
    Ciudad    object
    dtype: object
    
    Tipo de dato de los elementos de la Serie:
     int64
    
    Tipo de dato de los elementos del Índice:
     object
    

### Propiedad size
La propiedad `size` devuelve el número total de elementos contenidos en una Serie o DataFrame.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Número total de elementos en el DataFrame:\n",df.size)
serie = pd.Series([10, 20, 30, 40, 50])
print("\nNúmero total de elementos en la Serie:\n",serie.size)
```

    Número total de elementos en el DataFrame:
     12
    
    Número total de elementos en la Serie:
     5
    

### Propiedad name
La propiedad `name` permite asignar o recuperar el nombre de una Serie o de un índice. Se trata de un valor interno que puede ser útil para identificar la Serie o el índice en contextos más complejos.


```python
serie = pd.Series([10, 20, 30, 40, 50])
serie.name = "Números"
print("Nombre de la Serie:\n",serie.name)
indice = pd.Index(['a', 'b', 'c', 'd', 'e'])
indice.name = "Letras"
print("\nNombre del Índice:\n",indice.name)
```

    Nombre de la Serie:
     Números
    
    Nombre del Índice:
     Letras
    

### Propiedad shape
La propiedad `shape` devuelve una tupla que indica las dimensiones de una Serie o DataFrame.

En el caso de una Serie, devuelve una tupla con un solo valor que representa el número

En el caso de un DataFrame, devuelve una tupla con dos valores que representan el número de filas y columnas, respectivamente.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Dimensiones del DataFrame (filas, columnas):\n",df.shape)
serie = pd.Series([10, 20, 30, 40, 50])
print("\nDimensiones de la Serie:\n",serie.shape)
```

    Dimensiones del DataFrame (filas, columnas):
     (4, 3)
    
    Dimensiones de la Serie:
     (5,)
    

### Propiedad index
Permite obtener el índice asociado a una Serie o DataFrame.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Índice del DataFrame:\n",df.index)
serie = pd.Series([10, 20, 30, 40, 50])
print("\nÍndice de la Serie:\n",serie.index)
serie = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])
print("\nÍndice de la Serie con etiquetas personalizadas:\n",serie.index)
```

    Índice del DataFrame:
     RangeIndex(start=0, stop=4, step=1)
    
    Índice de la Serie:
     RangeIndex(start=0, stop=5, step=1)
    
    Índice de la Serie con etiquetas personalizadas:
     Index(['a', 'b', 'c', 'd', 'e'], dtype='object')
    

### Propiedad columns
La propiedad `columns` devuelve un objeto de tipo `Index` que contiene los nombres de las columnas de un DataFrame.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Nombres de las columnas del DataFrame:\n",df.columns)
```

    Nombres de las columnas del DataFrame:
     Index(['Nombre', 'Edad', 'Ciudad'], dtype='object')
    

### Función len
La función `len()` devuelve el número de elementos en una Serie o el número de filas en un DataFrame.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Número de filas en el DataFrame:\n",len(df))
serie = pd.Series([10, 20, 30, 40, 50])
print("\nNúmero de elementos en la Serie:\n",len(serie))
```

    Número de filas en el DataFrame:
     4
    
    Número de elementos en la Serie:
     5
    

## Selección de datos
Podemos acceder a los datos contenidos en un DataFrame y en una Serie utilizando diferentes métodos y técnicas.
### Acceso a un elemento de una serie
Podemos acceder a un elemento específico de una Serie utilizando su índice.


```python
serie = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])
print("Elemento con índice 'c':\n",serie['c'])  # Acceder al elemento con índice 'c'
serie = pd.Series([10, 20, 30, 40, 50])
print("\nElemento en la posición 2:\n",serie[2])  # Acceder al elemento en la posición 2
```

    Elemento con índice 'c':
     30
    
    Elemento en la posición 2:
     30
    

Podemos modificar un elemento específico de una Serie utilizando su índice.


```python
serie = pd.Series([10, 20, 30, 40, 50], index=['a', 'b', 'c', 'd', 'e'])
serie['c'] = 99  # Modificar el elemento con índice 'c'
print("Serie con el elemento modificado:\n",serie)
```

    Serie con el elemento modificado:
     a     10
    b     20
    c    999
    d     40
    e     50
    dtype: int64
    

### Indexaciones de series
Se puede utilizar la forma `inicio:fin:paso` para acceder a un rango de elementos en una Serie.


```python
serie = pd.Series([10, 20, 30, 40, 50])
print("Elementos desde la posición 1 hasta la 3 (excluida):\n",serie[1:3])  # Elementos desde la posición 1 hasta la 3 (excluida)
print("\nElementos desde el inicio hasta la posición 2 (excluida):\n",serie[:2])  # Elementos desde el inicio hasta la posición 2 (excluida)
print("\nElementos desde la posición 2 hasta el final:\n",serie[2:])  # Elementos desde la posición 2 hasta el final
print("\nElementos con paso 2:\n",serie[::2])  # Elementos con paso 2
print("\nElementos en orden inverso:\n",serie[::-1])  # Elementos en orden inverso
```

    Elementos desde la posición 1 hasta la 3 (excluida):
     1    20
    2    30
    dtype: int64
    
    Elementos desde el inicio hasta la posición 2 (excluida):
     0    10
    1    20
    dtype: int64
    
    Elementos desde la posición 2 hasta el final:
     2    30
    3    40
    4    50
    dtype: int64
    
    Elementos con paso 2:
     0    10
    2    30
    4    50
    dtype: int64
    
    Elementos en orden inverso:
     4    50
    3    40
    2    30
    1    20
    0    10
    dtype: int64
    

### Obtener columnas de un DataFrame en forma de Serie
Podemos acceder a una columna específica de un DataFrame utilizando el nombre de la columna entre corchetes `[]`, usando el estilo de acceder a los datos de los diccionarios. Esto devuelve una **Serie** que contiene los datos de esa columna.
Más adelante exploraremos las Series en detalle.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
serie = df['Edad']
print(serie)
```

    0    28
    1    34
    2    29
    3    42
    Name: Edad, dtype: int64
    

Se puede indicar también el nombre de la columna como un atributo del DataFrame utilizando el punto `.`. Esta forma es más corta y legible, pero solo funciona si el nombre de la columna es un identificador válido en Python (sin espacios, sin caracteres especiales, etc.).


```python
serie = df.Edad
print(serie)
```

    0    28
    1    34
    2    29
    3    42
    4    39
    Name: Edad, dtype: int64
    

Puesto que lo que obtenemos es una Serie, podemos utilizar las técnicas de acceso a datos que hemos visto para las Series y así llegar a un dato concreto.


```python
print("Edad de la tercera persona:\n",df["Edad"][2])  # Edad de la tercera persona (índice 2)
```

    Edad de la tercera persona:
     29
    

También podemos modificar un dato concreto de una columna accediendo primero a la columna como una Serie y luego al dato específico utilizando su índice.


```python
df['Edad'][2] = 99  # Modificar la edad de la tercera persona (índice 2)
print(df)
```

       Nombre  Edad    Ciudad
    0     Ana    28  Valencia
    1    Luis    34    Madrid
    2  Carlos    99  Valencia
    3   Marta    42   Sevilla
    4     Eva    39    Madrid
    

    C:\Users\jorge\AppData\Local\Temp\ipykernel_3764\3528726459.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      df['Edad'][2] = 99  # Modificar la edad de la tercera persona (índice 2)
    

Pero esta forma de modificar valores está desaconsejada (se produce un warning avisando de que no es apropiada). Más adelante veremos la forma correcta de hacerlo usando *loc* o *iloc*.

### Obtener varias columnas de un DataFrame
Podemos acceder a varias columnas de un DataFrame proporcionando una lista de nombres de columnas entre corchetes `[]`. Esto devuelve un nuevo DataFrame que contiene solo las columnas especificadas.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
df_seleccionado = df[['Nombre', 'Ciudad']]
print(df_seleccionado)
```

       Nombre     Ciudad
    0     Ana     Madrid
    1    Luis  Barcelona
    2  Carlos   Valencia
    3   Marta    Sevilla
    

### Acceso a filas de un DataFrame
Podemos utilizar indexaciones para obtener filas concretas de un DataFrame.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Segunda fila:\n",df[1:2])  # Segunda fila (índice 1)
print("\nFilas desde la segunda hasta la cuarta (excluida):\n",df[1:3])  # Filas desde la segunda hasta la tercera
print("\nTres primeras filas:\n",df[:3])  # Tres primeras filas
```

    Segunda fila:
       Nombre  Edad     Ciudad
    1   Luis    34  Barcelona
    
    Filas desde la segunda hasta la cuarta (excluida):
        Nombre  Edad     Ciudad
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    
    Tres primeras filas:
        Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    

Se pueden hacer indexaciones aunque los índices no sean numéricos


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
}, index=['a', 'b', 'c', 'd'])
print("Fila con índice 'b':\n",df['b':'b'])  # Fila con índice 'b'
print("\nFilas desde el índice 'b' hasta el 'c' (incluido):\n",df['b':'c'])  # Filas desde el índice 'b' hasta el 'c' (incluido)
```

    Fila con índice 'b':
       Nombre  Edad     Ciudad
    b   Luis    34  Barcelona
    
    Filas desde el índice 'b' hasta el 'c' (incluido):
        Nombre  Edad     Ciudad
    b    Luis    34  Barcelona
    c  Carlos    29   Valencia
    

También se pueden mostrar valores de columnas concretas


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']})
print("Tres primeros valores de la columna 'Nombre':\n",df['Nombre'][:3])
# Mediante una lista de nombres de columnas
print("\nTres primeros valores de las columnas 'Nombre' y 'Edad':\n",df[['Nombre','Edad']][:3])
```

    Tres primeros valores de la columna 'Nombre':
     0       Ana
    1      Luis
    2    Carlos
    Name: Nombre, dtype: object
    
    Tres primeros valores de las columnas 'Nombre' y 'Edad':
        Nombre  Edad
    0     Ana    28
    1    Luis    34
    2  Carlos    29
    

### Acceso a filas y columnas con loc[]
El método `loc[]` permite acceder a los datos utilizando las etiquetas de las filas y columnas


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
# Acceder a una fila específica por etiqueta
print("Segunda fila: \n",df.loc[1])  # Segunda fila (índice 1)
# Mostrar varias filas
print("\nFilas con índices 1 y 3:\n",df.loc[[1, 3]])
print("\nTres primeras filas:\n",df.loc[:2])
# Acceder a una columna específica por etiqueta
print("\nColumna edad:\n",df.loc[:, 'Edad'])
# Acceder a un valor específico por fila y columna
print("\nValor de la tercera fila y columna Ciudad:\n",df.loc[2, 'Ciudad'])
# Valores de dos columnas
print("\nValores de las columnas 'Nombre' y 'Edad':\n",df.loc[:, ['Nombre', 'Edad']])
```

    Segunda fila: 
     Nombre         Luis
    Edad             34
    Ciudad    Barcelona
    Name: 1, dtype: object
    
    Filas con índices 1 y 3:
       Nombre  Edad     Ciudad
    1   Luis    34  Barcelona
    3  Marta    42    Sevilla
    
    Tres primeras filas:
        Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    
    Columna edad:
     0    28
    1    34
    2    29
    3    42
    Name: Edad, dtype: int64
    
    Valor de la tercera fila y columna Ciudad:
     Valencia
    
    Valores de las columnas 'Nombre' y 'Edad':
        Nombre  Edad
    0     Ana    28
    1    Luis    34
    2  Carlos    29
    3   Marta    42
    

Se puede modificar un valor concreto usando *loc*


```python
df.loc[2, 'Ciudad'] = 'Palencia'
print("\nDataFrame con la ciudad de la tercera fila modificada:\n",df)
```

    
    DataFrame modificado:
        Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Palencia
    3   Marta    42    Sevilla
    

Podemos modificar varios valores a la vez


```python
#  Modificación usando listas
df.loc[:, 'Ciudad'] = ['A Coruña', 'Lugo', 'Ourense', 'Pontevedra']
df.loc[:, 'Edad'] = 25
print("\nDataFrame con la columna Edad modificada:\n",df)
df.loc[0:1, 'Nombre'] = ['Juan', 'María']
print("\nDataFrame con los nombres de las primeras dos filas modificados:\n",df)
```

    
    DataFrame con la columna Edad modificada:
        Nombre  Edad      Ciudad
    0    Juan    25    A Coruña
    1   Pedro    25        Lugo
    2  Carlos    25     Ourense
    3   Marta    25  Pontevedra
    
    DataFrame con los nombres de las primeras dos filas modificados:
        Nombre  Edad      Ciudad
    0    Juan    25    A Coruña
    1   María    25        Lugo
    2  Carlos    25     Ourense
    3   Marta    25  Pontevedra
    

### Acceso por posición con iloc[]
El método `iloc[]` permite acceder a los datos utilizando las posiciones enteras de las filas y columnas.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print("Valor de la segunda fila y tercera columna:\n",df.iloc[1,2])
print("\nSegunda fila:\n",df.iloc[1])  # Segunda fila (índice 1)
print("\nColumna edad:\n",df.iloc[:, 1])  # Columna 'Edad'
print("\nValor de la tercera fila y columna Ciudad:\n",df.iloc[2, 2])  # Valor en la tercera fila y columna 'Ciudad'
```

    Valor de la segunda fila y tercera columna:
     Barcelona
    
    Segunda fila:
     Nombre         Luis
    Edad             34
    Ciudad    Barcelona
    Name: 1, dtype: object
    
    Columna edad:
     0    28
    1    34
    2    29
    3    42
    Name: Edad, dtype: int64
    
    Valor de la tercera fila y columna Ciudad:
     Valencia
    

`iloc` también permite modificar los valores de un DataFrame.


```python
df.iloc[2, 2] = 'Palencia'
print("\nDataFrame con la ciudad de la tercera fila modificada:\n",df)
df.iloc[:,1] = 25
print("\nDataFrame con la columna Edad modificada:\n",df)
df.iloc[0:2,0] = ['Juan','María']
print("\nDataFrame con los nombres de las primeras dos filas modificados:\n",df)
```

    
    DataFrame con la ciudad de la tercera fila modificada:
        Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Palencia
    3   Marta    42    Sevilla
    
    DataFrame con la columna Edad modificada:
        Nombre  Edad     Ciudad
    0     Ana    25     Madrid
    1    Luis    25  Barcelona
    2  Carlos    25   Palencia
    3   Marta    25    Sevilla
    
    DataFrame con los nombres de las primeras dos filas modificados:
        Nombre  Edad     Ciudad
    0    Juan    25     Madrid
    1   María    25  Barcelona
    2  Carlos    25   Palencia
    3   Marta    25    Sevilla
    

## Filtrar datos en un DataFrame
### Filtrado lógico
Podemos filtrar los datos de un DataFrame utilizando condiciones lógicas para seleccionar filas que cumplan ciertos criterios.

Los filtros lógicos se realizan utilizando operadores booleanos sobre las columnas del DataFrame, lo que devuelve una Serie de valores booleanos que indican si cada fila cumple la condición especificada. Luego, podemos utilizar esta Serie booleana para indexar el DataFrame y obtener solo las filas que cumplen la condición.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
# Filtrar filas donde la edad es mayor que 30
filtro = df['Edad'] > 30
df_filtrado = df[filtro]
print("DataFrame filtrado (edad > 30):\n",df_filtrado)
filtro = df['Nombre'] == 'Ana'
df_filtrado = df[filtro]
print("\nDataFrame filtrado (nombre = 'Ana'):\n",df_filtrado)
```

    DataFrame filtrado (edad > 30):
       Nombre  Edad     Ciudad
    1   Luis    34  Barcelona
    3  Marta    42    Sevilla
    
    DataFrame filtrado (nombre = 'Ana'):
       Nombre  Edad  Ciudad
    0    Ana    28  Madrid
    

Se pueden unir varias condiciones con operaciones lógicas (& para and,  | para or, ...)


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta', 'Eva'],
    'Edad': [28, 34, 29, 42, 39],
    'Ciudad': ['Valencia', 'Madrid', 'Valencia', 'Sevilla', 'Madrid']
})
filtro1 = df['Edad'] > 35
filtro2 = df['Ciudad'] == 'Madrid'
df_filtrado = df[(filtro1 & filtro2)]
print("DataFrame filtrado (edad > 35 y ciudad = 'Madrid'):\n",df_filtrado)
df_filtrado = df[(filtro1 | filtro2)]
print("\nDataFrame filtrado (edad > 35 o ciudad = 'Madrid'):\n",df_filtrado)
df_filtrado = df[(filtro1 & ~filtro2)]
print("\nDataFrame filtrado (edad > 35 y ciudad != 'Madrid'):\n",df_filtrado)

```

    0    28
    1    34
    2    29
    3    42
    4    39
    Name: Edad, dtype: int64
    DataFrame filtrado (edad > 35 y ciudad = 'Madrid'):
       Nombre  Edad  Ciudad
    4    Eva    39  Madrid
    
    DataFrame filtrado (edad > 35 o ciudad = 'Madrid'):
       Nombre  Edad   Ciudad
    1   Luis    34   Madrid
    3  Marta    42  Sevilla
    4    Eva    39   Madrid
    
    DataFrame filtrado (edad > 35 y ciudad != 'Madrid'):
       Nombre  Edad   Ciudad
    3  Marta    42  Sevilla
    

### Método filter()
El método `filter()` permite filtrar las columnas o filas de un DataFrame basándose en etiquetas o condiciones específicas.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
}, index= ['cod203', 'cod475', 'cod507', 'cod607'])
print("DataFrame original:\n",df)
# Filtrar columnas por nombre
df_filtrado = df.filter(["Nombre","Edad"])
print("DataFrame con columnas filtradas:\n",df_filtrado)
# Filtrar filas por índice
df_filtrado = df.filter(["cod203","cod607"], axis=0)
print("\nDataFrame con filas filtradas:\n",df_filtrado)
# Filtrar filas por condición en el índice
df_filtrado = df.filter(like="7", axis=0)
print("\nDataFrame con filas cuyo índice contiene '7':\n",df_filtrado)
df_filtrado = df.filter(regex="7$", axis=0)
print("\nDataFrame con filas cuyo índice termina en '7':\n",df_filtrado)
```

    DataFrame original:
             Nombre  Edad     Ciudad
    cod203     Ana    28     Madrid
    cod475    Luis    34  Barcelona
    cod507  Carlos    29   Valencia
    cod607   Marta    42    Sevilla
    DataFrame con columnas filtradas:
             Nombre  Edad
    cod203     Ana    28
    cod475    Luis    34
    cod507  Carlos    29
    cod607   Marta    42
    
    DataFrame con filas filtradas:
            Nombre  Edad   Ciudad
    cod203    Ana    28   Madrid
    cod607  Marta    42  Sevilla
    
    DataFrame con filas cuyo índice contiene '7':
             Nombre  Edad     Ciudad
    cod475    Luis    34  Barcelona
    cod507  Carlos    29   Valencia
    cod607   Marta    42    Sevilla
    
    DataFrame con filas cuyo índice termina en '7':
             Nombre  Edad    Ciudad
    cod507  Carlos    29  Valencia
    cod607   Marta    42   Sevilla
    
    DataFrame con columnas cuyo nombre termina en 'a':
     Empty DataFrame
    Columns: []
    Index: [cod203, cod475, cod507, cod607]
    

### Filtrado por tipo de datos
Se realiza mediante el método `select_dtypes`, al que se le pasa el tipo de datos que queremos seleccionar


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']})
df_filtrado = df.select_dtypes("int")
print("Filtrado por tipo = 'int':\n",df_filtrado)
df_filtrado = df.select_dtypes(["int","object"])
print("\nFiltrado por tipo = 'int' u 'object':\n",df_filtrado)
df_filtrado = df.select_dtypes(exclude="object")
print("\nFiltrado por tipo distinto de 'object':\n",df_filtrado)
```

    Filtrado por tipo = 'int':
        Edad
    0    28
    1    34
    2    29
    3    42
    
    Filtrado por tipo = 'int' u 'object':
        Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    3   Marta    42    Sevilla
    
    Filtrado por tipo distinto de 'object':
        Edad
    0    28
    1    34
    2    29
    3    42
    

### Filtrado con arrays booleanos
Podemos filtrar un DataFrame utilizando arrays booleanos, que son arrays de valores booleanos de la misma longitud que el DataFrame.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
filtro = [True, False, True, False]
print("Array original:\n",df);
print("\nArray de filtros:\n",filtro)
print("\nValores filtrados:\n",df[filtro])
```

    Array original:
        Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    3   Marta    42    Sevilla
    
    Array de filtros:
     [True, False, True, False]
    
    Valores filtrados:
        Nombre  Edad    Ciudad
    0     Ana    28    Madrid
    2  Carlos    29  Valencia
    

## Operar con DataFrames
### Eliminar columnas
Podemos eliminar columnas utilizando el operador `del`.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
del df['Ciudad']
print("DataFrame con la columna 'Ciudad' eliminada:\n",df)
```

    DataFrame con la columna 'Ciudad' eliminada:
        Nombre  Edad
    0     Ana    28
    1    Luis    34
    2  Carlos    29
    3   Marta    42
    

### Añadir columnas a DataFrames
Basta con indicar su nombre entre corchetes e indicar un primer valor con el que se rellenarán todas sus filas


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
df["Departamento"] = "Ventas"
print("DataFrame con nueva columna 'Departamento':\n", df)
```

    DataFrame con nueva columna 'Departamento':
        Nombre  Edad     Ciudad Departamento
    0     Ana    28     Madrid       Ventas
    1    Luis    34  Barcelona       Ventas
    2  Carlos    29   Valencia       Ventas
    3   Marta    42    Sevilla       Ventas
    

Podemos también dar varios valores concretos a la columna


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
df["Departamento"] = ["Ventas","Producción","Producción","Ventas"]
print("DataFrame con nueva columna 'Departamento':\n", df)
```

    DataFrame con nueva columna 'Departamento':
        Nombre  Edad     Ciudad Departamento
    0     Ana    28     Madrid       Ventas
    1    Luis    34  Barcelona   Producción
    2  Carlos    29   Valencia   Producción
    3   Marta    42    Sevilla       Ventas
    

### Eliminar filas
Podemos eliminar filas utilizando el método `drop()`, especificando el índice de la fila que queremos eliminar y el parámetro `inplace=True` para modificar el DataFrame original (de otro modo se devuelve una copia y el original se deja sin modificar).


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
df.drop(1, inplace=True)  # Elimina la fila con índice 1 (segunda fila)
print("DataFrame con la segunda fila eliminada:\n",df)
```

    DataFrame con la segunda fila eliminada:
        Nombre  Edad    Ciudad
    0     Ana    28    Madrid
    2  Carlos    29  Valencia
    3   Marta    42   Sevilla
    

### Trasponer un DataFrame
Podemos trasponer un DataFrame utilizando el atributo `T`, que intercambia las filas y las columnas. Este atributo devuelve una nueva vista con el DataFrame traspuesto.



```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
df_traspuesto = df.T
print("DataFrame traspuesto:\n",df_traspuesto)
```

    DataFrame traspuesto:
                  0          1         2        3
    Nombre     Ana       Luis    Carlos    Marta
    Edad        28         34        29       42
    Ciudad  Madrid  Barcelona  Valencia  Sevilla
    

### Operaciones matemáticas
Podemos sumar escalares a columnas, filas o selecciones concretas de un DataFrame


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]
})
print("Muestra la columna edad sumada 5:\n",df['Edad'] + 5)
df['Edad'] += 5
print("\nDataFrame con la edad sumada 5:\n",df)
# Subir las ventas de Madrid en 150
mascara = df['Ciudad'] == 'Madrid'
df.loc[mascara, 'Ventas'] += 150
print("\nDataFrame con las ventas incrementadas en 150 para Madrid:\n",df)
```

    Muestra la columna edad sumada 5:
     0    33
    1    39
    2    34
    3    47
    Name: Edad, dtype: int64
    
    DataFrame con la edad sumada 5:
        Nombre  Edad     Ciudad  Ventas
    0     Ana    33     Madrid  1200.5
    1    Luis    39  Barcelona   650.0
    2  Carlos    34   Valencia  1860.5
    3   Marta    47     Madrid   930.2
    
    DataFrame con las ventas incrementadas en 150 para Madrid:
        Nombre  Edad     Ciudad  Ventas
    0     Ana    33     Madrid  1350.5
    1    Luis    39  Barcelona   650.0
    2  Carlos    34   Valencia  1860.5
    3   Marta    47     Madrid  1080.2
    

Podemos operar usando valores de una Serie:


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]
})

serie = pd.Series([100, 200, 300, 400])
df["Ventas"] += serie
print("Ventas incrementadas con los datos de la Serie:\n",df)
```

    Ventas incrementadas con los datos de la Serie:
        Nombre  Edad     Ciudad  Ventas
    0     Ana    28     Madrid  1300.5
    1    Luis    34  Barcelona   850.0
    2  Carlos    29   Valencia  2160.5
    3   Marta    42     Madrid  1330.2
    

Lo mismo con otros tipos de datos compatibles como listas, tuplas, arrays de NumPy, etc.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]
})
#Nueva lista de edades
edades = [25, 31, 30, 50]
df["Edad"] = edades
print("DataFrame con las edades actualizadas:\n",df)
#Array de NumPy con el incremento de las ventas
incremento = np.array([.2,.1,.3,.4])
df["Ventas"] *= (1+incremento)
print("\nDataFrame con las ventas incrementadas:\n",df)

```

    DataFrame con las edades actualizadas:
        Nombre  Edad     Ciudad  Ventas
    0     Ana    25     Madrid  1200.5
    1    Luis    31  Barcelona   650.0
    2  Carlos    30   Valencia  1860.5
    3   Marta    50     Madrid   930.2
    
    DataFrame con las ventas incrementadas:
        Nombre  Edad     Ciudad   Ventas
    0     Ana    25     Madrid  1440.60
    1    Luis    31  Barcelona   715.00
    2  Carlos    30   Valencia  2418.65
    3   Marta    50     Madrid  1302.28
    

### Usar cálculos de totales
Las series de panda poseen cálculos de totales que se aplican a los valores de la serie. Disponemos de los métodos: `count`, `min`, `max`, `mean`, `std`, `sum`, etc.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]
})
print("Media de las ventas:\n",df['Ventas'].mean())
print("Máximo valor de las ventas:\n",df['Ventas'].max())
print("Mínimo valor de las ventas:\n",df['Ventas'].min())
print("Suma de las ventas:\n",df['Ventas'].sum())
```

    Media de las ventas:
     1160.3
    Máximo valor de las ventas:
     1860.5
    Mínimo valor de las ventas:
     650.0
    Suma de las ventas:
     4641.2
    

### Método **agg**
Otra forma de realizar estos cálculos, es mediante la función `agg` la cual permite indicar la función de cálculo como string.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]
})
print("Media de las ventas:\n",df['Ventas'].agg("mean"))
print("Máximo valor de las ventas:\n",df['Ventas'].agg("max"))
print("Mínimo valor de las ventas:\n",df['Ventas'].agg("min"))
print("Suma de las ventas:\n",df['Ventas'].agg("sum"))
```

La ventaja fundamental de `agg` es que podemos realizar varios cálculos a la vez ya que admite que se reciba una lista de cálculos


```python
print("Mínimo y máximo:\n",df['Ventas'].agg(['max','min']))
```

    Mínimo y máximo:
     max    1860.5
    min     650.0
    Name: Ventas, dtype: float64
    

### Uso de funciones **callback** para cálculos de totales
Se pueden personalizar los cálculos de totales mediante funciones personales.

En el ejemplo siguiente se define una función que calcula la diferencia entre el máximo y el mínimo de una serie. Luego se utiliza esta función en el método `agg` para calcular este valor junto con el máximo y el mínimo de la serie de ventas.


```python
# Calcula la diferencia entre el máximo y el mínimo de una serie
def dif_max_min(serie):
    return serie.max() - serie.min()

df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]
})
print(df['Ventas'].agg(["max","min",dif_max_min]))


```

    max            1860.5
    min             650.0
    dif_max_min    1210.5
    Name: Ventas, dtype: float64
    

### Trasformaciones
El métdo `agg()` permite aplicar funciones de cálculo, las cuales devuelven un único valor. Si queremos aplicar funciones que transformen cada uno de los datos de una serie, debemos usar el método `transform()`.

Su funcionamiento es similar, recibe como parámetro una función (predefinida o personalizada) y la aplica a cada uno de los valores de la serie, devolviendo una nueva serie con los valores transformados.


```python
def ventas_con_iva(venta):
    return venta * 1.21  # Añade un 21% de IVA

df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]b
})

df["Ventas_con_IVA"] = df['Ventas'].transform(ventas_con_iva)
print("Ventas con IVA aplicado:\n",df)
```

    Ventas con IVA aplicado:
        Nombre  Edad     Ciudad  Ventas  Ventas_con_IVA
    0     Ana    28     Madrid  1200.5        1452.605
    1    Luis    34  Barcelona   650.0         786.500
    2  Carlos    29   Valencia  1860.5        2251.205
    3   Marta    42     Madrid   930.2        1125.542
    

Aunque en este caso es más sencillo usar operaciones vectorizadas, el método `transform()` es útil cuando se necesitan funciones de transformación más complejas.

El equivalente vectorizado sería:


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Madrid'],
    'Ventas': [1200.5, 650., 1860.5, 930.2]
})
df["Ventas_con_IVA"] = df['Ventas'] * 1.21
print("Ventas con IVA aplicado (vectorizado):\n",df)
```

    Ventas con IVA aplicado (vectorizado):
        Nombre  Edad     Ciudad  Ventas  Ventas_con_IVA
    0     Ana    28     Madrid  1200.5        1452.605
    1    Luis    34  Barcelona   650.0         786.500
    2  Carlos    29   Valencia  1860.5        2251.205
    3   Marta    42     Madrid   930.2        1125.542
    

### Método `map()`
El método `map()` permite aplicar una función a cada uno de los elementos de una Serie, devolviendo una nueva Serie con los resultados.

La diferencia con `transform()` es que `map()` se utiliza exclusivamente con Series, mientras que `transform()` puede aplicarse tanto a Series como a DataFrames.

Otra diferencia es que `map()` permite mapear valores específicos a otros valores utilizando un diccionario o una Serie, además de aplicar funciones.


```python
# Ejemplo de función para mapear comprueba si tenemos una nota
# o una lista de notas y calcula la media si tenemos una lista
def calcular_media(nota):
    if isinstance(nota,list):
        return sum(nota) / len(nota)
    else:
        return nota
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Notas': [8.5, [7.0, 8.0, 9.0], 6.5, [9.0, 8.5]]
})
df['Media'] = df['Notas'].map(calcular_media)
print("DataFrame con la media de las notas:\n",df)
```

    DataFrame con la media de las notas:
        Nombre            Notas  Media
    0     Ana              8.5   8.50
    1    Luis  [7.0, 8.0, 9.0]   8.00
    2  Carlos              6.5   6.50
    3   Marta       [9.0, 8.5]   8.75
    

### Método `unique()`
El método `unique()` devuelve un array de NumPy que contiene los valores únicos presentes en una Serie.

Los valores se devuelven en forma de array de NumPy.


```python
serie = pd.Series(['Manzana', 'Plátano', 'Manzana', 'Naranja', 'Plátano', 'Manzana'])
valores_unicos = serie.unique()
print("Valores únicos en la Serie:\n",valores_unicos)
```

    Valores únicos en la Serie:
     ['Manzana' 'Plátano' 'Naranja']
    

### Método `value_counts()`
El método `value_counts()` cuenta la frecuencia de cada valor único en una Serie y devuelve una nueva Serie con los valores únicos como índice y sus frecuencias como valores.


```python
serie = pd.Series(['Manzana', 'Plátano', 'Manzana', 'Naranja', 'Plátano', 'Manzana'])
frecuencias = serie.value_counts()
print("Frecuencia de cada fruta:\n",frecuencias)
```

    Frecuencia de cada fruta:
     Manzana    3
    Plátano    2
    Naranja    1
    Name: count, dtype: int64
    

### Método `describe()`
El método `describe()` proporciona estadísticas descriptivas resumidas de una Serie o DataFrame, incluyendo conteo, media, desviación estándar, valores mínimos y máximos, y percentiles.


```python
serie = pd.Series([10, 20, 30, 40, 50])
estadisticas = serie.describe()
print("Estadísticas descriptivas de la Serie:\n",estadisticas)
df = pd.DataFrame({
    'Edad': [28, 34, 29, 42],
    'Ventas': [1200.5, 650., 1860.5,  930.2],
})
estadisticas_df = df.describe()
print("\nEstadísticas descriptivas del DataFrame:\n",estadisticas_df)
```

    Estadísticas descriptivas de la Serie:
     count     5.000000
    mean     30.000000
    std      15.811388
    min      10.000000
    25%      20.000000
    50%      30.000000
    75%      40.000000
    max      50.000000
    dtype: float64
    
    Estadísticas descriptivas del DataFrame:
                 Edad       Ventas
    count   4.000000     4.000000
    mean   33.250000  1160.300000
    std     6.396614   518.088853
    min    28.000000   650.000000
    25%    28.750000   860.150000
    50%    31.500000  1065.350000
    75%    36.000000  1365.500000
    max    42.000000  1860.500000
    

### Método `astype()`
El método `astype()` permite convertir el tipo de datos de una Serie a otro tipo especificado.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Salario': ['2875', '2300', '1700', '1650']
})
df['Salario'] = df['Salario'].astype('float64')
print("DataFrame con la columna 'Salario' convertida a float:\n",df)
```

    DataFrame con la columna 'Salario' convertida a float:
        Nombre  Salario
    0     Ana   2875.0
    1    Luis   2300.0
    2  Carlos   1700.0
    3   Marta   1650.0
    

### Método `sort_values()`
El método `sort_values()` permite ordenar los valores de una Serie o DataFrame en orden ascendente o descendente.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
# Ordenar por edad en orden ascendente
df_ordenado = df.sort_values(by='Edad')
print("DataFrame ordenado por edad (ascendente):\n",df_ordenado)
# Ordenar por edad en orden descendente
df_ordenado_desc = df.sort_values(by='Edad', ascending=False)
print("\nDataFrame ordenado por edad (descendente):\n",df_ordenado_desc)

```

    DataFrame ordenado por edad (ascendente):
        Nombre  Edad     Ciudad
    0     Ana    28     Madrid
    2  Carlos    29   Valencia
    1    Luis    34  Barcelona
    3   Marta    42    Sevilla
    
    DataFrame ordenado por edad (descendente):
        Nombre  Edad     Ciudad
    3   Marta    42    Sevilla
    1    Luis    34  Barcelona
    2  Carlos    29   Valencia
    0     Ana    28     Madrid
    

## Obtener información del DataFrame
### Método info()
El método `info()` proporciona un resumen conciso del DataFrame, incluyendo el número de filas.


```python
df = pd.DataFrame({
    'Nombre': ['Ana', 'Luis', 'Carlos', 'Marta'],
    'Edad': [28, 34, 29, 42],
    'Ciudad': ['Madrid', 'Barcelona', 'Valencia', 'Sevilla']
})
print(df.info())
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4 entries, 0 to 3
    Data columns (total 3 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   Nombre  4 non-null      object
     1   Edad    4 non-null      int64 
     2   Ciudad  4 non-null      object
    dtypes: int64(1), object(2)
    memory usage: 228.0+ bytes
    None
    

### Propiedad columns
La propiedad `columns` devuelve un objeto de tipo `Index` que contiene los nombres de las columnas del DataFrame.


```python
print(df.columns)
```

    Index(['Nombre', 'Edad', 'Ciudad'], dtype='object')
    

### Propiedad shape
La propiedad `shape` devuelve una tupla que indica el número de filas y columnas del DataFrame.


```python
print(df.shape)
```

    (4, 3)
    

### Propiedad dtypes
La propiedad `dtypes` devuelve una **Serie** que contiene los tipos de datos de cada columna del DataFrame.


```python
print(df.dtypes)
```

    Nombre    object
    Edad       int64
    Ciudad    object
    dtype: object
    

### Propiedad index
La propiedad `index` devuelve el índice (etiquetas de las filas) del DataFrame


```python
print(df.index);
```

    RangeIndex(start=0, stop=4, step=1)
    
