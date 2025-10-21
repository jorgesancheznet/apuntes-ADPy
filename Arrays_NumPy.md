# Uso de arrays en NumPy
## Índice
- [Características de los arrays](#características-de-los-arrays)
    - [Características principales](#características-principales)
    - [Ventajas sobre las listas de Python](#ventajas-sobre-las-listas-de-python)
    - [Operaciones comunes](#operaciones-comunes)
    - [Limitación principal](#limitación-principal)
- [Creación de arrays](#creación-de-arrays)
    - [Creación a partir de colecciones](#creación-a-partir-de-colecciones)
    - [Creación desde una lista](#creación-desde-una-lista)
    - [Creación desde una tupla](#creación-desde-una-tupla)
    - [Crear arrays desde rangos de números](#crear-arrays-desde-rangos-de-números)
    - [Relleno de arrays con un mismo valor](#relleno-de-arrays-con-un-mismo-valor)
    - [Creación de arrays vacíos](#creación-de-arrays-vacíos)
    - [Creación de arrays con valores aleatorios](#creación-de-arrays-con-valores-aleatorios)
- [Acceso y modificación de elementos](#acceso-y-modificación-de-elementos)
    - [Acceder a un elemento](#acceder-a-un-elemento)
- [Tipos de datos numéricos de los arrays](#tipos-de-datos-numéricos-de-los-arrays)
    - [Tipos de datos específicos de los arrays de NumPy](#tipos-de-datos-específicos-de-los-arrays-de-numpy)
    - [Propiedad dtype](#propiedad-dtype)
    - [Tipos de datos numéricos en NumPy](#tipos-de-datos-numéricos-en-numpy)
    - [Conversión a otro tipo de dato](#conversión-a-otro-tipo-de-dato)
    - [Crear arrays con un tipo de dato específico](#crear-arrays-con-un-tipo-de-dato-específico)
- [Propiedades de los arrays](#propiedades-de-los-arrays)
    - [size](#size)
    - [ndim](#ndim)
    - [shape](#shape)
    - [itemsize](#itemsize)
    - [nbytes](#nbytes)
- [Operaciones con arrays](#operaciones-con-arrays)
    - [Operaciones de cambio de forma](#operaciones-de-cambio-de-forma)
    - [Indexaciones](#indexaciones)
    - [Indexación sofisticada](#indexación-sofisticada)
    - [Vistas y copias](#vistas-y-copias)
    - [Operaciones vectorizadas (broadcasting)](#operaciones-vectorizadas-broadcasting)
    - [Operaciones de cálculo de totales](#operaciones-de-cálculo-de-totales)
    - [Otras operaciones útiles](#otras-operaciones-útiles)

La línea de código siguiente importa la librería NumPy y la asigna al alias **np**, que es el alias convencionalmente utilizado en la comunidad científica de Python. Esto permite acceder a las funciones y clases de NumPy utilizando el prefijo **np.**
Es imprescindible ejecutar esta línea para poder ejecutar cualquiera de las celdas de código de este cuaderno.


```python
import numpy as np # Siempre hay que ejecutar este código antes de poder ejecutar el resto de celdas
```



## Características de los arrays
Los arrays de NumPy son estructuras de datos fundamentales para computación científica en Python:

### Características principales:

* **Homogéneos**: Todos los elementos deben ser del mismo tipo de dato
* **Tamaño fijo**: Una vez creado, el tamaño no puede cambiar (a diferencia de las listas)
* **Multidimensionales**: Pueden tener 1D, 2D, 3D o más dimensiones
* **Eficientes**: Operaciones optimizadas en C, mucho más rápidas que las listas de Python
* **Operaciones vectorizadas**: Permiten operaciones elemento a elemento sin bucles explícitos

### Ventajas sobre las listas de Python

* **Rendimiento**: Entre 10-100x más rápidas para operaciones numéricas
* **Menos memoria**: Almacenamiento más compacto
* **Broadcasting** : Operaciones entre arrays de diferentes formas
* **Funciones matemáticas** : Amplia biblioteca de funciones optimizadas

### Operaciones comunes

- Indexación y slicing avanzado
- Operaciones aritméticas elemento a elemento
- Álgebra lineal (multiplicación de matrices, determinantes, etc.)
- Estadísticas (media, mediana, desviación estándar)
- Reshape y transposición

### Limitación principal

No pueden contener tipos de datos mixtos de forma eficiente (a diferencia de las listas de Python).

# Creación de arrays

## Creación a partir de colecciones

### Creación desde una lista


```python
a = np.array([10,20,30,40,50])
print(a)
```

    [10 20 30 40 50]


### Creación desde una tupla


```python
a = np.array((10,20,30,40,50))
print(a)
```

    [10 20 30 40 50]


Los datos deben de ser homogéneos. Si hay arrays y strings combinados, todos los datos se convierten a strings


```python
a = np.array([10,20,'Hola',40,True,2.9])
print(a)
```

    ['10' '20' 'Hola' '40' 'True' '2.9']



```python

```

## Crear arrays desde rangos de números


```python
a = np.arange(1,10)
print(a)

b = np.arange(1,10,2)
print(b)

c = np.arange(10,1,-1)
print(c)
```

    [1 2 3 4 5 6 7 8 9]
    [1 3 5 7 9]
    [10  9  8  7  6  5  4  3  2]


El método linspace crea arrays desde un rango, pero en este caso indica el rango y el número de elementos que deseamos


```python
a = np.linspace(1,10,3)
print(a) # 3 valores entre 1 y 10 separados por la misma cantidad

b = np.linspace(1,101,51)
print(b) # 51 valores entre 1 y 101 separados por la misma cantidad
```

    [ 1.   5.5 10. ]
    [  1.   3.   5.   7.   9.  11.  13.  15.  17.  19.  21.  23.  25.  27.
      29.  31.  33.  35.  37.  39.  41.  43.  45.  47.  49.  51.  53.  55.
      57.  59.  61.  63.  65.  67.  69.  71.  73.  75.  77.  79.  81.  83.
      85.  87.  89.  91.  93.  95.  97.  99. 101.]


### Relleno de arrays con un mismo valor


```python
a = np.zeros(5)
print(a)
```

    [0. 0. 0. 0. 0.]


Relleno de unos


```python
a = np.ones(5)
print(a)
```

    [1. 1. 1. 1. 1.]


Rellenar de un valor cualquiera


```python
a = np.full(5,6) # 5 seises
print(a)
```

    [6 6 6 6 6]


Arrays de varias dimensiones rellenos con un mismo valor


```python
a = np.zeros((3,4)) # Array de 3 filas y 4 columnas relleno de ceros
print(a)

b = np.full((2,5),9) # Array de 2 filas y 5 columnas relleno de nueves
print(b)
```

    [[0. 0. 0. 0.]
     [0. 0. 0. 0.]
     [0. 0. 0. 0.]]
    [[9 9 9 9 9]
     [9 9 9 9 9]]


## Creación de arrays vacíos
El método **empty** crea un array sin inicializar. Los valores que contiene son indeterminados (lo que haya en la memoria en ese momento)


```python
a = np.empty(5)
print(a) # Es impredecible lo que contiene el array a
```

    [ 1.    2.75  6.   10.75 17.  ]


## Creación de arrays con valores aleatorios
El módulo **random** de NumPy permite crear arrays con valores aleatorios.
Posee varios métodos para generar este tipo de arrays.
###  randint
Genera un array con valores enteros aleatorios dentro de un rango especificado



```python
a = np.random.randint(1,10,5) # 5 valores enteros aleatorios entre 1 y 9
print(a)
a = np.random.randint(1,100,(3,4)) # Array de 3 filas y 4 columnas con valores entre 1 y 99
print(a)
```

    [1 8 2 2 4]
    [[80 90 36 74]
     [67 62 40 74]
     [11 35 80 55]]


### random
Genera un array con valores decimales aleatorios entre 0 y 1


```python
a = np.random.random(5) # 5 valores decimales aleatorios entre 0 y 1
print(a)
a = np.random.random((2,3)) # Array de 2 filas y 3 columnas con valores entre 0 y 1
print(a)
```

    [0.84453385 0.74732011 0.53969213 0.58675117 0.96525531]
    [[0.60703425 0.27599918 0.29627351]
     [0.16526694 0.01563641 0.42340148]]


### Otras distribuciones aleatorias
El módulo random posee otros métodos para generar arrays con distribuciones específicas y útiles para cálculos estadísticos.
Un ejemplo de ello es el método **standard_normal** que genera un array con valores decimales aleatorios siguiendo una distribución normal estándar (media 0 y desviación típica 1)


```python
a = np.random.standard_normal(5) # 5 valores decimales aleatorios con distribución normal estándar
print(a)
a = np.random.standard_normal((2,3)) # Array de 2 filas y 3 columnas con valores con distribución normal estándar
print(a)
```

    [-1.05683555  0.53269907  1.68188475  1.05290483  1.57430606]
    [[-2.08348299 -0.49540658 -0.46915604]
     [-0.90232818 -0.05155832  0.9624893 ]]


Otras funciones son:
* **normal(loc, scale, size)**: Genera valores con distribución normal con media *loc* y desviación típica *scale*
* **uniform(low, high, size)**: Genera valores con distribución uniforme entre *low* y *high*
* **binomial(n, p, size)**: Genera valores con distribución binomial con *n* ensayos y probabilidad *p*
* **poisson(lam, size)**: Genera valores con distribución de Poisson con media *lam*
* **choice(a, size, replace, p)**: Genera una muestra aleatoria de tamaño *size* a partir del array *a*, con o sin reemplazo y con probabilidades *p*
* **shuffle(x)**: Mezcla aleatoriamente los elementos del array *x*
* **permutation(x)**: Devuelve una permutación aleatoria de los elementos del array *x*

### Cambio de la semilla
El módulo random permite establecer una semilla para el generador de números aleatorios. La semilla es el valor inicial que se utiliza para generar la secuencia de números aleatorios. Si se establece la misma semilla, se obtendrá la misma secuencia de números aleatorios cada vez que se ejecute el código.
El método **seed** permite establecer la semilla.


```python
a = np.random.seed(42) # Establece la semilla a 42
a = np.random.randint(1,10,5) # 5 valores enteros aleatorios entre 1 y 9
print(a) # Siempre escribirá los mismos valores al usar la misma semilla
```

Se recomienda actualmente usar el objeto Generator para generar números aleatorios, ya que ofrece mejores prestaciones y más funcionalidades.
Para ello se utiliza el método **default_rng** que crea un generador de números aleatorios.
Los generadores aportan métodos para crear arrays con diferentes distribuciones de probabilidad.


```python
rng = np.random.default_rng(42) # Crea un generador con semilla 42
a = rng.integers(1,10,5) # 5 valores enteros aleatorios entre 1 y 9
print(a) # Siempre escribirá los mismos valores al usar la misma semilla
a = rng.random((2,3)) # Array de 2 filas y 3 columnas con valores entre 0 y 1
print(a)
a = rng.normal(0,1,(2,3)) # Array de 2 filas y 3 columnas con distribución normal (media 0, desviación típica 1)
print(a)
```

# Acceso y modificación de elementos

## Acceder a un elemento
Se puede acceder utilizando índices, empezando por 0. El índice se usa entre corchetes []. Para arrays multidimensionales, se usan comas para separar los índices de cada dimensión.


```python
a = np.array([10,20,30,40,50])
print(a[2]) # Escribe 30
```

    30


Los arrays son mutables, podemos cambiar el valor de los elementos


```python
a[2] = 90
print(a) # Escribe [10 20 90 40 50]

```

    [10 20 90 40 50]


Acceso a elementos en arrays multidimensionales


```python
a = np.array([[10,20,30,40],
              [50,60,70,80],
              [90,100,110,120]])
print(a[1,2]) # Accede a la segunda fila, tercera columna (valor 70)

```

    70


Podemos usar valores negativos en los índices para contar desde el final


```python
a = np.array([10,20,30,40])
print(a[-1]) # Accede al último elemento, escribe 40
print(a[-2]) # Accede al penúltimo elemento, escribe 30
```

    40
    30


# Tipos de datos numéricos de los arrays
## Tipos de datos específicos de los arrays de NumPy
- Hay que tener en cuenta que lo que se pretende de esta librería es precisión y velocidad
- Los tipos numéricos existentes en Python (**integer** y **float**) son demasiado genéricos, especialmente en el caso de integer.
- NumPy usa tipos mucho más especializados
- Son más parecidos a los que utilizan lenguajes de alto rendimiento como por ejemplo **C**.
- Son mucho más eficientes

## Propiedad dtype
Cada array tiene una propiedad llamada **dtype** que indica el tipo de datos de sus elementos


```python
a = np.array([10,20,30,40,50])
print(a.dtype) # Escribe el tipo entero por defecto, int64 o int32 según el sistema operativo
```

    int64


m## Tipos de datos numéricos en NumPy
### Enteros
| **Tipo**   | **Valores**                                                  | **Rango**        |
| ---------- | ------------------------------------------------------------ | ---------------- |
| **bool**   | Solo  True o False. Ocupa 1 bit                              | True  o False    |
| **int**    | Entero  por defecto en el sistema (pueden ser int32 o int64) | ...              |
| **int8**   | Enteros  pequeños de un byte                                 | -128  a 127      |
| **int16**  | Enteros  de dos bytes                                        | -32768  a 32767  |
| **int32**  | Enteros  de 4 bytes                                          | de  -231 a 231-1 |
| **int64**  | Enteros  de 8 bytes                                          | de  -263 a 263-1 |
| **uint8**  | Enteros  positivos de 1 byte                                 | 0  a 255         |
| **uint16** | Enteros  positivos de 2 bytes                                | 0  a 65535       |
| **uint32** | Enteros  positivos de 4 bytes                                | 0  a a 232-1     |
| **uint64** | Enteros  positivos de 8 bytes                                | 0  a a 264-1     |

### Decimales de coma flotante
| **Tipo**      | **Valores**                                    |
| ------------- | ---------------------------------------------- |
| **float**     | Decimal  de coma flotante genérico. Es float64 |
| **float16**   | Números  decimales de coma flotante de 2 bytes |
| **float32**   | Números  decimales de coma flotante de 4 bytes |
| **float63**   | Números  decimales de coma flotante de 8 bytes |
| **complex**   | Números  complejos genéricos. Es complex128    |
| **complex64** | Número  complejo formado por dos float32       |
| **complex64** | Número  complejo formado por dos float64       |

## Conversión a otro tipo de dato


```python
x = np.array([19, 25])
print(np.float64(x))
```

    [19. 25.]


## Crear arrays con un tipo de dato específico
La mayoría de funciones de creación de arrays dispone de un parámetro llamado dtype para especificar el tipo.


```python
array = np.array([1,2,3], dtype="float64")
print(array)
```

    [1. 2. 3.]


# Propiedades de los arrays
## size
Indica el tamaño de un array


```python
a = np.arange(1,11)
b = np.array([[2, 3, 4],[5, 6, 7]])
print(a.size) # Escribe 10
print(b.size) # aunque tiene dos dimensiones cuenta elementos (6)

```

    10
    6


## ndim
Indica el número de dimensiones del array


```python
a = np.arange(1,11)
b = np.array([[2, 3, 4],[5, 6, 7]])
print(a.ndim) # Escribe 1
print(b.ndim) # Escribe 2, dos dimensiones
```

    1
    2


## shape
Indica la forma del array, es decir, el número de elementos en cada dimensión. Es más completo que size y ndim


```python
a = np.arange(1,11)
b = np.array([[2, 3, 4],[5, 6, 7]])
print(a.shape) # Escribe (10,)
print(b.shape) # Escribe (2,3)

```

    (10,)
    (2, 3)


## itemsize
Indica el tamaño en bytes de cada elemento del array
## nbytes
Indica el tamaño total en bytes del array (es como itemsize * size)


```python
a = np.random.randint(1,10,100, dtype="int64") # Array de 100 elementos con valores entre 1 y 10
print(a.itemsize) # Cada elemento ocupa 8 bytes (int64)
print(a.nbytes) # Como hay 100 elementos, ocupa 800 bytes

```

    8
    800


# Operaciones con arrays
## Operaciones de cambio de forma
### reshape
Cambia la forma del array sin cambiar sus datos. No modifica el array original, devuelve otro.
El nuevo tamaño debe ser compatible con el número total de elementos.


```python
a = np.array([1,2,3,4,5,6,7,8,9])
a2 = a.reshape(3,3)
print(a2)
```

    [[1 2 3]
     [4 5 6]
     [7 8 9]]



```python
a = np.array([[2, 3, 4],[5, 6, 7]])
a2 = a.reshape(6)
print(a2)
```

    [2 3 4 5 6 7]


## flatten
Convierte un array multidimensional en un array unidimensional. No modifica el array original, devuelve otro.


```python
a = np.array([[2, 3, 4],[5, 6, 7]])
a2 = a.flatten()
print(a2)
# Este código es equivalente
a2 = a.reshape(a.size)
print(a2)
```

    [2 3 4 5 6 7]
    [2 3 4 5 6 7]


### ravel
Funciona como flatten. Pero lo que devuelve es una vista del array original, no una copia. Por tanto, si se modifica el array resultante, se modifica también el original.



```python
a = np.array([[2, 3, 4],[5, 6, 7]])
a2 = a.ravel()
print(a2)
```

    [2 3 4 5 6 7]


### transpose
Transpone un array, es decir, intercambia filas por columnas. No modifica el array original, devuelve otro.


```python
a = np.array([[2, 3, 4],[5, 6, 7]])
a2 = a.transpose()
print(a2)
```

    [[2 5]
     [3 6]
     [4 7]]


## Indexaciones
### Indexaciones simples
Los arrays de NumPy permiten las operaciones de indexación de las listas de Python.
El formato es:
```
array[inicio:fin:pasos]
```
Des esta forma, podemos seleccionar desde el índice inicio hasta el índice fin e indicar el salto entre elemento y elemento
Si no se indican *pasos*, los elementos se recogen de uno en uno



```python
a = np.arange(1,11)
print("array original (a) ->",a)
print("a[2:5] ->",a[2:5])
print("a[:5] ->",a[:5])
print("a[2:] ->",a[2:])
print("a[2:7:2] ->",a[2:7:2])
print("a[::-1] ->",a[::-1])
print("a[-3:] ->",a[-3:])

```

    array original (a) -> [ 1  2  3  4  5  6  7  8  9 10]
    a[2:5] -> [3 4 5]
    a[:5] -> [1 2 3 4 5]
    a[2:] -> [ 3  4  5  6  7  8  9 10]
    a[2:7:2] -> [3 5 7]
    a[::-1] -> [10  9  8  7  6  5  4  3  2  1]
    a[-3:] -> [ 8  9 10]


### Arrays multidimensionales
Los arrays multidimensionales permiten indexaciones más complejas, pero el formato es similar.


```python
b= np.arange(1,13).reshape(4,3) # Array de 4 filas y 3 columnas
print("Array b original \n",b)
print("b[1] \n",b[1]) # Toma la segunda fila
print("b[:,1]\n",b[:,1]) # Toma la segunda columna
print("b[1,:2]\n",b[1,:2]) # Toma los dos primeros elementos de la segunda fila
print("b[:2,:2]\n",b[:2,:2]) # 2 primeras filas y columnas
```

    Array b original 
     [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]
    b[1] 
     [4 5 6]
    b[:,1]
     [ 2  5  8 11]
    b[1,:2]
     [4 5]
    b[:2,:2]
     [[1 2]
     [4 5]]


## Indexación sofisticada
### Filtros booleanos
Se pueden realizar operaciones lógicas con arrays, devolviendo un array de booleanos. Este array se puede usar para filtrar los elementos del array original.


```python
a = np.arange(1,11)
print("a>5 -> ",a>5) # Devuelve un array de booleanos con valores
            # True para los mayores de 5 y False para los menores o iguales
```

    a>5 ->  [False False False False False  True  True  True  True  True]


Podemos, con ayuda de ese tipo de resultado, filtrar los elementos del array original de modo que se muestren solo los elementos que cumplen la condición


```python
print("a[a>5] -> ",a[a>5])
```

    a[a>5] ->  [ 6  7  8  9 10]


### Arrays de índices
Se pueden usar arrays de índices para seleccionar elementos específicos de un array.


```python
a = np.arange(1,21).reshape(5,4)
print("Array a original \n",a)
indices =  [1,2]
print("Array usando índices [1,2]\n",a[indices])
```

    Array a original 
     [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]
     [13 14 15 16]
     [17 18 19 20]]
    Array usando índices [1,2]
     [[ 5  6  7  8]
     [ 9 10 11 12]]


## Vistas y copias
### Vistas
Cuando se crea un nuevo array a partir de otro mediante indexación (o _slicing_), se crea una vista del array original. Esto significa que ambos arrays comparten los mismos datos en memoria. Si se modifica uno, se modifica el otro.


```python
a  = np.arange(1,13).reshape(4,3)
print("Array original, a:\n",a)
vista = a[:2,1:3] # Vista de las dos primeras filas y dos últimas columnas
print("Vista :\n",vista)
vista[0,0] = 99 # Modificamos un elemento de la vista
print("Array original modificado \n",a) # El array original también se ha modificado
```

    Array original, a:
     [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]
    Vista :
     [[2 3]
     [5 6]]
    Array original modificado 
     [[ 1 99  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]


### Copias
Si se desea crear un nuevo array independiente del original, se debe usar el método copy(). De esta forma, las modificaciones en el nuevo array no afectan al original.


```python
a  = np.arange(1,13).reshape(4,3)
print("Array original, a:\n",a)
copia = a[:2,1:3].copy() # Copia de las dos primeras filas y dos últimas columnas
print("Copia :\n",copia)
copia[0,0] = 88 # Modificamos un elemento de la copia
print("Array original tras modificar la copia \n",a) # El array original no se ha modificado
```

    Array original, a:
     [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]
    Copia :
     [[2 3]
     [5 6]]
    Array original tras modificar la copia 
     [[ 1  2  3]
     [ 4  5  6]
     [ 7  8  9]
     [10 11 12]]


## Operaciones vectorizadas (_broadcasting_)
### Operaciones aritméticas básicas
Las operaciones aritméticas básicas (suma, resta, multiplicación, división) se aplican elemento a elemento en arrays de NumPy. No es necesario usar bucles explícitos.


```python
a = np.arange(10,70,10).reshape(2,3)
print("Array original, a:\n",a)
b = np.arange(5,35,5).reshape(2,3)
print("Array original, b:\n",b)
# Operaciones
print("Suma a + b:\n",a + b)
print("Resta a - b:\n",a - b)
print("Multiplicación a * b:\n",a * b)
print("División a / b:\n",a / b)
print("Resto a % b:\n",a % b)
```

    Array original, a:
     [[10 20 30]
     [40 50 60]]
    Array original, b:
     [[ 5 10 15]
     [20 25 30]]
    Suma a + b:
     [[15 30 45]
     [60 75 90]]
    Resta a - b:
     [[ 5 10 15]
     [20 25 30]]
    Multiplicación a * b:
     [[  50  200  450]
     [ 800 1250 1800]]
    División a / b:
     [[2. 2. 2.]
     [2. 2. 2.]]
    Resto a % b:
     [[0 0 0]
     [0 0 0]]


### Operaciones con escalares
Las operaciones aritméticas también se pueden realizar entre un array y un escalar. El escalar se aplica a cada elemento del array.


```python
b = a + 3
print("Array 'b' tras b = a + 3:\n",b)
b = a * 2
print("Array 'b' tras b = a * 2:\n",b)
```

    Array 'b' tras b = a + 3:
     [[ 35  55  75]
     [ 95 115 135]]
    Array 'b' tras b = a * 2:
     [[ 64 104 144]
     [184 224 264]]


Es posible incluso aplicar operaciones de asignación


```python
a += 3
print("Array 'a' tras a += 3:\n",a)
a *= 2
print("Array 'a' tras a *= 2:\n",a)
```

    Array 'a' tras a += 3:
     [[16 26 36]
     [46 56 66]]
    Array 'a' tras a *= 2:
     [[ 32  52  72]
     [ 92 112 132]]


### Funciones matemáticas
NumPy proporciona una amplia gama de funciones matemáticas que se aplican a cada elemento del array.


```python
a = np.arange(1,13).reshape(3,4)
print("Array original, a:\n",a)
print("Raíz cuadrada de a:\n",np.sqrt(a))
print("Exponencial de a:\n",np.exp(a))
print("Logaritmo natural de a:\n",np.log(a))
print("Seno de a:\n",np.sin(a))
print("Coseno de a:\n",np.cos(a))
print("Tangente de a:\n",np.tan(a))
```

    Array original, a:
     [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]]
    Raíz cuadrada de a:
     [[1.         1.41421356 1.73205081 2.        ]
     [2.23606798 2.44948974 2.64575131 2.82842712]
     [3.         3.16227766 3.31662479 3.46410162]]
    Exponencial de a:
     [[2.71828183e+00 7.38905610e+00 2.00855369e+01 5.45981500e+01]
     [1.48413159e+02 4.03428793e+02 1.09663316e+03 2.98095799e+03]
     [8.10308393e+03 2.20264658e+04 5.98741417e+04 1.62754791e+05]]
    Logaritmo natural de a:
     [[0.         0.69314718 1.09861229 1.38629436]
     [1.60943791 1.79175947 1.94591015 2.07944154]
     [2.19722458 2.30258509 2.39789527 2.48490665]]
    Seno de a:
     [[ 0.84147098  0.90929743  0.14112001 -0.7568025 ]
     [-0.95892427 -0.2794155   0.6569866   0.98935825]
     [ 0.41211849 -0.54402111 -0.99999021 -0.53657292]]
    Coseno de a:
     [[ 0.54030231 -0.41614684 -0.9899925  -0.65364362]
     [ 0.28366219  0.96017029  0.75390225 -0.14550003]
     [-0.91113026 -0.83907153  0.0044257   0.84385396]]
    Tangente de a:
     [[ 1.55740772e+00 -2.18503986e+00 -1.42546543e-01  1.15782128e+00]
     [-3.38051501e+00 -2.91006191e-01  8.71447983e-01 -6.79971146e+00]
     [-4.52315659e-01  6.48360827e-01 -2.25950846e+02 -6.35859929e-01]]


## Operaciones de cálculo de totales
Se pueden utilizar operaciones para calcular totales, medias, mínimos, máximos, etc.



```python
a = np.array([[10,20,30],[40,50,60],[70,80,90]])
print("Array original, a:\n",a)
print("Suma total de todos los elementos:\n", np.sum(a))
print("Media de todos los elementos:\n", np.mean(a))
print("Valor mínimo:\n", np.min(a))
print("Valor máximo:\n", np.max(a))
print("Desviación estándar:\n", np.std(a))
print("Mediana:\n", np.median(a))
print("Percentil 25:\n", np.percentile(a, 25))
print("Todos los valores verdaderos en a > 50:\n", np.all(a > 50))
print("Algún valor verdadero en a > 50:\n", np.any(a > 50))
```

    Array original, a:
     [[10 20 30]
     [40 50 60]
     [70 80 90]]
    Suma total de todos los elementos:
     450
    Media de todos los elementos:
     50.0
    Valor mínimo:
     10
    Valor máximo:
     90
    Desviación estándar:
     25.81988897471611
    Mediana:
     50.0
    Percentil 25:
     30.0
    Todos los valores verdaderos en a > 50:
     False
    Algún valor verdadero en a > 50:
     True


## Otras operaciones útiles
### Concatenación
Se pueden concatenar varios arrays en uno solo usando la función concatenate().


```python
a = np.array([1,2,3])
b = np.array([4,5,6])
c = np.concatenate((a,b))
print("Array concatenado c:\n",c)
```

    Array concatenado c:
     [1 2 3 4 5 6]


Se pueden concatenar arrays de dos dimensiones, siempre que las dimensiones sean compatibles


```python
a= np.arange(1,7).reshape(2,3)
print("Array original, a:\n",a)
b= np.arange(7,10).reshape(1,3)
print("Array original, b:\n",b)
print("Concatenación de a y b:\n",np.concatenate((a,b)))
```

    Array original, a:
     [[1 2 3]
     [4 5 6]]
    Array original, b:
     [[7 8 9]]
    Concatenación de a y b:
     [[1 2 3]
     [4 5 6]
     [7 8 9]]


### Concatenación de arrays de diferentes dimensiones
El método **vstack** permite concatenar arrays apilándolos verticalmente (uno encima de otro)



```python
a= np.arange(1,7).reshape(2,3)
print("Array original, a:\n",a)
b = np.array([10,20,30])
print("Array original, b:\n",b)
print("Array apilado con vstack:\n",np.vstack([a,b]))
```

    Array original, a:
     [[1 2 3]
     [4 5 6]]
    Array original, b:
     [10 20 30]
    Array apilado con vstack:
     [[ 1  2  3]
     [ 4  5  6]
     [10 20 30]]


El método **hstack** permite concatenar arrays apilándolos horizontalmente (uno al lado de otro)


```python
a= np.arange(1,7).reshape(2,3)
print("Array original, a:\n",a)
b = np.array([[10],[20]])
print("Array original, b:\n",b)
print("Array apilado con hstack:\n",np.hstack([a,b]))
```

    Array original, a:
     [[1 2 3]
     [4 5 6]]
    Array original, b:
     [[10]
     [20]]
    Array apilado con hstack:
     [[ 1  2  3 10]
     [ 4  5  6 20]]


### Trocear arrays (_slicing_)
El método **split** permite dividir un array en varios subarrays. Para ello recibe una lista con los índices donde se desea hacer el corte.


```python
a = np.arange(1,10)
print("Array original, a:\n",a)
print("Arrays resultantes del troceado:\n",np.split(a,[3,5]))

```

    Array original, a:
     [1 2 3 4 5 6 7 8 9]
    Arrays resultantes del troceado:
     [array([1, 2, 3]), array([4, 5]), array([6, 7, 8, 9])]


Mediante la operación de desempaquetado se pueden asignar los subarrays resultantes a variables independientes


```python
a = np.arange(1,10)
print("Array original, a:\n",a)
x, y, z = np.split(a,[3,5])
print("X ->",x)
print("Y ->",y)
print("Z ->",z)
```

    Array original, a:
     [1 2 3 4 5 6 7 8 9]
    X -> [1 2 3]
    Y -> [4 5]
    Z -> [6 7 8 9]


El método **vsplit** permite dividir un array multidimensional en varios subarrays dividiendo por filas (división vertical).


```python
a = np.arange(1,13).reshape(3,4)
print("Array original, a:\n",a)
x,y = np.vsplit(a,[2]) # Divide en dos arrays, el primero con las dos primeras filas
print("x:\n",x)
print("Yy:\n",y)
```

    Array original, a:
     [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]]
    x:
     [[1 2 3 4]
     [5 6 7 8]]
    Yy:
     [[ 9 10 11 12]]


El método **hsplit** permite dividir un array multidimensional en varios subarrays dividiendo por columnas (división horizontal).


```python
a = np.arange(1,13).reshape(3,4)
print("Array original, a:\n",a)
x,y = np.hsplit(a,[2]) # Divide en dos arrays, el primero con las dos primeras columnas
print("x:\n",x)
```

    Array original, a:
     [[ 1  2  3  4]
     [ 5  6  7  8]
     [ 9 10 11 12]]
    x:
     [[ 1  2]
     [ 5  6]
     [ 9 10]]


### Operaciones de conjuntos
Se pueden realizar operaciones de conjuntos como unión, intersección y diferencia utilizando funciones específicas de NumPy.


```python
a = np.array([10,20,30,40,50])
b = np.array([30,40,50,60,70])
print("Array a:\n",a)
print("Array b:\n",b)
print("Unión de a y b:\n",np.union1d(a,b))
print("Intersección de a y b:\n",np.intersect1d(a,b))
print("Diferencia de a y b (elementos en a no en b):\n",np.setdiff1d(a,b))
print("Operación xor simétrica (elementos en a o b pero no en ambos):\n",np.setxor1d(a,b))
```

    Array a:
     [10 20 30 40 50]
    Array b:
     [30 40 50 60 70]
    Unión de a y b:
     [10 20 30 40 50 60 70]
    Intersección de a y b:
     [30 40 50]
    Diferencia de a y b (elementos en a no en b):
     [10 20]
    Operación xor simétrica (elementos en a o b pero no en ambos):
     [10 20 60 70]


Las operaciones conjuntos eliminan automáticamente los elementos duplicados y ordenan el resultado.
Estas operaciones también funcionan con arrays multidimensionales, pero se consideran los arrays como conjuntos de filas.


```python
a = np.array([[1,2],[3,4],[5,6]])
b = np.array([[3,4],[5,6],[7,8]])
print("Array a:\n",a)
print("Array b:\n",b)
print("Unión de a y b:\n",np.union1d(a,b))
print("Intersección de a y b:\n",np.intersect1d(a,b))
print("Diferencia de a y b (filas en a no en b):\n",np.setdiff1d(a,b))
print("Operación xor simétrica (filas en a o b pero no en ambos):\n",np.setxor1d(a,b))

```

    Array a:
     [[1 2]
     [3 4]
     [5 6]]
    Array b:
     [[3 4]
     [5 6]
     [7 8]]
    Unión de a y b:
     [1 2 3 4 5 6 7 8]
    Intersección de a y b:
     [3 4 5 6]
    Diferencia de a y b (filas en a no en b):
     [1 2]
    Operación xor simétrica (filas en a o b pero no en ambos):
     [1 2 7 8]


### Ordenar arrays
El método **sort** permite ordenar los elementos de un array. Por defecto, ordena en orden ascendente.


```python
a = np.array([4,8,4,7,2,5,1])
print("Array a:\n",a)
a.sort()
print("Array a ordenado:\n",a)
```

    Array a:
     [4 8 4 7 2 5 1]
    Array a ordenado:
     [1 2 4 4 5 7 8]


El método **argsort** devuelve los índices que ordenarían el array. No modifica el array original.


```python
a = np.array([4,8,4,7,2,5,1])
print("Array a ordenado:\n",a)
i = a.argsort()
print("Array de índices para ordenar a:\n",i)
print("Array a ordenado usando los índices:\n",a[i])
```

    Array a ordenado:
     [4 8 4 7 2 5 1]
    Array de índices para ordenar a:
     [6 4 0 2 5 3 1]
    Array a ordenado usando los índices:
     [1 2 4 4 5 7 8]


En los arrays multidimensionales, también funciona el mñetodo sort, pero se puede especificar el eje (filas o columnas) por el que se desea ordenar utilizando el parámetro axis. A este parámetro se le puede asignar el valor 0 (ordenar por columnas) o 1 (ordenar por filas). Si no se especifica, ordena por filas (axis=1)


```python
a = np.array([[6,8,4],
              [3,2,7],
              [9,3,1]])
print("Array a:\n",a)
b = a.copy() # copia para no perder los datos originales
b.sort()
print("Array b ordenado tal cual (ordena por filas)",b)
b = a.copy()
print("Array b ordenado por columnas (axis=0):\n",np.sort(b,axis=0))
```

    Array a:
     [[6 8 4]
     [3 2 7]
     [9 3 1]]
    Array b ordenado tal cual (ordena por filas) [[4 6 8]
     [2 3 7]
     [1 3 9]]
    Array b ordenado por columnas (axis=0):
     [[3 2 1]
     [6 3 4]
     [9 8 7]]

