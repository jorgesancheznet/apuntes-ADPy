# Estructuras de Control
## Contenidos
- [Condicionales](#Condicionales)
  - [Sentencia `if` simple](#Sentencia-if-simple)
  - [Sentencia `if-else` (if compuesto)](#Sentencia-if-else-(if-compuesto))
  - [Sentencia `if-elif-else` (if múltiple o anidado)](#Sentencia-if-elif-else-(if-múltiple-o-anidado))
- [Iteraciones (Bucles)](#Iteraciones-(Bucles))
  - [Bucle `while`](#Bucle-while)
  - [Sentencia `for`](#Sentencia-for)
  - [Sentencia `break`](#Sentencia-break)
  - [Sentencia `continue`](#Sentencia-continue)
- [Recorrido de colecciones](#Recorrido-de-colecciones)
  - [Recorrer listas, tuplas y conjuntos](#Recorrer-listas,-tuplas-y-conjuntos)
  - [Recorrido de diccionarios](#Recorrido-de-diccionarios)
- [Manejo de excepciones](#Manejo-de-excepciones)
  - [Sentencia `try-except`](#Sentencia-try-except)


## Condicionales
### Sentencia `if` simple
Se trata de una estructura que permite ejecutar un bloque de código si se cumple una condición determinada.

**Sintaxis:**
```python
if condición:
    # bloque de código a ejecutar si la condición es verdadera
```
**Ejemplo:**


```python
numero = int(input("Introduce un numero: "))
if numero > 0:
    print("El número es positivo")
```

    El número es positivo
    

### Sentencia `if-else` (if compuesto)
Permite ejecutar un bloque de código si se cumple una condición y otro bloque si no se cumple.

**Sintaxis:**
```python
if condición:
    # bloque de código si la condición es verdadera
else:
    # bloque de código si la condición es falsa
```
**Ejemplo:**


```python
numero = int(input("Introduce un numero: "))
if numero > 0:
    print("El número es positivo")
else:
    print("El número es cero o negativo")
```

    El número es cero o negativo
    

### Sentencia `if-elif-else` (if múltiple o anidado)
Permite evaluar múltiples condiciones de manera secuencial. Se basa en el uso de `if` para la primera condición, `elif` (contracción de `else-if`) para establecer condiciones a revisar en el caso de que no se cumplan las anteriores y `else` para el caso en el que no se cumpla ninguna de las condiciones anteriores.

**Sintaxis:**
```python
if condición1:
    # bloque de código si condición1 es verdadera
elif condición2:
    # bloque de código si condición2 es verdadera
# más posibles elif...
else:
    # bloque de código si ninguna condición es verdadera
```
**Ejemplo:**


```python
nota = int(input("Introduce tu nota (0-10): "))
if nota >= 9:
    print("Sobresaliente")
elif nota >= 7:
    print("Notable")
elif nota >= 5:
    print("Aprobado")
else:
    print("Suspenso")
```

    Notable
    

## Iteraciones (Bucles)
### Bucle `while`
Se utiliza para repetir un bloque de código mientras una condición sea verdadera.
**Sintaxis:**
```python
while condición:
    # bloque de código a repetir
```
**Ejemplo:**


```python
i = 1
while i <= 10: # Imprime números del 1 al 10
    print(i)
    i += 1
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    

### Sentencia `for`
Se utiliza para iterar sobre una secuencia (como una lista, tupla, diccionario, conjunto o cadena de texto).
**Sintaxis:**
```python
for elemento in secuencia:
    # bloque de código a ejecutar para cada elemento
```
**Ejemplo:**


```python
for i in range(1, 11): # Imprime números del 1 al 10
    print(i)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    


```python
for i in range(1,11,2): # Imprime números impares del 1 al 10
    print(i)
```

    1
    3
    5
    7
    9
    

### Sentencia `break`
Se utiliza para salir de un bucle antes de que haya terminado su ciclo natural.
**Ejemplo:**


```python
for i in range(1, 11):
    if i == 6:
        break  # Sale del bucle cuando i es 6
    print(i)
```

### Sentencia `continue`
Se utiliza para saltar la iteración actual y continuar con la siguiente iteración del bucle.
**Ejemplo:**


```python
for i in range(1,11):
    if i % 2 == 0:
        continue  # Salta los números pares
    print(i)  # Imprime solo números impares
```

No es conveniente abusar de las instrucciones `break` y `continue`, ya que pueden dificultar la lectura y comprensión del código. Es preferible utilizarlas con moderación y solo cuando realmente mejoren la claridad del código.

## Recorrido de colecciones
### Recorrer listas, tuplas y conjuntos
Para recorrer estos tipos de colecciones, se puede utilizar un bucle `for`.
**Ejemplo con lista:**


```python
ciudades = ["Madrid", "Barcelona", "Valencia"]
for ciudad in ciudades:
    print(ciudad)
```

    Madrid
    Barcelona
    Valencia
    

Para poder acceder al índice de cada elemento durante el recorrido, se puede utilizar la función `enumerate()`, la cual devuelve tanto el índice como el valor del elemento en cada iteración.
**Ejemplo con `enumerate()`:**


```python
ciudades = ["Madrid", "Barcelona", "Valencia"]
for indice, ciudad in enumerate(ciudades):
    print(f"Ciudad {indice}: {ciudad}")
```

    Ciudad 0: Madrid
    Ciudad 1: Barcelona
    Ciudad 2: Valencia
    

Las tuplas y los conjuntos se recorren de la misma manera que las listas.
**Ejemplo con tupla:**


```python
tupla = (1, 2, 3)
for numero in tupla:
    print(numero)
```

    1
    2
    3
    

### Recorrido de diccionarios
Para recorrer un diccionario, se pueden utilizar diferentes métodos dependiendo de si se desea acceder a las claves, los valores o ambos.
#### Recorrer claves
Podemos recorrer solo las claves del diccionario utilizando un bucle `for`:


```python
capitales = {"España": "Madrid",
             "Francia": "París",
             "Italia": "Roma"}
for pais in capitales:
    print(pais)
```

    España
    Francia
    Italia
    

Las claves del diccionario también se pueden obtener utilizando el método `keys()`:



```python
capitales = {"España": "Madrid",
             "Francia": "París",
             "Italia": "Roma"}
for pais in capitales.keys():
    print(pais)
```

    España
    Francia
    Italia
    

Los valores están accesibles mediante el método `values()`:


```python
capitales = {
    "España": "Madrid",
    "Francia": "París",
    "Italia": "Roma"
}
for ciudad in capitales.values():
    print(ciudad)
```

    Madrid
    París
    Roma
    

El método `items()` permite recorrer tanto las claves como los valores simultáneamente:


```python
capitales = {
    "España": "Madrid",
    "Francia": "París",
    "Italia": "Roma"
}
for pais, ciudad in capitales.items():
    print(f"La capital de {pais} es {ciudad}")
```

    La capital de España es Madrid
    La capital de Francia es París
    La capital de Italia es Roma
    

## Manejo de excepciones
### Sentencia `try-except`
Se utiliza para manejar errores y excepciones que pueden ocurrir durante la ejecución del programa, permitiendo que el programa continúe funcionando en lugar de detenerse abruptamente.
**Sintaxis:**
```python
try:
    # bloque de código que puede generar una excepción
except TipoDeExcepcion:
    # bloque de código para manejar la excepción
```
**Ejemplo:**


```python
# Ejemplo de manejo de excepciones
try:
    numero = int(input("Introduce un número: "))
    resultado = 10 / numero
    print(f"El resultado es: {resultado}")
except ValueError: # Captura errores de conversión de tipo
    print("Error: Debes introducir un número válido.")
except ZeroDivisionError: # Captura errores de división por cero
    print("Error: No se puede dividir por cero.")
```

    Error: No se puede dividir por cero.
    

La excepción genérica `Exception` puede capturar cualquier tipo de excepción, pero es recomendable manejar excepciones específicas para un mejor control de errores.

Si se usan varias excepciones y, entre ellas la genérica `Exception`, esta última debe ir al final de todas las excepciones específicas para asegurar que las específicas tienen prioridad.
