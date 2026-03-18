# Visualización de datos
## Índice
- [Introducción a la visualización de datos](#introducción-a-la-visualización-de-datos)
- [Visualización con Matplotlib](#visualización-con-matplotlib)
    - [Instalación de Matplotlib](#instalación-de-matplotlib)
    - [Utilización de Matplotlib en Jupyter](#utilización-de-matplotlib-en-jupyter)
    - [Generación de gráficos con Matplotlib](#generación-de-gráficos-con-matplotlib)
        - [Gráficos de líneas](#gráficos-de-líneas)
        - [Personalización de gráficos](#personalización-de-gráficos)
        - [Datos en ambos ejes](#datos-en-ambos-ejes)
        - [Gráficos de barras](#gráficos-de-barras)
        - [Gráficos de sectores](#gráficos-de-sectores)
        - [Histogramas](#histogramas)
        - [Gráficos de dispersión](#gráficos-de-dispersión)
        - [Gráficos de burbuja](#gráficos-de-burbuja)
- [Generación de gráficos con la función `plot()`de `pandas`](#generación-de-gráficos-con-la-función-`plot()`de-`pandas`)
- [Visualización con Seaborn](#visualización-con-seaborn)
    - [Instalación de Seaborn](#instalación-de-seaborn)
    - [Trazados lm](#trazados-lm)
    - [Gráficos de barra](#gráficos-de-barra)
    - [Gráficos de distribución](#gráficos-de-distribución)
    - [Gráficos de caja](#gráficos-de-caja)
    - [Gráficos de violín](#gráficos-de-violín)
    - [Diagrama de barras de frecuencia](#diagrama-de-barras-de-frecuencia)
    - [Gráficos de conjunto](#gráficos-de-conjunto)
    - [Mapas de calor](#mapas-de-calor)


## Introducción a la visualización de datos

La visualización de datos es una parte fundamental del análisis de datos, ya que permite comunicar información de manera efectiva y descubrir patrones ocultos en los datos. En Python, existen varias bibliotecas populares para la visualización de datos, como Matplotlib, Seaborn y Plotly.

Mediante la fase de visualización podremos:
- Explorar los datos de manera visual para identificar patrones, tendencias y relaciones entre variables.
- Comunicar los resultados de manera efectiva a través de gráficos y visualizaciones.
- Tomar decisiones informadas basadas en la interpretación de los datos.
- Detectar valores atípicos y errores en los datos.
- Comparar diferentes conjuntos de datos o categorías de manera visual.

A la hora de elaborar un gráfico es importante tener en cuenta:
- El tipo de gráfico adecuado para el tipo de datos que se está visualizando.
- La claridad y simplicidad del gráfico para facilitar su interpretación.
- El uso de colores y etiquetas para mejorar la comprensión del gráfico.
- La inclusión de títulos y leyendas para proporcionar contexto y facilitar la interpretación del gráfico.
- La consistencia en el diseño de los gráficos para facilitar la comparación entre diferentes visualizaciones.
- La audiencia a la que se dirige el gráfico, adaptando el nivel de detalle y complejidad según sea necesario.
- La ética en la visualización de datos, evitando manipular o distorsionar la información para transmitir un mensaje específico.
- La interactividad en los gráficos, especialmente cuando se presentan datos complejos o grandes conjuntos de datos, para permitir a los usuarios explorar y analizar la información de manera más efectiva.
- La actualización y mantenimiento de los gráficos a medida que se obtienen nuevos datos o se realizan cambios en el análisis, para garantizar que la visualización siga siendo relevante y precisa.
- La documentación y el código fuente de los gráficos, para facilitar la reproducibilidad y el entendimiento de cómo se generaron las visualizaciones.

En resumen, un gráfico debe de ser:
- Claro
- Conciso
- Informativo
- Atractivo visualmente
- Relevante
- Ético
- Interactivo (si es necesario)
- Actualizado
- Documentado
- Adaptado a la audiencia

## Visualización con Matplotlib

Matplotlib es una biblioteca de visualización de datos en Python que proporciona una amplia gama de funciones para crear gráficos estáticos, animados e interactivos. Es una de las bibliotecas más populares para la visualización de datos en Python y se utiliza ampliamente en la comunidad científica y de análisis de datos.

### Instalación de Matplotlib

Para instalar Matplotlib, puedes usar pip, el gestor de paquetes de Python o bien conda, el gestor de paquetes de Anaconda.

Mediante `pip` se haría de esta forma:
```bash
pip install matplotlib
```

Mediante `conda` se haría de esta forma (suponiendo que hemos activado nuestro entorno de trabajo:
```bash
conda install matplotlib
```


### Utilización de Matplotlib en Jupyter
Si queremos comenzar a utilizar Matplotlib en nuestro cuaderno de Jupyter, es necesario importar la biblioteca y configurar el entorno para mostrar los gráficos dentro del cuaderno.

Dentro de la librería Matplotlib, el módulo `pyplot` es el que se utiliza para crear gráficos de manera sencilla. Para importar `pyplot`, se suele utilizar la siguiente convención:


```python
import matplotlib.pyplot as plt
```

Para asegurar que los gráficos se muestren dentro del cuaderno de Jupyter, es necesario utilizar el comando mágico `%matplotlib inline`. Este comando configura Matplotlib para que los gráficos se rendericen directamente en el cuaderno, en lugar de abrirse en una ventana separada.


```python
%matplotlib inline
```

Además necesitaremos las librerías `numpy` y `pandas` para poder utilizar datos de ejemplo en nuestros gráficos.


```python
import pandas as pd
import numpy as np
```

### Generación de gráficos con Matplotlib
#### Gráficos de líneas
Los gráficos de líneas son útiles para mostrar la evolución de una variable a lo largo del tiempo o para comparar varias series de datos. Para crear un gráfico de líneas con Matplotlib, se puede utilizar la función `plt.plot()`.

Ejemplo de gráfico sencillo:




```python
datos = np.arange(10) # Array con valores del 0 al 9
plt.plot(datos) # Crear un gráfico de líneas con los datos
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_10_0.png)
    


#### Personalización de gráficos
La función `plt.plot()` también permite personalizar el gráfico. Algunos parámetros habituales para personalizar el gráfico de líneas incluyen:
- `color`: Especifica el color de la línea. Puede ser un nombre de color (por ejemplo, 'red', 'blue', 'green') o un código hexadecimal (por ejemplo, '#FF0000' para rojo).
- `linestyle`: Define el estilo de la línea. Puede ser sólido ('-'), punteado ('--'), con puntos (':') o sin línea ('').
- `label`: Proporciona una etiqueta para la línea, que se puede usar en la leyenda del gráfico.
- `linewidth`: Especifica el grosor de la línea.


```python
plt.plot(datos, color='red', linestyle='--', label='Datos de ejemplo', linewidth=2) # Crear un gráfico de líneas personalizado
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_12_0.png)
    


Los gráficos puede incluir datos de varias series. En ese caso podemos realizar varias llamadas a `plt.plot()` para cada serie de datos que queramos incluir en el gráfico. De esa manera podremos personalizar cada serie de datos de forma independiente.


```python
datos1 = [1, 2, 3, 4, 5]
datos2 = [2, 4, 6, 8, 10]
plt.plot(datos1, color='blue', linestyle='-', label='Serie 1') # Gráfico de la primera serie
plt.plot(datos2, color='orange', linestyle='--', label='Serie 2')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_14_0.png)
    


También disponemos de los siguientes métodos para personalizar el gráfico:
- `plt.title()`: Agrega un título al gráfico.
- `plt.xlabel()`: Agrega una etiqueta al eje x.
- `plt.ylabel()`: Agrega una etiqueta al eje y.
- `plt.legend()`: Muestra la leyenda del gráfico, que es útil para identificar las diferentes series de datos. El nombre de las series se especifica mediante el parámetro `label` en cada llamada a `plt.plot()`. Se dispone además de un parámetro `loc` para configurar la ubicación de la leyenda en el gráfico, con opciones como 'upper left', 'upper right', 'lower left', 'lower right', 'center', entre otras.
- `plt.grid()`: Agrega una cuadrícula al gráfico para facilitar la lectura de los valores.
- `plt.xticks()`: Permite configurar las etiquetas del eje x, especificando una lista de valores para las posiciones de las etiquetas en el eje X.
- `plt.yticks()`: Permite configurar las etiquetas del eje y, especificando una lista de valores para las posiciones de las etiquetas en el eje Y.


```python
datos1 = [1, 2, 3, 4, 5]
datos2 = [2, 4, 6, 8, 10]
plt.plot(datos1, color='blue', linestyle='-', label='Serie 1') # Gráfico de la primera serie
plt.plot(datos2, color='orange', linestyle='--', label='Serie 2')
plt.title("Gráfico de líneas personalizado") # Agregar título al gráfico
plt.xlabel("Eje X") # Agregar etiqueta al eje x
plt.ylabel("Eje Y") # Agregar etiqueta al eje y
plt.legend() # Mostrar la leyenda del gráfico
plt.grid() # Agregar cuadrícula al gráfico
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_16_0.png)
    


### Datos en ambos ejes
En el ejemplo anterior, los datos se asignan automáticamente a los ejes x e y. SIn embargo, lo habitual es que queramos asignar datos específicos a cada eje. Para ello, podemos pasar dos listas o arrays a la función `plt.plot()`, donde el primer argumento corresponde a los valores del eje x y el segundo argumento corresponde a los valores del eje y.


```python
# Datos para la primera serie
x = [1,3,5,7,9,11]
y = [10,25,35,33,41,59]
plt.plot(x,y,label="S1",color="blue")
# Datos para la segunda serie
x = [2,4,6,8,10,12]
y = [15,29,32,33,38,55]
plt.plot(x,y,label="S2",color="red")
plt.xlabel("Eje X")
plt.ylabel("Eje Y")
plt.title("Gráfico de líneas con dos series de datos")
plt.legend()
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_18_0.png)
    


Veamos ya un ejemplo con datos reales utilizando la biblioteca `pandas` para cargar un conjunto de datos y luego visualizarlos con Matplotlib. En este caso, utilizaremos un conjunto de datos de ejemplo sobre dos jugadores de baloncesto. Cada serie refleja los puntos y rebotes realizados en cada partido. El conjunto de datos se puede cargar en un DataFrame de `pandas` y luego se pueden crear gráficos para comparar el rendimiento de los dos jugadores a lo largo de la temporada.

Esto es posible porque las series pueden ser arrays o listas, pero también pueden ser columnas de un DataFrame de `pandas`. De esta manera, podemos utilizar los datos almacenados en un DataFrame para crear gráficos de líneas con Matplotlib.


```python
dfJugador1 = pd.DataFrame({
    "Partido": [1, 2, 3, 4, 5],
    "Puntos": [20, 25, 30, 28, 35],
    "Rebotes": [5, 7, 6, 8, 10]
})
dfJUgador2 = pd.DataFrame({
    "Partido": [1, 2, 3, 4, 5],
    "Puntos": [15, 18, 22, 20, 27],
    "Rebotes": [4, 6, 5, 7, 9]
})
# Generamos la primera serie de datos para el jugador 1
plt.plot(dfJugador1["Partido"], dfJugador1["Puntos"], label="Pts Jugador 1", color="blue")
plt.plot(dfJUgador2["Partido"], dfJUgador2["Puntos"], label="Pts Jugador 2", color="red")
plt.xlabel("Partido")
plt.ylabel("Puntos")
plt.title("Puntos por partido de los jugadores")
plt.legend()
plt.show()
# Generamos la segunda serie de datos para el jugador 1
plt.plot(dfJugador1["Partido"], dfJugador1["Rebotes"], label="Rebotes Jugador 1", color="blue")
plt.plot(dfJUgador2["Partido"], dfJUgador2["Rebotes"], label="Rebotes Jugador 2", color="red")
plt.xlabel("Partido")
plt.ylabel("Rebotes")
plt.title("Rebotes por partido de los jugadores")
plt.legend()
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_20_0.png)
    



    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_20_1.png)
    


### Gráficos de barras
Los gráficos de barras son útiles para comparar diferentes categorías o grupos de datos. Para crear un gráfico de barras con Matplotlib, se puede utilizar la función `plt.bar()`.


```python
categorias = ['A', 'B', 'C', 'D', 'E']
valores = [10, 15, 7, 12, 20]
plt.bar(categorias, valores, color='blue') # Crear un gráfico de barras
plt.xlabel('Categorías') # Agregar etiqueta al eje x
plt.ylabel('Valores') # Agregar etiqueta al eje y
plt.title('Gráfico de barras') # Agregar título al gráfico
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_22_0.png)
    


Vamos otro ejemplo usando los datos de los jugadores de baloncesto, visto anteriormente, pero esta vez utilizando un gráfico de barras para comparar los puntos y rebotes de ambos jugadores en cada partido.


```python
dfJugador1 = pd.DataFrame({
    "Partido": [1, 2, 3, 4, 5],
    "Puntos": [20, 25, 30, 28, 35],
    "Rebotes": [5, 7, 6, 8, 10]
})
dfJUgador2 = pd.DataFrame({
    "Partido": [1, 2, 3, 4, 5],
    "Puntos": [15, 18, 22, 20, 27],
    "Rebotes": [4, 6, 5, 7, 9]
})
# Gráfico de barras para puntos
plt.bar(dfJugador1["Partido"] - 0.2, dfJugador1["Puntos"], width=0.4, label="Pts Jugador 1", color="blue")
# Se resta 0.2 a los valores del eje x para el jugador 1 y se suma 0.2 para el jugador 2, de esa manera las barras de ambos jugadores no se superponen y se pueden comparar fácilmente.
plt.bar(dfJUgador2["Partido"] + 0.2, dfJUgador2["Puntos"], width=0.4, label="Pts Jugador 2", color="red")
plt.xlabel("Partido")
plt.ylabel("Puntos")
plt.title("Puntos por partido de los jugadores")
plt.legend()
plt.show()

```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_24_0.png)
    



```python
# Gráfico de barras para rebotes
plt.bar(dfJugador1["Partido"] - 0.2, dfJugador1["Rebotes"], width=0.4, label="Rebotes Jugador 1", color="blue")
plt.bar(dfJUgador2["Partido"] + 0.2, dfJUgador2["Rebotes"], width=0.4, label="Rebotes Jugador 2", color="red")
plt.xlabel("Partido")
plt.ylabel("Rebotes")
plt.title("Rebotes por partido de los jugadores")
plt.legend()
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_25_0.png)
    


### Gráficos de sectores
Los gráficos de sectores, también conocidos como gráficos de pastel, son útiles para mostrar la proporción de cada categoría en relación con el total. Para crear un gráfico de sectores con Matplotlib, se puede utilizar la función `plt.pie()`.


```python
ventas = [30, 20, 15, 10, 25]
categorias = ['Producto A', 'Producto B', 'Producto C', 'Producto D', 'Producto E']
plt.pie(ventas, labels=categorias, autopct='%1.1f%%', startangle=90) # Crear un gráfico de sectores
plt.title('Distribución de ventas por producto') # Agregar título al gráfico
plt.axis('equal') # Asegurar que el gráfico sea circular
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_27_0.png)
    


El método `pie()`posee parámetros para personalizar el gráfico de sectores, como:
- `labels`: Especifica las etiquetas para cada sector del gráfico. Recibe una lista de cadenas que corresponden a cada categoría representada en el gráfico.
- `autopct`: Muestra el porcentaje de cada sector en el gráfico. El formato se indica mediante una cadena de formato que funciona de esta forma:
    - El símbolo `%` indica el inicio del formato.
    - El siguiente número indica el ancho mínimo de caracteres para indicar el número entero.
    - Tras el símbolo `.` se indica el número de decimales que se desean mostrar.
    - Un símbolo de `%` al final indica que se desea mostrar el símbolo de porcentaje después del número. Se indican dos símbolos para que se tome como literal el símbolo de porcentaje, ya que un solo símbolo se interpreta como el inicio del formato.
- `startangle`: Especifica el ángulo de inicio del gráfico de sectores. El valor se indica en grados, donde 0 grados corresponde a la posición de las 3 en punto en un reloj. Un valor positivo hace que el gráfico gire en sentido contrario a las agujas del reloj, mientras que un valor negativo hace que gire en sentido horario.
- `colors`: Permite especificar los colores de cada sector del gráfico. Recibe una lista de colores que corresponden a cada categoría representada en el gráfico. Los colores pueden ser especificados mediante nombres de color (por ejemplo, 'red', 'blue', 'green') o códigos hexadecimales (por ejemplo, '#FF0000' para rojo).
- `explode`: Permite resaltar un sector del gráfico separándolo del centro. Recibe una lista de valores que corresponden a cada categoría representada en el gráfico. Un valor de 0 indica que el sector no se separa, mientras que un valor positivo indica la distancia a la que se separa el sector del centro del gráfico. Por ejemplo, un valor de 0.1 separaría el sector un 10% del radio del gráfico.
- `shadow`: Agrega una sombra al gráfico de sectores para darle un efecto tridimensional. Recibe un valor booleano (True o False) que indica si se desea agregar la sombra o no.
- `labeldistance`: Especifica la distancia a la que se colocan las etiquetas de cada sector del gráfico. Recibe un valor numérico que indica la distancia en relación al radio del gráfico. Por ejemplo, un valor de 1.1 colocaría las etiquetas a una distancia del 110% del radio del gráfico.
- `pctdistance`: Especifica la distancia a la que se colocan los porcentajes de cada sector del gráfico. Recibe un valor numérico que indica la distancia en relación al radio del gráfico. Por ejemplo, un valor de 0.6 colocaría los porcentajes a una distancia del 60% del radio del gráfico.
- `axis`: Permite configurar los ejes del gráfico. En el caso de los gráficos de sectores, es común utilizar `plt.axis('equal')` para asegurar que el gráfico sea circular, ya que por defecto Matplotlib puede ajustar la forma del gráfico según el espacio disponible, lo que podría resultar en un gráfico de sectores ovalado.

En el ejemplo anterior se usó el parámetro `autopct` para mostrar el porcentaje de cada sector en el gráfico, y el parámetro `startangle` para iniciar el gráfico desde las 12 en punto. Además, se utilizó el método `axis('equal')` para asegurar que el gráfico sea circular.

Veamos un ejemplo donde se usa `explode` para resaltar un sector del gráfico, `shadow` para agregar una sombra al gráfico y `colors` para personalizar los colores de cada sector.


```python
ventas = [30, 20, 15, 10, 25]
categorias = ['Producto A', 'Producto B', 'Producto C', 'Producto D', 'Producto E']
colores = ['#FF9999', '#66B3FF', '#99FF99', '#FFCC99', '#FFD700'] # Colores personalizados para cada sector
explode = [0, 0, 0, 0.3, 0] # Resaltar el cuarto sector del gráfico
plt.pie(ventas, labels=categorias, autopct='%1.1f%%', startangle=90, colors=colores, explode=explode, shadow=True) # Crear un gráfico de sectores personalizado
plt.title('Distribución de ventas por producto') # Agregar título al gráfico
plt.axis('equal') # Asegurar que el gráfico sea circular
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_29_0.png)
    


### Histogramas
Los histogramas son útiles para mostrar la distribución de una variable numérica. Por defecto muestran un gráfico de barras donde cada barra representa un rango de valores (bin) y la altura de la barra representa la frecuencia de los datos que caen dentro de ese rango. Es muy útil para visualizar la forma de la distribución de los datos, identificar patrones y detectar valores atípicos.

Para crear un histograma con Matplotlib, se puede utilizar la función `plt.hist()`.

En ese método, el parámetro `bins` permite especificar el número de bins o intervalos en los que se agrupan los datos para crear el histograma. Un valor más alto de `bins` resultará en un histograma más detallado, mientras que un valor más bajo resultará en un histograma más generalizado. El número óptimo de bins puede depender del tamaño y la distribución de los datos, por lo que a menudo es útil experimentar con diferentes valores para encontrar el que mejor represente la distribución de los datos.



```python
datos = np.random.randn(1000) # Generar 1000 datos aleatorios con distribución de campana de gauss
plt.hist(datos, bins=30, color='blue', edgecolor='black') # Crear un histograma con 30 bins
plt.xlabel('Valor') # Agregar etiqueta al eje x
plt.ylabel('Frecuencia') # Agregar etiqueta al eje y
plt.title('Histograma de datos aleatorios') # Agregar título al gráfico
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_31_0.png)
    


### Gráficos de dispersión
Los gráficos de dispersión son útiles para mostrar la relación entre dos variables numéricas. Para crear un gráfico de dispersión con Matplotlib, se puede utilizar la función `plt.scatter()`.


```python
x = np.random.rand(100) # Generar 100 datos aleatorios para el eje x
y = np.random.rand(100) # Generar 100 datos aleatorios para el eje y
plt.scatter(x, y, color='blue') # Crear un gráfico de dispersión
plt.xlabel('Variable X') # Agregar etiqueta al eje x
plt.ylabel('Variable Y') # Agregar etiqueta al eje y
plt.title('Gráfico de dispersión de datos aleatorios') # Agregar título al gráfico
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_33_0.png)
    


Para un ejemplo más realista, podemos utilizar un conjunto de datos de ejemplo sobre la relación entre el número de horas de estudio y las calificaciones obtenidas por un grupo de estudiantes. El gráfico de dispersión nos permitirá visualizar si existe una correlación entre estas dos variables.


```python
horasInvertidas = [5, 4, 2, 9, 10, 8, 9, 12, 13, 10, 12, 16, 18, 9]
calificaciones = [7.0, 7.0, 7.0, 7.5, 8.0, 8.0, 8.5, 8.5, 9.0, 9.5, 9.5, 10, 10, 10]
plt.scatter(horasInvertidas, calificaciones, color='blue') # Crear un gráfico de dispersión
plt.xlabel('Horas de estudio') # Agregar etiqueta al eje x
plt.ylabel('Calificaciones') # Agregar etiqueta al eje y
plt.title('Relación entre horas de estudio y calificaciones') # Agregar título al gráfico
plt.show() # Mostrar el gráfico


```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_35_0.png)
    


### Gráficos de burbuja
Los gráficos de burbuja son una extensión de los gráficos de dispersión, donde cada punto en el gráfico representa una observación, y el tamaño de la burbuja representa una tercera variable. Para crear un gráfico de burbuja con Matplotlib, se puede utilizar la función `plt.scatter()` y especificar el tamaño de las burbujas mediante el parámetro `s`.


```python
# Ejemplo de datos reales  para el gráfico de burbuja
dfPaises = pd.DataFrame({
    "País": ["País A", "País B", "País C", "País D", "País E"],
    "Población": [1000000, 5000000, 2000000, 3000000, 4000000],
    "PIB": [50000, 200000, 100000, 150000, 250000],
    "Tasa de crecimiento": [2.5, 3.0, 1.5, 2.0, 2.8]
})
# Crear un gráfico de burbuja
plt.scatter(dfPaises["Población"], dfPaises["PIB"], s=dfPaises["Tasa de crecimiento"]*100, color='blue', alpha=0.5) # El tamaño de las burbujas se basa en la tasa de crecimiento
plt.xlabel('Población') # Agregar etiqueta al eje x
plt.ylabel('PIB') # Agregar etiqueta al eje y
plt.title('Gráfico de burbuja de países') # Agregar título al gráfico
plt.legend(['Tasa de crecimiento']) # Agregar leyenda para la tasa de
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_37_0.png)
    


Los parámetros de scatter para personalizar el gráfico de burbuja incluyen:
- `s`: Especifica el tamaño de las burbujas en el gráfico.
- `color`: Permite personalizar el color de las burbujas. Puede ser un nombre de color (por ejemplo, 'red', 'blue', 'green') o un código hexadecimal (por ejemplo, '#FF0000' para rojo).
- `alpha`: Controla la transparencia de las burbujas. Recibe un valor entre 0 y 1, donde 0 es completamente transparente y 1 es completamente opaco.
- `c`: Permite especificar un array de colores para cada burbuja, lo que es útil para representar una cuarta variable en el gráfico. Cada valor en el array se asigna a una burbuja y se puede personalizar mediante un mapa de colores (colormap) para mejorar la visualización.
- `cmap`: Especifica el mapa de colores a utilizar cuando se utiliza el parámetro `c` para asignar colores a las burbujas. Un mapa de colores es una función que asigna un color a cada valor en el array de colores, lo que permite visualizar la variación de la cuarta variable representada por el color de las burbujas. Algunos mapas de colores comunes incluyen 'viridis', 'plasma', 'inferno', 'magma' y 'cividis', entre otros. El uso de un mapa de colores adecuado puede mejorar significativamente la interpretación del gráfico de burbuja, especialmente cuando se representa una gran cantidad de datos o una amplia gama de valores para la cuarta variable.

Si, en el ejemplo anterior, deseamos que aparezca el nombre de cada país junto a su respectiva burbuja, podemos utilizar el método `plt.text()` para agregar etiquetas al gráfico. Este método permite colocar texto en una posición específica del gráfico, lo que es útil para identificar cada burbuja con su correspondiente país.

En este caso podemos iterar sobre cada fila del DataFrame `dfPaises` y utilizar `plt.text()` para agregar el nombre de cada país junto a su burbuja correspondiente en el gráfico de burbuja. Este método recibe como argumentos las coordenadas x e y donde se desea colocar el texto, el texto en sí (en este caso, el nombre del país) y opciones de formato para el texto, como el tamaño de la fuente (`fontsize`), la alineación horizontal (`ha`) y la alineación vertical (`va`). En el ejemplo, se utiliza `ha='center'` y `va='center'` para centrar el texto en la posición de la burbuja, lo que mejora la legibilidad del gráfico y facilita la identificación de cada país representado por las burbujas.

También vamos a incrementar el tamaño de cada burbuja multiplicando la tasa de crecimiento por 100, para que las diferencias entre las burbujas sean más visibles en el gráfico. Además, se ha agregado una leyenda para indicar que el tamaño de las burbujas representa la tasa de crecimiento, lo que ayuda a interpretar correctamente el gráfico de burbuja y a comprender la relación entre la población, el PIB y la tasa de crecimiento de cada país representado en el gráfico.


```python
# Ejemplo de datos reales  para el gráfico de burbuja
dfPaises = pd.DataFrame({
    "País": ["País A", "País B", "País C", "País D", "País E"],
    "Población": [1000000, 5000000, 2000000, 3000000, 4000000],
    "PIB": [50000, 200000, 100000, 150000, 250000],
    "Tasa de crecimiento": [5.5, 3.0, 1.5, 2.0, 2.8]
})

# Crear un gráfico de burbuja
plt.scatter(dfPaises["Población"], dfPaises["PIB"], s=dfPaises["Tasa de crecimiento"]*500, color='blue', alpha=0.5) # El tamaño de las burbujas se basa en la tasa de crecimiento
plt.xlabel('Población') # Agregar etiqueta al eje x
plt.ylabel('PIB') # Agregar etiqueta al eje y
plt.title('Burbuja de tasa de crecimiento') # Agregar título al gráfico
# Agregar etiquetas con el nombre de cada país
for i in range(len(dfPaises)):
    plt.text(dfPaises["Población"][i], dfPaises["PIB"][i], dfPaises["País"][i], fontsize=9, ha='center', va='center') # Agregar el nombre del país en la posición de su burbuja
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_40_0.png)
    


## Generación de gráficos con la función `plot()`de `pandas`
La función `plot()` de `pandas` es una forma conveniente de crear gráficos directamente desde un DataFrame.

Esta función actúa como un medio más directo y cómodo de utilizar Matplotlib para crear gráficos a partir de los datos almacenados en un DataFrame de `pandas`. Al utilizar `plot()`, se pueden generar gráficos de líneas, barras, sectores, histogramas, dispersión y burbuja, entre otros, sin necesidad de importar Matplotlib ni configurar el entorno para mostrar los gráficos dentro del cuaderno de Jupyter.

Esta función posee estos parámetros:
- `kind`: Especifica el tipo de gráfico que se desea crear. Puede ser 'line' para gráficos de líneas, 'bar' para gráficos de barras, 'pie' para gráficos de sectores, 'hist' para histogramas, 'scatter' para gráficos de dispersión o 'bubble' para gráficos de burbuja, entre otros.
- `figsize`: Permite especificar el tamaño del gráfico en pulgadas. Recibe una tupla con dos valores, donde el primer valor corresponde al ancho del gráfico y el segundo valor corresponde a la altura del gráfico utilizando una tupla (ancho, alto). Por ejemplo, `figsize=(10, 6)` crearía un gráfico con un ancho de 10 pulgadas y una altura de 6 pulgadas.
- `color`: Permite personalizar el color de las líneas, barras, sectores o puntos en el gráfico. Puede ser un nombre de color (por ejemplo, 'red', 'blue', 'green') o un código hexadecimal (por ejemplo, '#FF0000' para rojo).
- `title`: Agrega un título al gráfico. Recibe una cadena de texto que se mostrará como título del gráfico.
- `xlabel`: Agrega una etiqueta al eje x. Recibe una cadena de texto que se mostrará como etiqueta del eje x.
- `ylabel`: Agrega una etiqueta al eje y. Recibe una cadena de texto que se mostrará como etiqueta del eje y.
- `legend`: Muestra la leyenda del gráfico. Recibe un valor booleano (True o False) que indica si se desea mostrar la leyenda o no. Si se establece en True, se mostrará una leyenda que identifica cada serie de datos en el gráfico.
- `grid`: Agrega una cuadrícula al gráfico para facilitar la lectura de los valores. Recibe un valor booleano (True o False) que indica si se desea agregar la cuadrícula o no. Si se establece en True, se mostrará una cuadrícula en el fondo del gráfico, lo que puede ayudar a visualizar mejor los valores y las tendencias en el gráfico.
- `xticks`:Recibe una lista con la secuenca de valores para las etiquetas del eje x. Por ejemplo, `xticks=[0, 1, 2, 3, 4]` establecería las etiquetas del eje x en esos valores específicos.
- `yticks`: Recibe una lista con la secuencia de valores para las etiquetas del eje y. Por ejemplo, `yticks=[0, 10, 20, 30, 40]` establecería las etiquetas del eje y en esos valores específicos.

Ejemplo:


```python
dfAlumnos = pd.DataFrame({
    "alumno": ["Ana", "Luis", "María", "Carlos", "Sofía"],
    "edad": [20, 22, 21, 23, 19],
    "calificación": [8.5, 7.0, 9.0, 6.5, 8.0]
})
# Gráfico de dispersión
dfAlumnos.plot(kind='scatter', x='edad', y='calificación', color='blue', title='Relación entre edad y calificación', xlabel='Edad', ylabel='Calificación')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_42_0.png)
    



```python
 # Gráfico de barras
 dfAlumnos.plot(kind='bar', x='alumno', y='calificación', color='orange', title='Calificación de los alumnos', xlabel='Alumno', ylabel='Calificación')
 plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_43_0.png)
    


## Visualización con Seaborn
Seaborn es una librería basada en Matplot lib que proporciona una interfaz de alto nivel para crear gráficos estadísticos atractivos y fáciles de interpretar. Seaborn se integra bien con los DataFrames de `pandas` y ofrece funciones específicas para visualizar relaciones entre variables, distribuciones de datos y patrones en conjuntos de datos complejos.

### Instalación de Seaborn
Para instalar Seaborn, puedes usar pip, el gestor de paquetes de Python o bien conda, el gestor de paquetes de Anaconda.
Mediante `pip` se haría de esta forma:
```bash
pip install seaborn
```

Mediante `conda` se haría de esta forma (suponiendo que hemos activado nuestro entorno de trabajo:
```bash
conda install seaborn
```

Después deberemos importar la biblioteca para poder utilizarla en nuestro cuaderno de Jupyter:


```python
import seaborn as sns
```

### Trazados lm
Los trazados lm (linear model) son gráficos de dispersión que incluyen una línea de regresión ajustada a los datos. Estos gráficos son útiles para visualizar la relación entre dos variables numéricas y para identificar patrones lineales en los datos. Para crear un trazado lm con Seaborn, se puede utilizar la función `sns.lmplot()`. Esta función recibe como argumentos el nombre de las columnas del DataFrame que se desean graficar en el eje x e y, así como el DataFrame que contiene los datos.


```python
df = pd.DataFrame({
    "Horas de estudio": [1, 2, 3, 4, 5, 6, 5, 4, 4, 2],
    "Calificaciones": [7, 8, 6, 9, 10, 9, 8, 8, 6, 7],
    "Grupo": ['A', 'A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'B']
})
sns.lmplot(x='Horas de estudio', y='Calificaciones', data=df) # Crear un trazado lm
plt.title('Relación entre horas de estudio y calificaciones') # Agregar título al gráfico
plt.xlabel('Horas de estudio') # Agregar etiqueta al eje x
plt.ylabel('Calificaciones') # Agregar etiqueta al eje y
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_47_0.png)
    


Podemos eliminar la línea de regresión del trazado lm utilizando el parámetro `fit_reg=False`, lo que nos permitirá visualizar únicamente los puntos de datos sin la línea de regresión ajustada. Esto puede ser útil cuando queremos centrarnos en la distribución de los datos sin destacar una relación lineal específica entre las variables.


```python
df = pd.DataFrame({
    "Horas de estudio": [1, 2, 3, 4, 5, 6, 5, 4, 4, 2],
    "Calificaciones": [7, 8, 6, 9, 10, 9, 8, 8, 6, 7],
    "Grupo": ['A', 'A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'B']
})
sns.lmplot(x='Horas de estudio', y='Calificaciones', data=df, fit_reg=False)
plt.title('Relación entre horas de estudio y calificaciones')
plt.xlabel('Horas de estudio')
plt.ylabel('Calificaciones')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_49_0.png)
    


El método `lmplot()` también permite crear trazados lm para diferentes grupos de datos utilizando el parámetro `hue`. Este parámetro recibe el nombre de la columna del DataFrame que contiene las categorías o grupos que se desean diferenciar en el gráfico. Al utilizar `hue`, Seaborn asignará automáticamente un color diferente a cada grupo, lo que facilitará la visualización de las diferencias entre los grupos en el trazado lm. Esto es especialmente útil cuando se desea comparar la relación entre las variables para diferentes categorías o grupos dentro del mismo gráfico.


```python
df = pd.DataFrame({
    "Horas de estudio": [1, 2, 3, 4, 5, 6, 5, 4, 4, 2],
    "Calificaciones": [7, 8, 6, 9, 10, 9, 8, 8, 6, 7],
    "Grupo": ['A', 'A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'B']
})
sns.lmplot(x='Horas de estudio', y='Calificaciones', data=df, hue='Grupo')
plt.title('Relación entre horas de estudio y calificaciones por grupo')
plt.xlabel('Horas de estudio')
plt.ylabel('Calificaciones')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_51_0.png)
    


Podemos personalizar la visualización del gráfico mediante estos parámetros:
* palette: Que permite especificar una paleta personalizada indicado un array con los colores de cada grupo, o bien utilizando una paleta predefinida de Seaborn, como 'Set1', 'Set2', 'Set3', 'Pastel1', 'Pastel2', 'Dark2', entre otras.
* markers: Permite personalizar los marcadores utilizados para cada grupo en el gráfico. Recibe una lista de símbolos de marcador que corresponden a cada grupo, como 'o' para círculos, 's' para cuadrados, '^' para triángulos, entre otros. Esto ayuda a diferenciar visualmente los grupos en el gráfico de dispersión, especialmente cuando se utilizan colores similares para los grupos.
* scatter_kws: Permite personalizar los puntos de datos en el gráfico de dispersión. Recibe un diccionario de argumentos que se pasan a la función `plt.scatter()`, lo que permite ajustar aspectos como el tamaño de los puntos (`s`), la transparencia (`alpha`), el color (`color`), el tipo de marcador (`marker`), entre otros. Esto proporciona un mayor control sobre la apariencia de los puntos de datos en el gráfico, lo que puede mejorar la legibilidad y la interpretación del gráfico de dispersión.


```python
df = pd.DataFrame({
    "Horas de estudio": [1, 2, 3, 4, 5, 6, 5, 4, 4, 2],
    "Calificaciones": [7, 8, 6, 9, 10, 9, 8, 8, 6, 7],
    "Grupo": ['A', 'A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'B']
})
sns.lmplot(x='Horas de estudio', y='Calificaciones', data=df, hue='Grupo',  scatter_kws={'s': 100, 'alpha': 0.7}, markers=['o', 's'], palette=['green', 'violet'])
plt.title('Relación entre horas de estudio y calificaciones por grupo')
plt.xlabel('Horas de estudio')
plt.ylabel('Calificaciones')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_53_0.png)
    


### Gráficos de barra
Seaborn también proporciona funciones para crear gráficos de barras que permiten comparar diferentes categorías o grupos de datos. Para crear un gráfico de barras con Seaborn, se puede utilizar la función `sns.barplot()`. Esta función recibe como argumentos el nombre de las columnas del DataFrame que se desean graficar en el eje x e y, así como el DataFrame que contiene los datos. Además, el parámetro `hue` se puede utilizar para diferenciar grupos dentro de cada categoría, lo que permite comparar subcategorías dentro de cada categoría principal en el gráfico de barras.


```python
df = pd.DataFrame({
    "Asignatura": ['Lengua', 'Lengua', 'Matemáticas', 'Matemáticas', 'Ciencias', 'Ciencias'],
    "Calificación": [8, 7, 9, 6, 8, 6],
    "Grupo": ['A', 'B', 'A', 'B',  'A', 'B']
})
sns.barplot(x='Asignatura', y='Calificación', data=df, hue='Grupo', palette='Set2')
plt.title('Gráfico de barras con Seaborn')
plt.xlabel('Asignatura')
plt.ylabel('Calificación')
plt.legend(title='Grupo')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_55_0.png)
    


### Gráficos de distribución
El método `distplot()` de Seaborn se utiliza para visualizar la distribución de una variable numérica. Este método combina un histograma con una curva de densidad para mostrar la forma de la distribución de los datos. El histograma muestra la frecuencia de los datos en diferentes intervalos, mientras que la curva de densidad proporciona una estimación suave de la distribución subyacente. Esto es útil para identificar patrones, tendencias y posibles valores atípicos en los datos, así como para comparar la distribución de diferentes conjuntos de datos.

Para crear un gráfico de distribución con Seaborn, se puede utilizar la función `sns.distplot()`. Esta función recibe como argumento el nombre de la columna del DataFrame que contiene los datos numéricos que se desean visualizar, así como el DataFrame que contiene los datos. Además, el parámetro `hue` se puede utilizar para diferenciar grupos dentro de la distribución, lo que permite comparar la forma de la distribución para diferentes categorías o grupos dentro del mismo gráfico.

El parámetro `kde` se utiliza para mostrar la curva de densidad en el gráfico de distribución. Si se establece en True, se mostrará la curva de densidad junto con el histograma, lo que proporciona una representación más suave de la distribución de los datos. Esto puede ayudar a identificar patrones y tendencias en la distribución que pueden no ser evidentes solo con el histograma.


```python
df = pd.DataFrame({
    "Calificaciones": [7, 8, 6, 9, 10, 9, 8, 8, 6, 7],
    "Grupo": ['A', 'A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'B']
})
sns.displot(df['Calificaciones'],  kde=True) # Crear un gráfico de distribución
plt.title('Distribución de calificaciones')
plt.xlabel('Calificaciones')
plt.ylabel('Densidad')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_57_0.png)
    


### Gráficos de caja
Los gráficos de caja, también conocidos como boxplots, son útiles para mostrar la distribución de una variable numérica y para identificar valores atípicos.

En estos gráficos, la caja representa el rango intercuartílico (IQR) de los datos, que abarca desde el primer cuartil (Q1) hasta el tercer cuartil (Q3). La línea dentro de la caja indica la mediana de los datos. Los "bigotes" del gráfico se extienden desde los cuartiles hasta el valor máximo y mínimo dentro de un rango específico, generalmente 1.5 veces el IQR. Cualquier punto que caiga fuera de este rango se considera un valor atípico y se representa como un punto individual en el gráfico.

Para crear un gráfico de caja con Seaborn, se puede utilizar la función `sns.boxplot()`. Esta función recibe como argumentos el nombre de las columnas del DataFrame que se desean graficar en el eje x e y, así como el DataFrame que contiene los datos.

Nuevamente podemos utilizar el parámetro `hue` para diferenciar grupos dentro de cada categoría, lo que permite comparar la distribución de los datos para diferentes grupos dentro del mismo gráfico de caja. Esto es especialmente útil para identificar diferencias en la mediana, el rango intercuartílico y la presencia de valores atípicos entre los grupos representados en el gráfico de caja.



```python
df = {
    "empleado": ["Ana","Luis","Marta","Carlos","Sofía","Pedro","Lucía","Jorge","Elena","Raúl"],
    "sexo": ["M","H","M","H","M","H","M","H","M","H"],
    "edad": [23,45,31,50,29,41,37,60,26,48],
    "salario": [1800,3200,2400,4000,2100,3500,2900,5200,2000,3700]
}

sns.boxplot(x = df["sexo"], y = df["salario"], hue = df["sexo"], palette = "Set1") # Crear un gráfico de caja
plt.title('Gráfico de caja de salarios por sexo') # Agregar título al gráfico
plt.xlabel('Sexo') # Agregar etiqueta al eje x
plt.ylabel('Salario') # Agregar etiqueta al eje y
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_59_0.png)
    


### Gráficos de violín
Los gráficos de violín son una combinación de un gráfico de caja y un gráfico de densidad. Estos gráficos muestran la distribución de una variable numérica, al igual que los gráficos de caja, pero también incluyen una curva de densidad que representa la forma de la distribución de los datos.

Esto permite visualizar no solo la mediana, el rango intercuartílico y los valores atípicos, sino también la forma general de la distribución, lo que puede proporcionar información adicional sobre la presencia de múltiples modos o la asimetría en los datos.

Para crear un gráfico de violín con Seaborn, se puede utilizar la función `sns.violinplot()`. Esta función recibe como argumentos el nombre de las columnas del DataFrame que se desean graficar en el eje x e y, así como el DataFrame que contiene los datos. Al igual que con los gráficos de caja, el parámetro `hue` se puede utilizar para diferenciar grupos dentro de cada categoría, lo que permite comparar la distribución de los datos para diferentes grupos dentro del mismo gráfico de violín.


```python
df = pd.DataFrame({
    "empleado": ["Ana","Luis","Marta","Carlos","Sofía","Pedro","Lucía","Jorge","Elena","Raúl"],
    "sexo": ["M","H","M","H","M","H","M","H","M","H"],
    "edad": [23,45,31,50,29,41,37,60,26,48],
    "salario": [1800,3200,2400,4000,2100,3500,2900,5200,2000,3700]})
sns.violinplot(x = df["sexo"], y = df["salario"], hue = df["sexo"], palette = "Set2") # Crear un gráfico de violín
plt.title('Gráfico de violín de salarios por sexo') # Agregar título al gráfico
plt.xlabel('Sexo') # Agregar etiqueta al eje x
plt.ylabel('Salario') # Agregar etiqueta al eje y
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_61_0.png)
    


En el gráfico de violín, la parte más ancha del gráfico representa la mayor densidad de datos, mientras que la parte más estrecha representa una menor densidad de datos.

La línea dentro del gráfico de violín indica la mediana de los datos, y los "bigotes" se extienden hasta el valor máximo y mínimo dentro de un rango específico, similar a los gráficos de caja.

### Diagrama de barras de frecuencia
Los diagramas de barras de frecuencia son gráficos que muestran la frecuencia o el conteo de cada categoría en un conjunto de datos. Estos gráficos son útiles para visualizar la distribución de una variable categórica y para comparar la frecuencia de diferentes categorías.

Para crear un diagrama de barras de frecuencia con Seaborn, se puede utilizar la función `sns.countplot()`. Esta función recibe como argumento el nombre de la columna del DataFrame que contiene las categorías que se desean graficar, así como el DataFrame que contiene los datos.

El parámetro `hue` se puede utilizar para diferenciar grupos dentro de cada categoría, lo que permite comparar la frecuencia de las categorías para diferentes grupos dentro del mismo gráfico de barras de frecuencia.


```python
df = pd.DataFrame({
    "empleado": ["Ana","Luis","Marta","Carlos","Sofía","Pedro","Lucía","Jorge","Elena","Marta"],
    "sexo": ["M","H","M","H","M","H","M","H","M","M"],
    "edad": [23,45,31,50,29,41,37,60,26,48],
    "salario": [1800,3200,2400,4000,2100,3500,2900,5200,2000,3700]})

sns.countplot(x=df["sexo"], hue=df["sexo"], palette="Set1") # Crear un diagrama de barras de frecuencia
plt.title('Diagrama de barras de frecuencia por sexo') # Agregar título al gráfico
plt.xlabel('Sexo') # Agregar etiqueta al eje x
plt.ylabel('Frecuencia') # Agregar etiqueta al eje y
plt.show() # Mostrar el gráfico

```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_64_0.png)
    


### Gráficos de conjunto
Los gráficos de conjunto, también conocidos como gráficos de intersección o **gráficos de Venn**, son útiles para visualizar las relaciones entre diferentes conjuntos de datos. Estos gráficos muestran cómo se superponen los conjuntos y cuántos elementos pertenecen a cada conjunto y a las intersecciones entre ellos.

Para crear un gráfico de conjunto con Seaborn, se puede utilizar la función `sns.vennplot()`. Esta función recibe como argumentos el nombre de las columnas del DataFrame que contienen los conjuntos que se desean graficar, así como el DataFrame que contiene los datos.

Se dispone del parámetro `hue` que se puede utilizar para diferenciar grupos dentro de cada conjunto, lo que permite comparar la distribución de los datos para diferentes grupos dentro del mismo gráfico de conjunto.



```python
df = pd.DataFrame({
    "propina": [3, 5, 2, 4, 6, 1, 3, 5, 2, 4, 5, 2, 8, 6, 4, 7, 3, 5, 2, 4],
    "cuenta": [20, 30, 15, 25, 35, 10, 20, 30, 15, 25, 30, 15, 40, 35, 25, 45, 20, 30, 15, 25]
})
sns.jointplot(x="propina", y="cuenta", data=df) # Crear un gráfico de conjunto
plt.xlabel('Propina') # Agregar etiqueta al eje x
plt.ylabel('Cuenta') # Agregar etiqueta al eje y
plt.show() # Mostrar el gráfico


```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_66_0.png)
    


El parámetro `kind` en la función `sns.jointplot()` permite especificar el tipo de gráfico que se desea crear para visualizar la relación entre las dos variables. Los valores posibles para `kind` incluyen:
- `scatter`: Crea un gráfico de dispersión que muestra la relación entre las dos variables mediante puntos en el gráfico.
- `reg`: Crea un gráfico de regresión que incluye una línea de regresión ajustada a los datos, lo que permite visualizar la tendencia general de la relación entre las variables.
- `resid`: Crea un gráfico de residuos que muestra la diferencia entre los valores observados y los valores predichos por la línea de regresión, lo que ayuda a identificar patrones en los residuos que pueden indicar problemas con el modelo de regresión.
- `kde`: Crea un gráfico de densidad conjunta que muestra la distribución de las dos variables mediante una curva de densidad, lo que permite visualizar la concentración de los datos en diferentes áreas del gráfico.


```python
sns.jointplot(x = "propina", y = "cuenta", data = df, kind = "kde")
plt.xlabel('Propina')
plt.ylabel('Cuenta')
plt.show()
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_68_0.png)
    


### Mapas de calor
Los mapas de calor son gráficos que utilizan colores para representar la intensidad o la frecuencia de los datos en una matriz o tabla. Estos gráficos son útiles para visualizar patrones, tendencias y relaciones entre variables en conjuntos de datos complejos.

Para crear un mapa de calor con Seaborn, se puede utilizar la función `sns.heatmap()`. Esta función recibe como argumento una matriz o tabla de datos que se desea visualizar, así como el DataFrame que contiene los datos. Además, el parámetro `annot` se puede utilizar para mostrar los valores numéricos dentro de cada celda del mapa de calor, lo que facilita la interpretación de los datos representados en el gráfico.

El parámetro `cmap` permite personalizar la paleta de colores utilizada en el mapa de calor. Se pueden utilizar paletas predefinidas de Seaborn, como 'YlGnBu', 'viridis', 'plasma', 'inferno', entre otras, o bien especificar una paleta personalizada utilizando un array de colores. La elección de una paleta de colores adecuada puede mejorar significativamente la legibilidad y la interpretación del mapa de calor, especialmente cuando se representan datos con una amplia gama de valores o cuando se desea destacar ciertas áreas del gráfico.


```python
df = pd.DataFrame({
    "empleado": ["Ana","Luis","Marta","Carlos","Sofía","Pedro","Lucía","Jorge","Elena","Marta"],
    "sexo": ["M","H","M","H","M","H","M","H","M","M"],
    "edad": [23,45,31,50,29,41,37,60,26,48],
    "salario": [2400,3200,2400,2100,2100,3500,2900,2900,2900,3700]})

# Crear una tabla de contingencia para el mapa de calor
tabla_contingencia = pd.crosstab(df["sexo"], df["salario"])

sns.heatmap(tabla_contingencia, annot=True, cmap="inferno") # Crear un mapa de calor
plt.title('Mapa de calor de salarios por sexo') # Agregar título al gráfico
plt.xlabel('Salario') # Agregar etiqueta al eje x
plt.ylabel('Sexo') # Agregar etiqueta al eje y
plt.show() # Mostrar el gráfico
```


    
![png](../../jupyter/U05/Visualizacion_files/Visualizacion_70_0.png)
    

