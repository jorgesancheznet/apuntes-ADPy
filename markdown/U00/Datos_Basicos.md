# Conceptos básicos de Python
## Contenidos
- [Uso de variables en Python](#uso-de-variables-en-python)
- [Introducción](#introducción)
- [Mostrar el tipo de dato de una variable](#mostrar-el-tipo-de-dato-de-una-variable)
- [Tipos de datos básicos en Python](#tipos-de-datos-básicos-en-python)
    - [Números enteros](#números-enteros)
        - [Expresiones con números enteros](#expresiones-con-números-enteros)
    - [Números decimales](#números-decimales)
    - [Valores booleanos](#valores-booleanos)
    - [Cadenas de caracteres. Strings.](#cadenas-de-caracteres-strings)
- [Comprobar el tipo de datos. `isinstance`](#comprobar-el-tipo-de-datos-isinstance)
- [Conversión de tipos](#conversión-de-tipos)
    - [Conversión a enteros](#conversión-a-enteros)
    - [Conversión a decimales](#conversión-a-decimales)
    - [Conversión a booleanos](#conversión-a-booleanos)
    - [Conversión a cadenas de texto](#conversión-a-cadenas-de-texto)
- [Operadores](#operadores)
    - [Operadores aritméticos](#operadores-aritméticos)
    - [Operadores de comparación](#operadores-de-comparación)
    - [Operadores lógicos](#operadores-lógicos)
    - [Asignación](#asignación)
    - [Concatenación de cadenas](#concatenación-de-cadenas)
    - [Operador de repetición](#operador-de-repetición)
- [Entrada y salida de datos](#entrada-y-salida-de-datos)
    - [Salida de datos](#salida-de-datos)
    - [Entrada de datos](#entrada-de-datos)
- [Librerías](#librerías)
    - [Librería de números aleatorios](#librería-de-números-aleatorios)
    - [Uso de librerías no estándar](#uso-de-librerías-no-estándar)


# Uso de variables en Python
## Introducción
Las variables en Python son contenedores que almacenan datos. A diferencia de otros lenguajes de programación, en Python no es necesario declarar el tipo de dato de una variable antes de usarla; Python lo determina automáticamente en función del valor asignado.


```python
a = 14 # Asignación de un valor entero a la variable 'a'
b = 3.5 # Asignación de un valor decimal (float) a la variable 'b'
nombre = "Juan" # Asignación de una cadena de texto (string) a la variable 'nombre'
es_estudiante = True # Asignación de un valor booleano a la variable 'es_estudiante'
```

El tipo de datos de una variables no es fijo, puede cambiar durante la ejecución del programa.


```python
a = 14
a = "Hola"
```

## Mostrar el tipo de dato de una variable
Se puede realizar mediante el método `type()`.


```python
a = 14
b = 3.5
c = "Hola"
print(type(a)) # Muestra: <class 'int'>
print(type(b)) # Muestra: <class 'float'>
print(type(c)) # Muestra: <class 'str'>
```

    <class 'int'>
    <class 'float'>
    <class 'str'>
    

# Tipos de datos básicos en Python
## Números enteros
El tipo de Python para números enteros es `int`. Sirve para almacenar valores sin decimales.

Python solo proporciona un tipo de datos para todos los enteros, sin importar su tamaño.

En Python los enteros pueden ser del tamaño que la memoria del sistema permita. No hay un límite específico como en otros lenguajes.


```python
a = 123456789012345678901234567890
print(a)
print(type(a)) # Muestra: <class 'int'>
```

    123456789012345678901234567890
    <class 'int'>
    

### Expresiones con números enteros
Podemos utilizar el carácter de guion bajo `_` para mejorar la legibilidad de los números grandes.


```python
a = 1_000_000_000
b = 2_500_000
print(a)
print(b)
```

    1000000000
    2500000
    

También podemos utilizar expresiones en hexadecimal, octal y binario para definir números enteros.


```python
a = 0x1A  # Hexadecimal (26 en decimal)
b = 0o12 # Octal (10 en decimal)
c = 0b1011 # Binario (11 en decimal)
print(a)
print(b)
print(c)
```

    26
    10
    11
    

## Números decimales
Los decimales usan el punto como separador decimal. Python solo proporciona un tipo de datos para los números decimales, que es `float`. Este tipo de datos se basa en la representación de punto flotante de doble precisión (64 bits), es equivalente al tipo `double` en otros lenguajes.


```python
a = 3.14159
b = 2.05
print(type(a)) # Muestra: <class 'float'>
print(type(b)) # Muestra: <class 'float'>
```

Se puede utilizar notación científica para representar números muy grandes o muy pequeños.


```python
a = 1.5e3  # 1.5 * 10^3 = 1500.0
b = 2.5e-4 # 2.5 * 10^-4 = 0.00025
print(a)
print(b)
```

    1500.0
    0.00025
    

# Valores booleanos
Representan dos valores posibles: `True` (verdadero) y `False` (falso). En Python, los valores booleanos son de tipo `bool`.

También se pueden obtener valores booleanos a partir de expresiones de comparación o expresiones lógicas. Todas ellas devuelven `True` o `False`.


```python
a = True
b = False
c = (5 > 3)  # Devuelve True
d = (2 == 4) # Devuelve False
print(a)
print(b)
print(c)
print(d)
```

    True
    False
    True
    False
    

Se consideran True los valores no nulos, el valores **None**, cadenas no vacías, listas no vacías, etc. Y se consideran False los valores nulos, cadenas vacías, listas vacías, etc.


```python
a = 12
b = 0
print(bool(a)) # Muestra: True
print(bool(b)) # Muestra: False
a = "Hola"
b = ""
print(bool(a)) # Muestra: True
print(bool(b)) # Muestra: False
```

# Cadenas de caracteres. Strings.
Las cadenas de caracteres en Python son secuencias de caracteres encerradas entre comillas simples (`'...'`) o comillas dobles (`"..."`). También se pueden usar comillas triples (`'''...'''` o `"""..."""`) para cadenas multilínea.


```python
texto1 = 'Hola, mundo!'
texto2 = "Python es genial."
texto3 = '''Esta es una cadena
multilínea.'''
texto4 = """Esta también
lo es."""
```

## Comprobar el tipo de datos. `isinstance`
La función `isinstance` permite comprobar si una variable es de un tipo específico.

Para ello se pasan dos argumentos: la variable a comprobar y el tipo de dato.




```python
x = 10
y = "Hola"
print(isinstance(x, int))    # Muestra: True
print(isinstance(y, str))    # Muestra: True
print(isinstance(x, float))  # Muestra: False
print(isinstance(y, bool))   # Muestra: False

```

    True
    True
    False
    False
    

## Conversión de tipos
### Conversión a enteros
Se pueden convertir datos de otros tipos a enteros utilizando la función `int()`.


```python
print(int(8.9)) # Muestra: 8
print(int("123")) # Muestra: 123
print(int(True)) # Muestra: 1
print(int(False)) # Muestra: 0
print(int("Hola")) # Error: ValueError
```

    8
    123
    1
    0
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Cell In[1], line 5
          3 print(int(True)) # Muestra: 1
          4 print(int(False)) # Muestra: 0
    ----> 5 print(int("Hola")) # Error: ValueError
    

    ValueError: invalid literal for int() with base 10: 'Hola'


### Conversión a decimales
Se pueden convertir datos de otros tipos a decimales utilizando la función `float()`.


```python
print(float(8)) # Muestra: 8.0
print(float("3.14")) # Muestra: 3.14
print(float(True)) # Muestra: 1.0
print(float(False)) # Muestra: 0.0
print(float("Hola")) # Error: ValueError
```

    8.0
    3.14
    1.0
    0.0
    


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Cell In[2], line 5
          3 print(float(True)) # Muestra: 1.0
          4 print(float(False)) # Muestra: 0.0
    ----> 5 print(float("Hola")) # Error: ValueError
    

    ValueError: could not convert string to float: 'Hola'


### Conversión a booleanos
Se pueden convertir datos de otros tipos a booleanos utilizando la función `bool()`.


```python
print(bool(8)) # Muestra: True
print(bool(0)) # Muestra: False
print(bool(3.14)) # Muestra: True
print(bool(0.0)) # Muestra: False
print(bool("Hola")) # Muestra: True
print(bool("")) # Muestra: False

```

### Conversión a cadenas de texto
Se pueden convertir datos de otros tipos a cadenas de texto utilizando la función `str()`.


```python
print(str(123)) # Muestra: '123'
print(str(3.14)) # Muestra: '3.14'
print(str(True)) # Muestra: 'True'
print(str(False)) # Muestra: 'False'
```

    123
    3.14
    True
    False
    

## Operadores
### Operadores aritméticos
Los operadores aritméticos permiten realizar operaciones matemáticas básicas.
- Suma: `+`
- Resta: `-`
- Multiplicación: `*`
- División: `/`
- División entera: `//`
- Módulo: `%`
- Exponenciación (potencias): `**`


```python
print(14/5)  # División normal, resultado: 2.8
print(14//5) # División entera, resultado: 2
print(14%5)  # Módulo, resultado: 4
print(2**3)  # Exponenciación, resultado: 8
```

    2.8
    2
    4
    8
    

### Operadores de comparación
Los operadores de comparación permiten comparar dos valores y devuelven un valor booleano (`True` o `False`).
- Igualdad: `==`
- Desigualdad: `!=`
- Mayor que: `>`
- Menor que: `<`
- Mayor o igual que: `>=`
- Menor o igual que: `<=`


```python
print(5 == 5)  # Muestra: True
print(5 != 3)  # Muestra: True
print(7 > 10)  # Muestra: False
print(4 < 8)   # Muestra: True
print(6 >= 6)  # Muestra: True
print(3 <= 2)  # Muestra: False
```

    True
    True
    False
    True
    True
    False
    

### Operadores lógicos
Los operadores lógicos permiten combinar expresiones booleanas.
- AND (y): `and`
- OR (o): `or`
- NOT (no): `not`


```python
print(True and False) # Muestra: False
print(True or False)  # Muestra: True
print(not True)       # Muestra: False
print(17>12 and 5<10)  # Muestra: True
print(3==3 or 4!=4)   # Muestra: True
```

### Asignación
Los operadores de asignación permiten asignar valores a las variables.
- Asignación simple: `=`
- Asignación con suma: `+=`
- Asignación con resta: `-=`
- Asignación con multiplicación: `*=`
- Asignación con división: `/=`
- Asignación con división entera: `//=`
- Asignación con módulo: `%=`
- Asignación con exponenciación: `**=`


```python
x = 29
x += 5  # Equivalente a x = x + 5
print(x) # Muestra: 34
x *= 2  # Equivalente a x = x * 2
print(x) # Muestra: 68
x //= 3  # Equivalente a x = x // 3
print(x) # Muestra: 22
```

### Concatenación de cadenas
Se puede utilizar el operador `+` para concatenar (unir) dos o más cadenas de texto. Requiere que todos los operandos sean cadenas de texto; si alguno no lo es, se debe convertir utilizando `str()`.


```python
print("Hola, " + "mundo!") # Muestra: Hola, mundo!
nombre = "Ana"
saludo = "Hola, " + nombre + "!"
print(saludo) # Muestra: Hola, Ana!
numero = 19
print("El número es: " + str(numero)) # Muestra: El número es: 19
```

    Hola, mundo!
    Hola, Ana!
    El número es: 19
    

### Operador de repetición
El operador `*` se puede usar para repetir una cadena de texto un número determinado de veces.


```python
texto = "Hola"
print(texto * 3)
print("-" * 40)
```

    HolaHolaHola
    ----------------------------------------
    

## Entrada y salida de datos
### Salida de datos
La función `print()` se utiliza para mostrar datos en la consola.

Podemos escribir varios valores separados por comas, y `print()` los mostrará con un espacio entre ellos.



```python
print("El valor de a es:", 14)
nombre = "Luis"
edad = 25
print("Nombre:", nombre, "Edad:", edad)
```

    El valor de a es: 14
    Nombre: Luis Edad: 25
    

Si deseamos que `print` no agregue un salto de línea al final, podemos usar el parámetro `end` y asignarle una cadena vacía `''` o cualquier otro carácter.


```python
print("Hola,", end=' ') # No agrega salto de línea y agrega un espacio
print("amigos")
```

    Hola, amigos
    

### Entrada de datos
La función `input()` se utiliza para leer datos desde la consola. Esta función siempre devuelve una cadena de texto.


```python
texto = input("Escribe un texto\n") # Muestra el mensaje y espera a que el usuario escriba algo
print("Tu texto es:", texto)
```

    Tu texto es: Este es mi texto
    

Si queremos leer un número, debemos convertir la cadena devuelta por `input()` al tipo de dato deseado utilizando `int()` o `float()`.


```python
numero = int(input("Escribe un número entero:\n"))
print("El número que escribiste es:", numero)
```

    El número que escribiste es: 260
    

## Librerías
Las librerías en Python son colecciones de módulos que contienen funciones y variables predefinidas para realizar tareas específicas. Podemos importar librerías utilizando la palabra clave `import`.


```python
import math # Importa la librería matemática
resultado = math.sqrt(16) # Utiliza la función sqrt() de la librería math
print("La raíz cuadrada de 16 es:", resultado)
print("El valor de pi es:", math.pi) # Utiliza la constante pi de la librería math
```

    La raíz cuadrada de 16 es: 4.0
    El valor de pi es: 3.141592653589793
    

Podemos importar solo funciones concretas de la librería utilizando la palabra clave `from`.


```python
from math import sqrt # Importa solo la función sqrt() de la librería math
resultado = sqrt(9) # Utiliza la función sqrt() directamente
print("La raíz cuadrada de 9 es:", resultado)
```

    La raíz cuadrada de 9 es: 3.0
    

Se le puede asignar un alias a una librería o función importada utilizando la palabra clave `as`.


```python
import math as m # Asigna el alias 'm' a la librería math
resultado = m.sqrt(9)
print("La raíz cuadrada de 9 es:", resultado)
```

    La raíz cuadrada de 9 es: 3.0
    

### Librería de números aleatorios
La librería `random` proporciona funciones para generar números aleatorios. SOn útiles en simulaciones, juegos y pruebas.

Algunas funciones:
- `random()`: Devuelve un número decimal aleatorio entre 0.0 y 1.0.
- `randint(a, b)`: Devuelve un número entero aleatorio entre `a` y `b` (ambos inclusive).


```python
import random
print("Número decimal aleatorio entre 0.0 y 1.0:", random.random())
print("Número entero aleatorio entre 1 y 10:", random.randint(1, 10))
```

    Número decimal aleatorio entre 0.0 y 1.0: 0.6207625372591672
    Número entero aleatorio entre 1 y 10: 7
    

### Uso de librerías no estándar
Python cuenta con un gestor de paquetes llamado `pip` que permite instalar librerías adicionales no incluidas en la instalación estándar de Python.

Para instalar una librería utilizando `pip`, se puede usar el siguiente comando en la terminal o línea de comandos:
```
pip install nombre_de_la_libreria
```
Por ejemplo, para instalar la librería `numpy`, que es muy utilizada para cálculos numéricos y manipulación de arrays, se usaría:
```
pip install numpy
```
