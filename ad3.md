# Actividad Dirigida 3
En esta actividad dirigida haremos uso de la [API de Covid-19](https://covid19api.com/#subscribe "API Covid") creada por Kyle Redelinghuys, a través de la cual se puede consultar información en tiempo real de la evolución de la pandemia COVID-19.

Los pasos que se seguirán en este código serán los siguientes:
1. Instalación de la librería Pandas y configuración
2. Variables
3. Creación de *Dataframe*
4. Explorar tabla
5. Acceso a datos
6. Tiempo real España
7. Tiempo real Colombia
8. Comparativa España-Colombia
9. Triple comparativa España-Colombia-Argentina
10. Seleccionar más columnas
11. Exportar datos

## Instalación de la librería Pandas y configuración
Lo primero que debemos hacer es instalar la librería [Pandas](https://pandas.pydata.org "Pandas") que se trata de una herramienta de análisis y manipulación de datos en código abierto construida sobre el lenguaje de programación Python. Para ello, haremos uso de la orden ```!pip install pandas```, ya que el ```pip``` es un gestor de paquetes estándar para este lenguaje que permite que se instalen y gestionen paquetes que no forman parte de la biblioteca estándar de Python.

Tras este primer paso, lo siguiente será configurar e introducir la librería de Pandas en este código y darle a pandas el alias de pd a través de la orden ```import pandas as pd```.

## Variables
En este segundo paso, lo primero que debemos hacer es definir la [URL](https://api.covid19api.com/countries "URL") en la que queremos hacer web scraping y obtener los datos. En este usaremos la orden ```url = 'https://api.covid19api.com/countries'``` para recabar la lista de países en los que se muestra la evolución en tiempo real de la pandemia.

## Creación de *Dataframe*
En este paso, utilizamos la función ```read_json``` de pandas con el objetivo de leer archivos en cadena de cualquier formato (archivos comprimidos o URLs, entre otros) en JSON de la API. 
En este caso la lectura se realizará desde una [URL API](https://api.covid19api.com/countries "URL API") y además haremos uso de la estrucutra de datos, DataFrame, es decir, ```df``` para guardar la información obtenida de distintos tipos en columnas como si fuera una hoja de cálculo. Para ello, utilizaremos la siguiente función: ```df = pd.read_json(url)```, y después simplemente introduciremos la orden ```df``` para que nos imprima la tabla de la [URL API](https://api.covid19api.com/countries "URL API") que hemos definido previamente. 

## Explorar tabla
El siguiente paso será explorar la tabla que hemos obtenido, para que nos muestre de un Data Frame: los países que aparecen en la cabecera de la lista a través de la orden ```df.head ()```, los países que aparecen en la cola a través de la orden ```df.tail ()``` y los datos estadísticos básicos a través de la orden ```df.describe ()```.

## Acceso a datos
En este apartado, lo que queremos es tener acceso a los datos que se encuentren bajo el nombre de **"Country"** y que estos se muestren en columnas, por lo que haremos uso del Data Frame a través de la siguiente orden: ```df['Country']```.

Asimismo, en este apartado, quisimos hacer una búsqueda más concreta, por lo que no solo buscamos los datos que se encontrasen bajo el nombre de **"Country"**, sino que se imprimiera justo el país que aparece en la posición *200* de la lista a través de la orden ```df['Country'][200]```, en el que el resultado fue Angola.

## Tiempo real España
### Definir URL
En este sexto punto, lo que queremos que es la información que se muestre en tiempo real de la evolución de la pandemia sea solo en España, por lo que se definirá una [URL](https://api.covid19api.com/country/spain/status/confirmed/live "Datos España") diferente a la previamente establecida, llamada ```url_es```.

Después, estableceremos la orden ```df_es``` en la que se obtendrá la información relativa a España a través de la estrucutra de datos Data Frame, haciendo uso de la función: ```df_es = pd.read_json(url_es)```. 

Finalmente,  simplemente introduciremos la orden ```df_es``` para que nos imprima la tabla de la [URL](https://api.covid19api.com/country/spain/status/confirmed/live "Datos España") que hemos definido previamente. 

### Funciones relevantes
Tras este primer paso, en el caso de España hicimos uso de diferentes funciones, con el objetivo de obtener información variada de la [URL](https://api.covid19api.com/country/spain/status/confirmed/live "Datos España") definida previamente.

- ```df_es.info()```: Esta función Pandas es utilizada para obtener un resumen conciso del marco de datos, que en este caso se centra solo en España. De esta manera, se imprimen un total de 10 columnas en las que se encuentra dividida la información, que en este caso son: "Country", "CountryCode", "Province", "City", "CityCode", "Lat", "Lon", "Cases", "Status" y "Date".            
- ```df_es.set_index('Date')```: Esta función se utiliza para mostrar la columna **"Date"** como índice de la tabla y después se imprimiran el resto de columnas del marco de datos.             
- ```df_es.set_index('Date')['Cases']```: Esta función se utiliza para mostrar la columna **"Date"** como índice de la tabla y que después aparezca la información relativa a los **"Cases"**.
- ```df_es.set_index('Date')['Cases'].plot()```: Al igual que en la función anterior, esta se utiliza para mostrar la columna **"Date"** como índice de la tabla y que después aparezca la información relativa a los **"Cases"**. Además, se añade la orden ```.plot()``` para que la información se dibuje en un polígono con los vértices dados por las coordenadas de la lista x ("date") y de la lista y ("cases").
- ```df_es.set_index('Date')['Cases'].plot(title='Casos de Covid19 en España')```: Esta función sirve para lo mismo que la mencionada previamente, pero en este caso, se le añade el título "Casos de Covid19 en España" a dicho gráfico.

## Tiempo real Colombia
Al igual que el paso anterior, en este lo que queremos que es la información que se muestre en tiempo real de la evolución de la pandemia sea solo en Colombia, por lo que se definirá una [URL](https://api.covid19api.com/country/colombia/status/confirmed/live "Datos Colombia") diferente a la previamente establecida, llamada ```url_co```.

Asimismo, estableceremos la orden ```df_co``` en la que se obtendrá la información relativa a Colombia a través de la estrucutra de datos Data Frame, haciendo uso de la función: ```df_co = pd.read_json(url_co)```. 

Finalmente, haremos uso de la función ```df_co.set_index('Date')['Cases'].plot(title='Casos de Covid19 en Colombia')``` para que se muestre la columna **"Date"** como índice de la tabla y que después aparezca la información relativa a los **"Cases"**, y toda esta información se dibuje en un gráfico a través de la orden ```.plot()``` con el título de "Casos de Covid19 en Colombia".


## Comparativa España-Colombia
En este apartado, 

## Triple comparativa España-Colombia-Argentina

## Seleccionar más columnas

## Exportar datos

