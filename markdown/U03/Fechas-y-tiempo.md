# Manejo de fechas e intervalos en Python
## Índice
[Fechas en Python](#Fechas-en-Python)
- [Módulo `datetime`](#Módulo-datetime)
- [Clase `date`](#Clase-date)
- [Clase `datetime`](#Clase-datetime)
- [Formato de fechas](#Formato-de-fechas)
- [Intervalos de tiempo con `timedelta`](#Intervalos-de-tiempo-con-timedelta)
- [Operaciones con fechas e intervalos](#Operaciones-con-fechas-e-intervalos)
## Manejo de fechas e intervalos con Pandas
- [Fechas en Pandas](#Fechas-en-Pandas)
- [Extraer información de fechas](#Extraer-información-de-fechas)
- [Filtrar datos por fechas](#Filtrar-datos-por-fechas)
- [Cálculos estadísticons con fechas](#Cálculos-estadísticons-con-fechas)
- [Remuestreo de fechas](#Remuestreo-de-fechas)
- [Intervalos temporales en Pandas](#Intervalos-temporales-en-Pandas)
- [Crear secuencias temporales](#Crear-secuencias-temporales)

## Fechas en Python
### Módulo `datetime`
En Python podemos usar el módulo `datetime` para trabajar con fechas y horas. Este módulo proporciona clases para manipular fechas y horas de manera sencilla.
Este módulo aporta varias clases, entre ellas:
- `datetime`: para representar fechas y horas.
- `date`: para representar solo fechas.
- `time`: para representar solo horas.
- `timedelta`: para representar diferencias entre fechas y horas (intervalos de tiempo).
- `tzinfo`: para manejar zonas horarias.
- `timezone`: para representar zonas horarias específicas.

Normalmente al importar el módulo `datetime`, se suelen importar solo la clases que necesitamos, por ejemplo:


```python
from datetime import date, datetime, timedelta
```


### Clase date
La clase `date` se utiliza para representar fechas sin información de tiempo, solo usando día, mes y año.

Podemos crear objetos de tipo date que recojan la fecha actual usando el método `today()`


```python
hoy = date.today()
print(hoy)
```

    2026-02-25
    

También podemos crear objetos de tipo date a partir de una fecha específica usando el constructor de la clase `date`:


```python
dia1 = date(2024, 6, 15)  # Año, mes, día
print(dia1)
```

    2024-06-15
    

## Clase `datetime`
Esta clase se utiliza para representar fechas y horas. Permite almacenar información de día, mes, año, hora, minuto, segundo y microsegundo.
Podemos crear objetos de tipo `datetime` que recojan la fecha y hora actual usando el método `now()`


```python
ahora = datetime.now()
print(ahora)
```

    2026-02-25 15:33:00.225632
    

También podemos crear objetos de tipo `datetime` a partir de una fecha y hora específica usando el constructor de la clase `datetime`, el cual recibe como argumentos el año, mes, día, hora, minuto, segundo y microsegundo (estos últimos son opcionales):


```python
fecha1 = datetime(2024, 6, 15, 14, 30, 0)  # Año, mes, día, hora, minuto, segundo
print(fecha1)
```

    2024-06-15 14:30:00
    

## Formato de fechas
A la hora de mostrar las fechas en pantalla, podemos usar el método `strftime()` para formatear la fecha de acuerdo a nuestras necesidades. Este método es parte de las clases `date` y `datetime` y permite convertir un objeto de fecha en una cadena de texto con el formato que especifiquemos.

Para ello el método `strftime()` recibe como argumento una cadena de formato que puede contener diferentes códigos para representar partes de la fecha. Los principales códigos de formato son:
- `%Y`: Año con cuatro dígitos (ejemplo: 2024)
- `%m`: Mes con dos dígitos (ejemplo: 06)
- `%d`: Día del mes con dos dígitos (ejemplo: 15)
- `%H`: Hora en formato de 24 horas con dos dígitos (ejemplo: 14)
- `%I`: Hora en formato de 12 horas con dos dígitos (ejemplo: 02)
- `%p`: AM o PM (ejemplo: PM)
- `%M`: Minuto con dos dígitos (ejemplo: 30)
- `%S`: Segundo con dos dígitos (ejemplo: 00)
- `%f`: Microsegundo con seis dígitos (ejemplo: 000000)
- `%A`: Nombre completo del día de la semana (ejemplo: Saturday)
- `%a`: Nombre abreviado del día de la semana (ejemplo: Sat)
- `%u`: Día de la semana como número (1-7, donde 1 es lunes)
- `%w`: Día de la semana como número (0-6, donde 0 es domingo)
- `%B`: Nombre completo del mes (ejemplo: June)
- `%b`: Nombre abreviado del mes (ejemplo: Jun)
- `%j`: Día del año con tres dígitos (ejemplo: 167)
- `%W`: Número de semana del año (lunes como primer día de la semana, 00-53)
- `%U`: Número de semana del año (domingo como primer día de la semana, 00-53)
- `%%`: Carácter de porcentaje literal (%)

Ejemplos:


```python
hoy = date.today()
print(hoy.strftime("%Y-%m-%d"))  # Formato ISO: Año-Mes-Día
print(hoy.strftime("%d/%m/%Y"))  # Formato común en español: Día/Mes/Año
# formato largo
print(hoy.strftime("%A, %d de %B de %Y"))  # Ejemplo: Saturday, 15 de June de 2024

ahora = datetime.now()
print(ahora.strftime("%Y-%m-%d %H:%M:%S")) # Formato ISO: Año-Mes-Día Hora:Minuto:Segundo
print(ahora.strftime("%d/%m/%Y %H:%M:%S")) # Formato común en español: Día/Mes/Año Hora:Minuto:Segundo
```

    2026-02-25
    25/02/2026
    Wednesday, 25 de February de 2026
    2026-02-25 15:33:00
    25/02/2026 15:33:00
    

#### Formato de fechas en español
Para mostrar los nombres de los días de la semana y los meses en español, podemos usar el módulo `locale` para determinar la configuración regional de nuestra aplicación. Esto nos permitirá formatear las fechas de acuerdo a las convenciones de nuestro idioma y región.

En el caso de España podemos establecer la configuración regional a `es_ES` (español de España). Para ello habría que ejecutar el siguiente código:


```python
import locale
locale.setlocale(locale.LC_TIME, 'es_ES')
# formato largo
hoy = date.today()
print(hoy.strftime("%A, %d de %B de %Y"))
```

    miércoles, 25 de febrero de 2026
    

Esa instrucción establece la configuración regional para el formato de fechas y horas a español de España. A partir de ese momento, al usar el método `strftime()` para formatear fechas, los nombres de los días de la semana y los meses se mostrarán en español.

## Intervalos de tiempo con `timedelta`
La clase `timedelta` sirve para representar intervalos de tiempo. Se utiliza habitualmente para realizar operaciones aritméticas con fechas, como sumar o restar días, horas, minutos, etc.
Podemos crear objetos de tipo `timedelta` usando su constructor, el cual recibe como argumentos los diferentes componentes del intervalo de tiempo:
- `weeks`: número de semanas (equivalente a 7 días)
- `days`: número de días
- `hours`: número de horas (equivalente a 60 minutos)- `seconds`: número de segundos
- `minutes`: número de minutos (equivalente a 60 segundos)
- `microseconds`: número de microsegundos
- `milliseconds`: número de milisegundos (equivalente a 1000 microsegundos)

Ejemplo:


```python
intervalo1 = timedelta(days=7)  # Intervalo de 7 días
intervalo2 = timedelta(hours=3, minutes=30)  # Intervalo de 3 horas y 30 minutos
intervalo3 = timedelta(weeks=2, days=3, hours=5)  # Intervalo de 2 semanas, 3 días y 5 horas
print(intervalo1)
print(intervalo2)
print(intervalo3)
```

    7 days, 0:00:00
    3:30:00
    17 days, 5:00:00
    

### Propiedades de `timedelta`
Los objetos de tipo `timedelta` tienen varias propiedades que nos permiten acceder a los diferentes componentes del intervalo de tiempo:
- `days`: número total de días en el intervalo
- `seconds`: número total de segundos en el intervalo (excluyendo los días)
- `microseconds`: número total de microsegundos en el intervalo (excluyendo los días y segundos)
- `total_seconds()`: Convierte el intervalo a segundos y devuelve el resultado como un número de punto flotante.

Podemos observar que no aparecen propiedades para obte


```python
intervalo = timedelta(days=1, hours=1)
print(f"Días: {intervalo.days}")
print(f"Segundos: {intervalo.seconds}") # Sale 3600, los segundos de la parte de la hora, pero no incluye el día
print(f"Microsegundos: {intervalo.microseconds}") # Sale 0, ya que no hemos incluido microsegundos en el intervalo
print(f"Total de segundos: {intervalo.total_seconds()}") # Sale 90000, que es el total de segundos del intervalo (1 día = 86400 segundos + 1 hora = 3600 segundos)
```

    Días: 1
    Segundos: 3600
    Microsegundos: 0
    Total de segundos: 90000.0
    

### Formato de intervalos de tiempo
Para mostrar los intervalos de tiempo en un formato legible, podemos convertir el objeto `timedelta` a una cadena de texto usando el método `str()`. Este método convierte el intervalo a forma de texto predefinida.

Normalmente el formato se da mediante el acceso a los atributos para mostrar solo las partes que nos interesen (días, horas, minutos, etc.).
Ejemplo:


```python
intervalo = timedelta(days=7, hours=3, minutes=30)
print(str(intervalo))  # Muestra el intervalo completo en formato legible
# Mostrar el intervalo en español
dias = intervalo.days
horas = intervalo.seconds // 3600
minutos = (intervalo.seconds % 3600) // 60
print(f"Intervalo: {dias} días, {horas} horas y {minutos} minutos")

# Mostrar solo los días, horas y minutos por separado
print(f"Días: {intervalo.days}, Horas: {intervalo.seconds // 3600}, Minutos: {(intervalo.seconds % 3600) // 60}")
```

    7 days, 3:30:00
    Intervalo: 7 días, 3 horas y 30 minutos
    Días: 7, Horas: 3, Minutos: 30
    

## Operaciones con fechas e intervalos
### Diferencia entre fechas
Podemos calcular la diferencia entre dos fechas o entre dos objetos `datetime` restándolos. El resultado de esta operación es un objeto de tipo `timedelta` que representa el intervalo de tiempo entre las dos fechas.
Ejemplo:


```python
fecha1 = date(2024, 6, 15)
fecha2 = date(2024, 7, 1)
diferencia = fecha2 - fecha1
print(diferencia)  # Muestra el intervalo de tiempo entre las dos fechas
print(f"Días de diferencia: {diferencia.days}")  # Muestra solo el número de días de diferencia
```

    16 days, 0:00:00
    Días de diferencia: 16
    

En el caso de otros cálculos como la diferencia en meses o años, no existe una forma directa de calcularlo usando `timedelta`, ya que los meses y años pueden tener diferentes números de días. Para calcular la diferencia en meses o años, tendríamos que implementar una lógica adicional que tenga en cuenta las variaciones en la duración de los meses y los años bisiestos.
Un ejemplo de cálculo, pero que resultaría inexacto debido a las variaciones en la duración de los meses, sería el siguiente:


```python

fecha1 = date(2024, 6, 15)
fecha2 = date(2026, 2, 13)
# Meses de diferencia
meses_diferencia = (fecha2.year - fecha1.year) * 12 + (fecha2.month - fecha1.month)
print(f"Meses de diferencia: {meses_diferencia}")
```

    Meses de diferencia: 20
    

Para cálculos más exactos en meses o años, podríamos usar una biblioteca externa como `dateutil`, que proporciona funciones para calcular diferencias entre fechas teniendo en cuenta las variaciones en la duración de los meses y los años bisiestos.

### Suma y resta de intervalos a fechas
Podemos sumar o restar un objeto `timedelta` a una fecha o a un objeto `datetime` para obtener una nueva fecha o fecha y hora resultante de la operación.
Ejemplo:


```python
fecha1 = date(2024, 6, 15)
intervalo = timedelta(days=10)
nueva_fecha = fecha1 + intervalo  # Suma el intervalo a la fecha
print(nueva_fecha)  # Muestra la nueva fecha resultante de la suma

fecha2 = datetime(2024, 6, 15, 14, 30)
intervalo2 = timedelta(hours=2, minutes=15)
nueva_fecha2 = fecha2 + intervalo2  # Suma el intervalo a la fecha
print(nueva_fecha2)  # Muestra la nueva fecha y hora resultante de la
```

    2024-06-25
    2024-06-15 16:45:00
    

### Comparaciones entre fechas
Las fechas y los objetos `datetime` se pueden comparar entre sí usando los operadores de comparación estándar (`<`, `<=`, `>`, `>=`, `==`, `!=`). Estas comparaciones se basan en la fecha y hora representada por los objetos, por lo que podemos determinar si una fecha es anterior, posterior o igual a otra.
Ejemplo:   


```python
fecha1 = date(2025, 6, 15)
fecha2 = date(2025, 6, 19)
print(fecha1 < fecha2)  # True, porque fecha1 es anterior a fecha2
print(fecha1 > fecha2)  # False, porque fecha1 no es posterior a fecha2
print(fecha1 == fecha2) # False, porque fecha1 no es igual a fecha2
```

    True
    False
    False
    

## Manejo de fechas e intervalos con Pandas
Pandas es una biblioteca de Python que proporciona estructuras de datos y herramientas para el análisis de datos. Pandas tiene varias funciones y métodos para trabajar con fechas e intervalos de tiempo, lo que facilita el manejo de datos temporales en nuestros análisis. 


```python
import pandas as pd
```

### Fechas en Pandas
Pandas tiene un tipo de dato específico para manejar fechas y horas, llamado `Timestamp`. Este tipo de dato es similar a la clase `datetime` del módulo `datetime`, pero con funcionalidades adicionales que facilitan el trabajo con series temporales. Además, Pandas tiene una función llamada `to_datetime()` que permite convertir diferentes formatos de fechas a objetos `Timestamp`, lo que facilita la manipulación de datos temporales en nuestros análisis.
#### Conversión de columnas a fechas
Si tenemos un DataFrame con una columna que contiene fechas en formato de texto, podemos convertir esa columna a objetos `Timestamp` usando la función `to_datetime()`. Esto nos permitirá realizar operaciones de fecha y hora de manera más sencilla en esa columna.
Ejemplo:


```python
datos = pd.DataFrame({
    "fecha": ["2025-06-15", "2025-07-01", "2025-08-20"],
    "valor": [9800, 7820, 8930] 
})
#La columna "fecha" está en formato de texto
print(datos["fecha"].dtype)  # Muestra el tipo de dato de la columna "fecha", aparece object, que es el tipo de dato para texto en Pandas
# Convertimos la columna "fecha" a tipo datetime
datos["fecha"] = pd.to_datetime(datos["fecha"])
print(datos["fecha"].dtype)  # Ahora muestra datetime64[ns], que es el tipo de dato para fechas en Pandas
```

    object
    datetime64[ns]
    

En el ejemplo anterior, la conversión es sencilla porque las fechas están en un formato estándar (YYYY-MM-DD). Sin embargo, `to_datetime()` es capaz de manejar una amplia variedad de formatos de fecha, por lo que incluso si las fechas estuvieran en un formato diferente, Pandas podría convertirlas correctamente a objetos `Timestamp`.
Para ello podemos usar el parámetro `format` de la función `to_datetime()` para especificar el formato de las fechas en la columna. 
EL parámetro `format` admite estos códigos de formato para fechas:
- `%Y`: Año con cuatro dígitos (ejemplo: 2024)
- `%m`: Mes con dos dígitos (ejemplo: 06)
- `%d`: Día del mes con dos dígitos (ejemplo: 15)
- `%H`: Hora en formato de 24 horas con dos dígitos (ejemplo: 14)
- `%I`: Hora en formato de 12 horas con dos dígitos (ejemplo: 02)
- `%p`: AM o PM (ejemplo: PM)
- `%M`: Minuto con dos dígitos (ejemplo: 30)
- `%S`: Segundo con dos dígitos (ejemplo: 00)
- `%f`: Microsegundo con seis dígitos (ejemplo: 000000)
- `%A`: Nombre completo del día de la semana (ejemplo: Saturday)
- `%a`: Nombre abreviado del día de la semana (ejemplo: Sat)
- `%u`: Día de la semana como número (1-7, donde 1 es lunes)
- `%w`: Día de la semana como número (0-6, donde 0 es domingo)
- `%B`: Nombre completo del mes (ejemplo: June)
- `%b`: Nombre abreviado del mes (ejemplo: Jun)
- `%W`: Número de semana del año (lunes como primer día de la semana, 00-53)
- `%U`: Número de semana del año (domingo como primer día de la semana, 00-53)

Podemos observar que son los mismos códigos de formato que se usan para el método `strftime()`, pero en este caso se utilizan para indicar el formato de las fechas que queremos convertir a objetos `Timestamp`.
Ejemplo:


```python
datos = pd.DataFrame({
    "fecha": ["12/06/2025", "01/07/2025", "20/08/2025"],
    "valor": [9800, 7820, 8930]
})
# Convertimos la columna "fecha" a tipo datetime especificando el formato
datos["fecha"] = pd.to_datetime(datos["fecha"], format="%d/%m/%Y")
print(datos["fecha"].dtype)  # Comprobamos que el tipo ha cambiado
```

    datetime64[ns]
    

### Extraer información de fechas
Una vez que tenemos una columna de fechas convertida a objetos `Timestamp`, podemos extraer fácilmente información específica de esas fechas usando los atributos de los objetos `Timestamp`. Por ejemplo, podemos extraer el año, el mes, el día, la hora, el minuto, el segundo, etc.

Para ello se utiliza la propiedad `dt` de la columna de fechas, que nos permite acceder a los diferentes componentes de las fechas. Esta propiedad retorna un objeto de tipo `Series` con los diferentes atributos de las fechas, como `year`, `month`, `day`, `hour`, `minute`, `second`, etc.
Ejemplo:


```python
datos = pd.DataFrame({
    "fecha": ["12/06/2025", "01/07/2025", "20/08/2025"],
    "valor": [9800, 7820, 8930]
})
datos["fecha"] = pd.to_datetime(datos["fecha"], format = "%d/%m/%Y") 
print("Años:\n", datos["fecha"].dt.year)  # Extrae el año de cada fecha
print("Meses:\n",datos["fecha"].dt.month) # Extrae el mes de cada fecha
print("Días:\n",datos["fecha"].dt.day)   # Extrae el día de cada fecha
print("Horas:\n",datos["fecha"].dt.hour)  # Extrae la hora de cada fecha (en este caso será 0, ya que no hemos incluido información de hora en las fechas)

```

    Años:
     0    2025
    1    2025
    2    2025
    Name: fecha, dtype: int32
    Meses:
     0    6
    1    7
    2    8
    Name: fecha, dtype: int32
    Días:
     0    12
    1     1
    2    20
    Name: fecha, dtype: int32
    Horas:
     0    0
    1    0
    2    0
    Name: fecha, dtype: int32
    

### Filtrar datos por fechas
Pandas también nos permite filtrar datos en un DataFrame basándonos en condiciones relacionadas con las fechas. Podemos usar operadores de comparación para filtrar filas que cumplan ciertas condiciones en una columna de fechas. Por ejemplo, podemos filtrar filas que correspondan a un año específico, a un rango de fechas, o a un mes determinado.
Ejemplo:


```python
# DataFrame en el que realizamos conversión de fechas durante su creación
datos = pd.DataFrame({
    "fecha":["2025-06-15", "2025-07-01", "2025-08-20","2025-09-10","2025-07-12"],
    "ventas":[9800, 7820, 8930, 12000, 11000]
})  # Especificamos el tipo de dato de la columna "fecha" durante la creación del DataFrame
datos["fecha"] = pd.to_datetime(datos["fecha"])  
# Mostrar fechas de 12 de juli de 2025 o posteriores
filtro_fecha = datos["fecha"] >= "2025-07-12"
datos_filtrados = datos[filtro_fecha]
print(datos_filtrados)
```

           fecha  ventas
    2 2025-08-20    8930
    3 2025-09-10   12000
    4 2025-07-12   11000
    


```python
# Mostrar fechas de julio de cualquier año
filtro_julio = datos["fecha"].dt.month == 7
datos_julio = datos[filtro_julio]
print(datos_julio)
```

           fecha  ventas
    1 2025-07-01    7820
    4 2025-07-12   11000
    

### Cálculos estadísticons con fechas
Pandas también nos permite realizar cálculos estadísticos basados en fechas. Por ejemplo, podemos calcular la media, la mediana, el máximo, el mínimo, etc., de una columna de fechas o de una columna numérica agrupada por fechas. Para ello podemos usar las funciones de agregación de Pandas, como `groupby()`, `mean()`, `median()`, `max()`, `min()`, etc., junto con la propiedad `dt` para agrupar por diferentes componentes de las fechas (por ejemplo, por año, por mes, por día de la semana, etc.).
Ejemplo:


```python
print("Fecha media: ", datos["fecha"].mean())  # Calcula la fecha media de la columna "fecha"
print("Fecha mínima: ", datos["fecha"].min())   # Calcula la fecha mínima de la columna "fecha"
print("Fecha máxima: ", datos["fecha"].max())   # Calcula la fecha máxima de la columna "fecha"
print("Mediana de la fecha: ", datos["fecha"].median())   # Calcula la mediana de la columna "fecha"

```

    Fecha media:  2025-07-24 04:48:00
    Fecha mínima:  2025-06-15 00:00:00
    Fecha máxima:  2025-09-10 00:00:00
    Mediana de la fecha:  2025-07-12 00:00:00
    

### Remuestreo de fechas
Pandas también nos permite realizar remuestreo de datos basados en fechas. El remuestreo es una técnica que consiste en cambiar la frecuencia de los datos temporales, por ejemplo, convertir datos diarios a datos mensuales, o datos horarios a datos diarios. Para ello podemos usar el método `resample()` de Pandas, que nos permite especificar la nueva frecuencia de los datos y la función de agregación que queremos aplicar a los datos remuestreados (por ejemplo, `mean()`, `sum()`, `max()`, etc.).

Para ello la columna de la fecha debe ser el índice del DataFrame, por lo que primero tendríamos que establecer la columna de fechas como índice usando el método `set_index()` o la propiedad `index`. Luego podríamos usar el método `resample()` para cambiar la frecuencia de los datos y aplicar la función de agregación deseada.


```python
datos = pd.DataFrame({
    "fecha":["2025-06-15", "2025-07-01", "2025-08-20","2025-09-10","2025-07-12"],
    "ventas":[9800, 7820, 8930, 12000, 11000]
})
datos["fecha"] = pd.to_datetime(datos["fecha"])  # Convertimos la columna "fecha" a tipo datetime
datos.set_index("fecha", inplace=True) # Modificamos el DataFrame original
datos.resample("ME").sum ()  # Remuestreamos los datos mensualmente y sumamos las ventas de cada mes
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ventas</th>
    </tr>
    <tr>
      <th>fecha</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2025-06-30</th>
      <td>9800</td>
    </tr>
    <tr>
      <th>2025-07-31</th>
      <td>18820</td>
    </tr>
    <tr>
      <th>2025-08-31</th>
      <td>8930</td>
    </tr>
    <tr>
      <th>2025-09-30</th>
      <td>12000</td>
    </tr>
  </tbody>
</table>
</div>



Visualmente el resultado no es muy atractivo al mostrar la fecha como índice en el que aparece (en este caso) el último día del mes. 

Esta forma de remuestrear es muy común para trabajar con series temporales en Pandas, ya que nos permite realizar operaciones de remuestreo y agregación de manera sencilla.

Si deseamos cambiar el formato de la fecha en el índice después de realizar el remuestreo, podemos usar el método `strftime()` para formatear las fechas del índice a un formato más legible. Para ello, después de realizar el remuestreo, podemos acceder al índice del DataFrame resultante y aplicar el método `strftime()` para formatear las fechas según nuestras necesidades.
Ejemplo:


```python
datos_sampleados = datos.resample("ME").sum ()  # Remuestreamos los datos mensualmente y sumamos las ventas de cada mes
datos_sampleados.set_index(datos_sampleados.index.strftime("%Y-%m"), inplace=True)  # Formateamos las fechas del índice a formato Año-Mes
print(datos_sampleados)
```

             ventas
    fecha          
    2025-06    9800
    2025-07   18820
    2025-08    8930
    2025-09   12000
    

Los códigos para remuestrear del método `resample()` son:
- `ME`: Fin de mes
- `MS`: Inicio de mes
- `A`: Fin de año
- `AS`: Inicio de año
- `Q`: Fin de trimestre
- `QS`: Inicio de trimestre
- `W`: Semanal (por defecto, el domingo como primer día de la semana)
- `D`: Diario
- `H`: Horario
- `T` o `min`: Minutal
- `S`: Segundal

### Intervalos temporales en Pandas
Pandas también tiene un tipo de dato específico para manejar intervalos de tiempo, llamado `Timedelta`. Este tipo de dato es similar a la clase `timedelta` del módulo `datetime`, pero con funcionalidades adicionales que facilitan el trabajo con intervalos de tiempo en series temporales.

Panda posee un método llamado `to_timedelta()` que permite convertir diferentes formatos de intervalos de tiempo a objetos `Timedelta`, lo que facilita la manipulación de intervalos temporales en nuestros análisis. Además, los objetos `Timedelta` tienen varias propiedades y métodos que nos permiten realizar operaciones con intervalos de tiempo de manera sencilla.



```python
datos2 = pd.DataFrame({
    "duracion" : ["1 day 3 hours", "2 days 5 hours", "3 days 2 hours", "3 days 9:15:00","1 day 8:23:00"],
    "coste" : [150, 370, 510, 620, 190]
})
datos2["duracion"] = pd.to_timedelta(datos2["duracion"])  # Convertimos
print(datos2)
```

             duracion  coste
    0 1 days 03:00:00    150
    1 2 days 05:00:00    370
    2 3 days 02:00:00    510
    3 3 days 09:15:00    620
    4 1 days 08:23:00    190
    

Para convertir columnas con otros formatos de intervalos el texto tiene que ser válido. Ejemplos de textos convertibles (este método no dispone de parámetro format) son:
- "1 day 3 hours"
- "2 days 5 hours"
- "3 days 8:15:23"
- "4 days 12:30:45.123456"

No es válido: `1 day 8:15` ya que en esa forma se requiere llegar a segundos. 

### Crear secuencias temporales
El método `date_range()` de Pandas nos permite crear secuencias de fechas con una frecuencia específica. Este método es útil para generar rangos de fechas para análisis de series temporales, creación de índices de tiempo, o para cualquier situación en la que necesitemos una secuencia de fechas.
El método `date_range()` recibe varios parámetros, entre los más comunes están:
- `start`: Fecha de inicio de la secuencia (puede ser un string, un objeto `Timestamp`, o un objeto `datetime`).
- `end`: Fecha de fin de la secuencia (puede ser un string, un objeto `Timestamp`, o un objeto `datetime`).
- `periods`: Número de períodos a generar (si se especifica, se ignora el parámetro `end`).
- `freq`: Frecuencia de la secuencia (por ejemplo "ME" para fin de mes, "D" para diario, "H" para horario, etc.). SOn los mismos códigos que los que se usan para el método `resample()`.



```python
secuencia = pd.date_range(start="2025-01-01", 
                          end="2025-12-31", 
                          freq="ME")  # Crea una secuencia de fechas con frecuencia mensual (fin de mes)
print(secuencia)
```

    DatetimeIndex(['2025-01-31', '2025-02-28', '2025-03-31', '2025-04-30',
                   '2025-05-31', '2025-06-30', '2025-07-31', '2025-08-31',
                   '2025-09-30', '2025-10-31', '2025-11-30', '2025-12-31'],
                  dtype='datetime64[ns]', freq='ME')
    


```python
secuencia = pd.date_range(start="2025-01-01", periods=24, freq="ME")  
# crea una secuencia que parte del 1 de enero de 2025 y que durará 24 meses 
print(secuencia)
```

    DatetimeIndex(['2025-01-31', '2025-02-28', '2025-03-31', '2025-04-30',
                   '2025-05-31', '2025-06-30', '2025-07-31', '2025-08-31',
                   '2025-09-30', '2025-10-31', '2025-11-30', '2025-12-31',
                   '2026-01-31', '2026-02-28', '2026-03-31', '2026-04-30',
                   '2026-05-31', '2026-06-30', '2026-07-31', '2026-08-31',
                   '2026-09-30', '2026-10-31', '2026-11-30', '2026-12-31'],
                  dtype='datetime64[ns]', freq='ME')
    

El objeto que crea este método es de tipo `DatetimeIndex`, que es un tipo de índice especializado para manejar fechas y horas en Pandas. Este índice nos permite realizar operaciones de filtrado, selección y manipulación de datos basados en fechas de manera eficiente.

Para relacionar un DataFrame ya existente a una secuencia de fechas creada con `date_range()`, podemos establecer la secuencia de fechas como el índice del DataFrame usando el método `set_index()`. Esto nos permitirá trabajar con el DataFrame utilizando las fechas como índice, lo que facilita el análisis de series temporales y la realización de operaciones basadas en fechas.

Ejemplo:


```python
# Dataframe de ejemplo con fechas y valores de ventas, con 20 filas para que se vea mejor el resultado del remuestreo
datos = pd.DataFrame({
    "fecha": ["2025-06-15", "2025-07-01", "2025-08-20", "2025-09-10", "2025-07-12",
              "2025-10-05", "2025-11-20", "2025-12-15", "2026-01-10", "2026-02-25",
              "2026-03-15", "2026-04-10", "2026-05-20", "2026-06-15", "2026-07-01",
              "2026-08-20", "2026-09-10", "2026-10-05", "2026-11-20", "2026-12-15"],
    "ventas": [9800, 7820, 8930, 6740, 8700, 9230, 7600, 6890, 7200, 8100,
               7210, 6820, 9230, 4900, 5800, 8230, 7200, 9600, 8240, 9050]
})
datos["fecha"] = pd.to_datetime(datos["fecha"])  # Convertimos la columna "fecha" a tipo datetime
secuencia
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>fecha</th>
      <th>ventas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2025-06-15</td>
      <td>9800</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2025-07-01</td>
      <td>7820</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2025-08-20</td>
      <td>8930</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2025-09-10</td>
      <td>6740</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2025-07-12</td>
      <td>8700</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2025-10-05</td>
      <td>9230</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2025-11-20</td>
      <td>7600</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2025-12-15</td>
      <td>6890</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2026-01-10</td>
      <td>7200</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2026-02-25</td>
      <td>8100</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2026-03-15</td>
      <td>7210</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2026-04-10</td>
      <td>6820</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2026-05-20</td>
      <td>9230</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2026-06-15</td>
      <td>4900</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2026-07-01</td>
      <td>5800</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2026-08-20</td>
      <td>8230</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2026-09-10</td>
      <td>7200</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2026-10-05</td>
      <td>9600</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2026-11-20</td>
      <td>8240</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2026-12-15</td>
      <td>9050</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
