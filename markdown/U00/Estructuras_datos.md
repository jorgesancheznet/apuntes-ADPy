# Estructuras de datos en Python
## Contenidos
- [Listas](#listas)
    - [¿Qué es una lista?](#qué-es-una-lista)
    - [Creación de listas](#creación-de-listas)
    - [Acceso a los elementos de una lista](#acceso-a-los-elementos-de-una-lista)
    - [Obtener el tamaño de una lista](#obtener-el-tamaño-de-una-lista)
    - [Operaciones con listas](#operaciones-con-listas)
        - [Concatenación](#concatenación)
        - [Repetición](#repetición)
        - [Añadir elementos a una lista](#añadir-elementos-a-una-lista)
        - [Contar elementos en una lista](#contar-elementos-en-una-lista)
        - [Eliminar elementos de una lista](#eliminar-elementos-de-una-lista)
        - [Eliminar toda la lista](#eliminar-toda-la-lista)
        - [Ordenar una lista](#ordenar-una-lista)
        - [Operador `in`](#operador-in)
        - [Método `index()`](#método-index)
    - [Slicing (rebanado) de listas. Índices avanzados](#slicing-rebanado-de-listas-índices-avanzados)
- [Tuplas](#tuplas)
    - [¿Qué es una tupla?](#qué-es-una-tupla)
    - [Creación de tuplas](#creación-de-tuplas)
    - [Acceso a los elementos de una tupla](#acceso-a-los-elementos-de-una-tupla)
    - [Operadores, propiedades y métodos de las tuplas](#operadores-propiedades-y-métodos-de-las-tuplas)
- [Conjuntos](#conjuntos)
    - [¿Qué es un conjunto?](#qué-es-un-conjunto)
    - [Creación de conjuntos](#creación-de-conjuntos)
    - [Limitaciones de los conjuntos](#limitaciones-de-los-conjuntos)
    - [Operaciones con conjuntos](#operaciones-con-conjuntos)
        - [Unión](#unión)
        - [Intersección](#intersección)
        - [Diferencia](#diferencia)
        - [Diferencia simétrica](#diferencia-simétrica)
- [Diccionarios](#diccionarios)
    - [¿Qué es un diccionario?](#qué-es-un-diccionario)
    - [Creación de diccionarios](#creación-de-diccionarios)
    - [Acceso a los elementos de un diccionario](#acceso-a-los-elementos-de-un-diccionario)
    - [Añadir elementos a un diccionario](#añadir-elementos-a-un-diccionario)
    - [Obtener el tamaño de un diccionario](#obtener-el-tamaño-de-un-diccionario)
    - [Operaciones con diccionarios](#operaciones-con-diccionarios)
        - [Unión de diccionarios](#unión-de-diccionarios)
        - [Eliminar elementos de un diccionario](#eliminar-elementos-de-un-diccionario)
        - [Eliminar todos los elementos de un diccionario](#eliminar-todos-los-elementos-de-un-diccionario)
- [Conversiones entre estructuras de datos](#conversiones-entre-estructuras-de-datos)
    - [Convertir a lista](#convertir-a-lista)
    - [Convertir a tupla](#convertir-a-tupla)
    - [Convertir a conjunto](#convertir-a-conjunto)
    - [Convertir a diccionario](#convertir-a-diccionario)

## Listas
### ¿Qué es una lista?
Una lista es una colección de datos que se almacenan en una variable.

Podemos acceder a cada elemento de la lista mediante un índice, que es un número que indica la posición del elemento en la lista. Los índices comienzan a numerar desde el cero.

Las listas tienen semejanzas con los arrays de otros lenguajes de programación, pero tienen la ventaja de que pueden contener elementos de diferentes tipos de datos (números, cadenas de texto, booleanos, etc.) y su tamaño puede cambiar dinámicamente.

Las listas son una estructura **mutable**, lo que significa que podemos modificar su contenido después de haberlas creado.

### Creación de listas
Podemos crear una lista utilizando corchetes `[]` y separando los elementos con comas. Por ejemplo:


```python
lista1 = []  # Lista vacía
lista2 = [1, 2, 3, 4, 5]  # Lista de números
lista3 = ['a', 'b', 'c', 'd']  # Lista de cadenas de texto
lista4 = [1, 'b', 3.5, True]  # Lista con diferentes tipos de datos
lista5 = ["Hola", 18, 25, [2, 3, 4]]  # Lista con una sublista
print(lista1)
print(lista2)
print(lista3)
print(lista4)
print(lista5)
```

    []
    [1, 2, 3, 4, 5]
    ['a', 'b', 'c', 'd']
    [1, 'b', 3.5, True]
    ['Hola', 18, 25, [2, 3, 4]]
    

Se pueden crear también listas utilizando la función `list()`:


```python
lista1 = list()  # Lista vacía
lista2 = list((1, 2, 3, 4, 5))  # Lista a partir de una tupla
lista3 = list("Hola")  # Lista a partir de una cadena de texto
print(lista1)
print(lista2)
print(lista3)
```

    []
    [1, 2, 3, 4, 5]
    ['H', 'o', 'l', 'a']
    

### Acceso a los elementos de una lista
Podemos acceder a los elementos de una lista utilizando su índice entre corchetes `[]`. Por ejemplo:


```python
lista = [10, 20, 30, 40, 50]
print(lista[0])  # Primer elemento
print(lista[2])  # Tercer elemento
print(lista[-1])  # Último elemento
```

    10
    30
    50
    

También se puede modificar el valor de un elemento accediendo a su índice:


```python
lista = [10, 20, 30, 40, 50]
lista[1] = 25  # Modificar el segundo elemento
print(lista)
```

    [10, 25, 30, 40, 50]
    

### Obtener el tamaño de una lista
Podemos obtener el número de elementos de una lista utilizando la función `len()`:


```python
lista = [10, 20, 30, 40, 50]
tamaño = len(lista)
print("El tamaño de la lista es:", tamaño)
```

    El tamaño de la lista es: 5
    

### Operaciones con listas
#### Concatenación
Se realiza mediante el operador '+':


```python
lista1 = [10, 20, 30]
lista2 = [40, 50]
lista3 = lista1 + lista2  # Muestra [10, 20, 30, 40, 50]
print(lista3)
```

    [10, 20, 30, 40, 50]
    

#### Repetición
Se realiza mediante el operador '*':


```python
lista1 = [10, 20]
lista2 = lista1 * 3
print(lista2)  # [10, 20, 10, 20, 10, 20]
```

    [10, 20, 10, 20, 10, 20]
    

#### Añadir elementos a una lista
El método `append()` añade un elemento al final de la lista:


```python
lista = [10, 20, 30]
lista.append(40)
print(lista)  # [10, 20, 30, 40]
```

    [10, 20, 30, 40]
    

#### Contar elementos en una lista
El método `count()` cuenta cuántas veces aparece un elemento en la lista:


```python
lista = [10, 20, 30, 20, 40, 20, 50]
contador = lista.count(20)  # El resultado es 3
print(contador)
```

    3
    

#### Eliminar elementos de una lista
El método `remove()` elimina la primera aparición de un elemento en la lista:


```python
lista = [10, 20, 30, 20, 40, 20, 50]
lista.remove(20)
print(lista)  # Quita el primer 20: [10, 30, 20, 40, 20, 50]
```

    [10, 30, 20, 40, 20, 50]
    

Por otro lado, el método `pop()` elimina un elemento en una posición específica y lo devuelve:


```python
lista = [10, 20, 30, 20, 40, 20, 50]
elemento = lista.pop(2)  # Elimina el elemento en la posición 2 (tercer elemento)
print("Elemento eliminado:", elemento)
print("Lista después de eliminar el elemento:", lista)
```

    Elemento eliminado: 30
    Lista después de eliminar el elemento: [10, 20, 20, 40, 20, 50]
    

#### Eliminar toda la lista
El método `clear()` elimina todos los elementos de la lista:


```python
lista = [10, 20, 30, 20, 40, 20, 50]
lista.clear()
print(lista)  # Muestra []
```

    []
    

#### Ordenar una lista
El método `sort()` ordena los elementos de la lista en orden ascendente. Este método modifica la lista original.


```python
lista = [20, 40, 10, 30, 60, 50]
lista.sort()
print(lista)  # Muestra [10, 20, 30, 40, 50, 60]
```

    [10, 20, 30, 40, 50, 60]
    

Podemos ordenar al revés utilizando el parámetro `reverse=True`:


```python
lista = [20, 40, 10, 30, 60, 50]
lista.sort(reverse=True)
print(lista)  # Muestra [60, 50, 40, 30, 20, 10]
```

    [60, 50, 40, 30, 20, 10]
    

#### Operador `in`
El operador `in` nos permite verificar si un elemento está presente en una lista:


```python
lista = [10, 20, 30, 40, 50]
print(20 in lista)  # True
print(60 in lista)  # False
```

    True
    False
    

#### Método `index()`
El método `index()` devuelve el índice de la primera aparición de un elemento en la lista:


```python
lista = [10, 20, 30, 40, 50]
print(lista.index(20)) # 1
print(lista.index(70)) # Error: ValueError
```

    1
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Cell In[19], line 3
          1 lista = [10, 20, 30, 40, 50]
          2 print(lista.index(20)) # 1
    ----> 3 print(lista.index(70)) # Error: ValueError
    

    ValueError: 70 is not in list


### Slicing (rebanado) de listas. Índices avanzados
El slicing nos permite obtener una sublista a partir de una lista original utilizando la sintaxis `lista[inicio:fin:paso]`:
- `inicio`: índice donde comienza la sublista (inclusive).
- `fin`: índice donde termina la sublista (exclusive).
- `paso`: cantidad de elementos que se saltan (opcional). Por defecto es 1.


```python
lista = [10, 20, 30, 40, 50, 60, 70, 80, 90]
sublista1 = lista[2:5]  # [30, 40, 50]
print("Sublista1:\n",sublista1)
sublista2 = lista[:4]  # [10, 20, 30, 40]
print("\nSublista2:\n",sublista2)
sublista3 = lista[5:]  # [60, 70, 80, 90]
print("\nSublista3:\n",sublista3)
sublista4 = lista[::2]  # [10, 30, 50, 70, 90]
print("\nSublista4:\n",sublista4)
sublista5 = lista[1:8:3]  # [20, 50, 80]
print("\nSublista5:\n",sublista5)
sublista6 = lista[::-1]  # [90, 80, 70, 60, 50, 40, 30, 20, 10]
print("\nSublista6:\n",sublista6)
```

    Sublista1:
     [30, 40, 50]
    
    Sublista2:
     [10, 20, 30, 40]
    
    Sublista3:
     [60, 70, 80, 90]
    
    Sublista4:
     [10, 30, 50, 70, 90]
    
    Sublista5:
     [20, 50, 80]
    
    Sublista6:
     [90, 80, 70, 60, 50, 40, 30, 20, 10]
    

## Tuplas
### ¿Qué es una tupla?
Una tupla es una colección de datos similar a una lista, pero a diferencia de las listas, las tuplas son **inmutables**, lo que significa que no se pueden modificar después de haber sido creadas.

Las tuplas ocupan menos espacio en memoria que las listas y pueden ser más rápidas en ciertas operaciones debido a su inmutabilidad.

Son ideales para almacenar datos que no deben cambiar a lo largo del tiempo.

### Creación de tuplas
Podemos crear una tupla utilizando paréntesis `()` y separando los elementos con comas. Por ejemplo:


```python
tupla = (10, 20, 30, 40, 50)
print(tupla)
```

    (10, 20, 30, 40, 50)
    

### Acceso a los elementos de una tupla
Podemos acceder a los elementos de una tupla utilizando su índice entre corchetes `[]`. Por ejemplo:


```python
tupla = (10, 20, 30, 40, 50)
print(tupla[0])  # Primer elemento
print(tupla[2])  # Tercer elemento
print(tupla[-1])  # Último elemento
```

    10
    30
    50
    

También se puede utilizar el slicing para obtener subtuplas:


```python
print(tupla[-2]) # Penúltimo elemento
print(tupla[1:4]) # Subtupla desde el segundo hasta el cuarto elemento
print(tupla[::3]) # Subtupla con paso 3
print(tupla[::2]) # Subtupla con paso 2
```

    40
    (20, 30, 40)
    (10, 40)
    (10, 30, 50)
    

### Operadores, propiedades y métodos de las tuplas
* Podemos utilizar la función `len()` para obtener el tamaño de una tupla
* El operador `in` nos permite verificar si un elemento está presente en una tupla
* El operador `+` nos permite concatenar dos tuplas
* El operador `*` nos permite repetir una tupla un número determinado de veces
* El método `count()` cuenta cuántas veces aparece un elemento en la tupla
* El método `index()` devuelve el índice de la primera aparición de un elemento en la tu
* No disponemos de los métodos `append()`, `remove()`, `pop()`, `clear()` o `sort()` ya que las tuplas son inmutables

## Conjuntos
### ¿Qué es un conjunto?
Un conjunto es una colección de datos no ordenada y sin elementos duplicados. Los conjuntos son útiles cuando necesitamos almacenar elementos únicos y realizar operaciones matemáticas como la unión, intersección y diferencia
### Creación de conjuntos
Podemos crear un conjunto utilizando llaves `{}` o la función `set()`. Por ejemplo:


```python
conjunto = {20, 40, 60, 40, 80}  # Los elementos duplicados se eliminan automáticamente
print(conjunto)  # Muestra {40, 80, 20, 60}
```

    {40, 80, 20, 60}
    

### Limitaciones de los conjuntos
* No podemos acceder a un elemento concreto mediante un índice, ya que los conjuntos no están ordenados
* No podemos tener elementos duplicados en un conjunto
* No son indexables ni rebanables (slicing)
* No podemos utilizar el operador `in` para verificar si un elemento está presente en un conjunto
### Operaciones con conjuntos
#### Unión
Se puede utilizar el método `union()` o el operador `|` para obtener la unión de dos conjuntos:


```python
conjunto1 = {20, 40, 60, 40}
conjunto2 = {30, 40, 50, 60}
conjunto3 = conjunto1 | conjunto2
print(conjunto3)
conjunto4 = conjunto1.union(conjunto2)
print(conjunto4) # Mismo resultado
```

    {50, 20, 40, 60, 30}
    {50, 20, 40, 60, 30}
    

#### Intersección
Se puede utilizar el método `intersection()` o el operador `&` para obtener la intersección de dos conjuntos. La intersección es el conjunto de elementos que están presentes en ambos conjuntos:


```python
conjunto1 = {20, 40, 60, 40}
conjunto2 = {30, 40, 50, 60}
conjunto3 = conjunto1 & conjunto2
print(conjunto3)
conjunto4 = conjunto1.intersection(conjunto2)
print(conjunto4) # Mismo resultado
```

    {40, 60}
    {40, 60}
    

#### Diferencia
Se puede utilizar el método `difference()` o el operador `-` para obtener la diferencia entre dos conjuntos. La diferencia entre dos conjuntos A y B es el conjunto de elementos que están en A pero no en B.


```python
conjunto1 = {20, 40, 60, 40}
conjunto2 = {30, 40, 50, 60}
conjunto3 = conjunto1 - conjunto2
print(conjunto3)
conjunto4 = conjunto1.difference(conjunto2)
print(conjunto4) # Mismo resultado
```

    {20}
    {20}
    

#### Diferencia simétrica
Se puede utilizar el método `symmetric_difference()` o el operador `^` para obtener la diferencia simétrica entre dos conjuntos. La diferencia simétrica entre dos conjuntos A y B es el conjunto de elementos que están en A o en B, pero no en ambos.


```python
conjunto1 = {20, 40, 60, 40}
conjunto2 = {30, 40, 50, 60}
conjunto3 = conjunto1 ^ conjunto2
print(conjunto3)
conjunto4 = conjunto1.symmetric_difference(conjunto2)
print(conjunto4) # Mismo resultado
```

    {50, 20, 30}
    {50, 20, 30}
    

## Diccionarios
### ¿Qué es un diccionario?
Un diccionario es una estructura que almacena una colección de datos de tipo **clave**/**valor**.

Cada valor es accesible a través de su clave única, que puede ser de cualquier tipo. Las claves forman una colección inmutable y no ordenada.

Los valores, sin embargo, pueden ser de cualquier tipo y pueden repetirse. Los valores son mutables, lo que significa que pueden ser modificados después de haber sido creados.

### Creación de diccionarios
Podemos crear un diccionario utilizando llaves `{}` y separando las claves y valores con dos puntos `:`. Por ejemplo:


```python
capitales = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
print(capitales)
alumnos = {
    25 : "Ana",
    30 : "Luis",
    35 : "María"
}
print(alumnos)
```

    {'España': 'Madrid', 'Francia': 'París', 'Italia': 'Roma'}
    

A través de los diccionarios podemos formar estructuras avanzadas de datos:


```python
alumnos = {
    25: {
        'nombre': 'Ana',
        'edad': 20,
        'cursos': ['Matemáticas', 'Física']
    },
    30: {
        'nombre': 'Luis',
        'edad': 22,
        'cursos': ['Química', 'Biología']
    },
    35: {
        'nombre': 'María',
        'edad': 21,
        'cursos': ['Historia', 'Literatura']
    }
}

print(alumnos)

```

    {25: {'nombre': 'Ana', 'edad': 20, 'cursos': ['Matemáticas', 'Física']}, 30: {'nombre': 'Luis', 'edad': 22, 'cursos': ['Química', 'Biología']}, 35: {'nombre': 'María', 'edad': 21, 'cursos': ['Historia', 'Literatura']}}
    

### Acceso a los elementos de un diccionario
Podemos acceder a los valores de un diccionario utilizando su clave entre corchetes `[]`. Por ejemplo:


```python
capitales = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
print(capitales["España"])  # Muestra 'Madrid'
print(capitales["Italia"])  # Muestra 'Roma'
```

    Madrid
    Roma
    

### Añadir elementos a un diccionario
Podemos añadir un nuevo par clave/valor a un diccionario asignando un valor a una nueva clave:


```python
capitales ["Alemania"] = "Berlín"
print(capitales)  # Muestra {'España': 'Madrid', 'Francia': 'París', 'Italia': 'Roma', 'Alemania': 'Berlín'}
```

    {'España': 'Madrid', 'Francia': 'París', 'Italia': 'Roma', 'Alemania': 'Berlín'}
    

### Obtener el tamaño de un diccionario
Podemos obtener el número de pares clave/valor en un diccionario utilizando la función `len()`:


```python
capitales = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
tamaño = len(capitales)
print("El tamaño del diccionario es:", tamaño)  # Muestra 3
```

    El tamaño del diccionario es: 3
    

### Operaciones con diccionarios
#### Unión de diccionarios
Podemos unir dos diccionarios utilizando el método `update()` o el operador `|`


```python
capitales1 = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
capitales2 = {
    'Alemania': 'Berlín',
    'Portugal': 'Lisboa'
}
# Usando el operador |
capitales3 = capitales1 | capitales2
print(capitales3)
# Usando el método update()
capitales1.update(capitales2) # Modifica el original, capitales1
print(capitales1)
```

    {'España': 'Madrid', 'Francia': 'París', 'Italia': 'Roma', 'Alemania': 'Berlín', 'Portugal': 'Lisboa'}
    {'España': 'Madrid', 'Francia': 'París', 'Italia': 'Roma', 'Alemania': 'Berlín', 'Portugal': 'Lisboa'}
    

#### Eliminar elementos de un diccionario
Podemos eliminar un par clave/valor de un diccionario utilizando el método `pop()` el cual devuelve el valor asociado a la clave eliminada:


```python
capitales = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
valor = capitales.pop('Francia')
print("Valor eliminado:", valor)  # Muestra 'París'
print("Diccionario después de eliminar el elemento:", capitales)  # Muestra {'España': 'Madrid', 'Italia': 'Roma'}
```

    Valor eliminado: París
    Diccionario después de eliminar el elemento: {'España': 'Madrid', 'Italia': 'Roma'}
    

También podemos utilizar el método `del` para eliminar un par clave/valor sin devolver el valor:


```python
capitales = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
del capitales['Italia']
print("Diccionario después de eliminar el elemento:", capitales)  # Muestra {'España
```

    Diccionario después de eliminar el elemento: {'España': 'Madrid', 'Francia': 'París'}
    

El método `popitem()` elimina la última clave/valor añadida al diccionario y la devuelve como una tupla:


```python
capitales = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
clave_valor = capitales.popitem()
print("Clave/valor eliminado:", clave_valor)  # Muestra ('Italia', '
print("Diccionario después de eliminar el elemento:", capitales)  # Muestra {'España': 'Madrid', 'Francia': 'París'}
```

    Clave/valor eliminado: ('Italia', 'Roma')
    Diccionario después de eliminar el elemento: {'España': 'Madrid', 'Francia': 'París'}
    

#### Eliminar todos los elementos de un diccionario
Podemos eliminar todos los pares clave/valor de un diccionario utilizando el método `clear()`:


```python
capitales.clear()
print(capitales)  # Muestra {}
```

    {}
    

## Conversiones entre estructuras de datos
### Convertir a lista
La función `list()` nos permite convertir otras estructuras de datos a listas:


```python
tupla = (10, 20, 30, 40, 50)
lista = list(tupla)
print("Lista convertida desde tupla:", lista)
conjunto = {20, 40, 60, 80}
lista2 = list(conjunto)
print("Lista convertida desde conjunto:", lista2)
diccionario = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
lista3 = list(diccionario)
print("Lista convertida desde diccionario (claves):", lista3) # Solo coge las claves
```

    Lista convertida desde tupla: [10, 20, 30, 40, 50]
    Lista convertida desde conjunto: [40, 80, 20, 60]
    Lista convertida desde diccionario (claves): ['España', 'Francia', 'Italia']
    

En el caso de los diccionarios podemos convertir a lista tanto las claves como los valores utilizando los métodos `keys()` y `values()` respectivamente:


```python
diccionario = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
lista_claves = list(diccionario.keys())
print("Lista de claves:", lista_claves)
lista_valores = list(diccionario.values())
print("Lista de valores:", lista_valores)
```

    Lista de claves: ['España', 'Francia', 'Italia']
    Lista de valores: ['Madrid', 'París', 'Roma']
    

 Cualquier objeto que tenga sentido convertir a lista se puede convertir utilizando la función `list()`, como por ejemplo cadenas de texto o rangos:


```python
lista = range(1,10,2)
print("Lista convertida desde rango:", list(lista))
cadena = "Hola Mundo"
print("Lista convertida desde cadena de texto:", list(cadena))
```

    Lista convertida desde rango: [1, 3, 5, 7, 9]
    Lista convertida desde cadena de texto: ['H', 'o', 'l', 'a', ' ', 'M', 'u', 'n', 'd', 'o']
    

### Convertir a tupla
La función `tuple()` nos permite convertir otras estructuras de datos a tuplas:


```python
lista = [10, 20, 30, 40, 50]
tupla = tuple(lista)
print("Tupla convertida desde lista:", tupla)
conjunto = {20, 40, 60, 80}
tupla2 = tuple(conjunto)
print("Tupla convertida desde conjunto:", tupla2)
diccionario = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
tupla3 = tuple(diccionario)
print("Tupla convertida desde diccionario (claves):", tupla3) # Solo coge las claves
```

    Tupla convertida desde lista: (10, 20, 30, 40, 50)
    Tupla convertida desde conjunto: (40, 80, 20, 60)
    Tupla convertida desde diccionario (claves): ('España', 'Francia', 'Italia')
    

### Convertir a conjunto
La función `set()` nos permite convertir otras estructuras de datos a conjuntos:


```python
lista = [10, 20, 30, 40, 50, 20]
conjunto = set(lista)
print("Conjunto convertido desde lista:", conjunto)
tupla = (20, 40, 60, 80, 40)
conjunto2 = set(tupla)
print("Conjunto convertido desde tupla:", conjunto2)
diccionario = {
    'España': 'Madrid',
    'Francia': 'París',
    'Italia': 'Roma'
}
conjunto3 = set(diccionario)
print("Conjunto convertido desde diccionario (claves):", conjunto3) # Solo coge las claves
```

    Conjunto convertido desde lista: {40, 10, 50, 20, 30}
    Conjunto convertido desde tupla: {40, 80, 20, 60}
    Conjunto convertido desde diccionario (claves): {'Francia', 'Italia', 'España'}
    

### Convertir a diccionario
La función `dict()` nos permite convertir otras estructuras de datos a diccionarios, siempre que la estructura tenga posibilidad de formar pares clave/valor.

Por ejemplo podemos convertir una lista de pares de tuplas en un diccionario:


```python
capitales = [('España', 'Madrid'),
             ('Francia', 'París'),
             ('Italia', 'Roma')]
capitales_dict = dict(capitales)
print("Diccionario convertido desde lista de tuplas:", capitales_dict)
```

    Diccionario convertido desde lista de tuplas: {'España': 'Madrid', 'Francia': 'París', 'Italia': 'Roma'}
    

Podemos utilizar la función `zip()` para crear una lista de tuplas a partir de dos listas (una de claves y otra de valores) y luego convertirla a diccionario:


```python
paises = ['España', 'Francia', 'Italia']
capitales = ['Madrid', 'París', 'Roma']
diccionario = dict(zip(paises, capitales))
print("Diccionario convertido desde dos listas:", diccionario)
```

    Diccionario convertido desde dos listas: {'España': 'Madrid', 'Francia': 'París', 'Italia': 'Roma'}
    
