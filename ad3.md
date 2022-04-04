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
En este apartado, comparemos la información en tiempo real de la evolución de la pandemia en España y en Colombia. Para ello, definiremos la función ```df_es.set_index('Date')['Cases']``` como ```casos_es``` en el caso de España y la función ```df_co.set_index('Date')['Cases']``` como ```casos_co``` para los datos de Colombia.

Para poder hacer la comparación de ambos dataframes a lo largo de la fila ```axis = 1```, debemos hacer uso de la siguiente función: ```pd.concat([casos_es,casos_co],axis=1)``` y la definiremos como ```vs```. Tras este paso, simplemente introduciremos la orden ```vs``` para que nos imprima la tabla comparativa de ambos países.

Como en ambas columnas aparecían tituladas bajo el nombre de **"Cases"**, a través de la función ```vs.columns = ['España', 'Colombia']``` diferenciamos ambos títulos, estableciendo para la primera columna el nombre de España y para la segunda, Colombia.

Finalmente, con el objetivo de poder visualizar esta comparativa en un gráfico, estableceremos la siguiente función: ```vs.plot(title='España vs Colombia',kind='area')```. El método plot de Pandas tiene un parámetro kind que nos ayuda a cambiar el tipo de gráfico que queremos dibujar, que en este caso será el de tipo área.

## Triple comparativa España-Colombia-Argentina
En este apartado, comparemos la información en tiempo real de la evolución de la pandemia en España, en Colombia y Argentina. Para ello, definiremos la función ```df_es.set_index('Date')['Cases']``` como ```casos_es``` en el caso de España, la función ```df_co.set_index('Date')['Cases']``` como ```casos_co``` para los datos de Colombia y la función de ```df_ag.set_index('Date')['Cases']```como ```casos_ag```.

Para poder hacer la concatenación de los tres dataframes a lo largo de la fila ```axis = 1```, debemos hacer uso de la siguiente función: ```pd.concat([casos_es,casos_co,casos_ag],axis=1)``` y la definiremos como ```vs2```. Tras este paso, simplemente introduciremos la orden ```vs2``` para que nos imprima la tabla comparativa de los tres países.

Como las tres columnas aparecían tituladas bajo el nombre de **"Cases"**, a través de la función ```vs.columns = ['España', 'Colombia', 'Argentina']``` diferenciamos ambos títulos, estableciendo para la primera columna el nombre de España, la segunda el de Colombia y la tercerda el de Argentina.

Finalmente, con el objetivo de poder visualizar esta comparativa en un gráfico, estableceremos la siguiente función: ```vs2.plot(title='España, Colombia y Argentina')```. El método plot de Pandas le pondremos el título de "España, Colombia y Argentina".

## Seleccionar más columnas
En este apartado, haremos uso de la función: ```df_es.set_index('Date')[['Cases','Lon']]```. Esta obtendrá los datos de España, mostrando la columna **"Date"** como índice de la tabla y después aparecerá la información relativa a los casos (**"Cases"**) y la longitud (**"Lon"**) en las columnas siguientes.

## Exportar datos
En este último paso, haremos uso de las funciones ```vs.to_csv('vs.csv')```y ```vs2.to_csv('vs2.csv')``` para guardar ambas comparativas en un archivo CSV (valores separados por comas), el cuál tiene un formato específico que permite agrupar los datos en un formato de tabla estructurada. 

Por último, además de los datos, también guardamos los gráficos relativos a ambas comparativas como archivo png, es decir, como una imagen, utilizando la siguiente función: ```grafico =vs.plot() fig = grafico.get_figure() fig.savefig('vs.png')```.



```
{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "4a337475",
   "metadata": {},
   "source": [
    "# Uso de API de Covid19 con Pandas"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9ec62152",
   "metadata": {},
   "source": [
    "- https://covid19api.com/\n",
    "- https://api.covid19api.com/"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3f5ba88a",
   "metadata": {},
   "source": [
    "## Instalación Pandas"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "6225764a",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Requirement already satisfied: pandas in c:\\programdata\\anaconda3\\lib\\site-packages (1.2.4)\n",
      "Requirement already satisfied: python-dateutil>=2.7.3 in c:\\programdata\\anaconda3\\lib\\site-packages (from pandas) (2.8.1)\n",
      "Requirement already satisfied: numpy>=1.16.5 in c:\\programdata\\anaconda3\\lib\\site-packages (from pandas) (1.20.1)\n",
      "Requirement already satisfied: pytz>=2017.3 in c:\\programdata\\anaconda3\\lib\\site-packages (from pandas) (2021.1)\n",
      "Requirement already satisfied: six>=1.5 in c:\\programdata\\anaconda3\\lib\\site-packages (from python-dateutil>=2.7.3->pandas) (1.15.0)\n"
     ]
    }
   ],
   "source": [
    "!pip install pandas"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "dc530463",
   "metadata": {},
   "source": [
    "## Configuración"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "6350d66b",
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "4fa6eab0",
   "metadata": {},
   "source": [
    "## Variables"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "a04b57be",
   "metadata": {},
   "outputs": [],
   "source": [
    "url ='https://api.covid19api.com/countries'"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "4409dcba",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'https://api.covid19api.com/countries'"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "url"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "e266c9cc",
   "metadata": {},
   "source": [
    "## Creación de *Dataframe*\n",
    "Utilizamos la función `red_json` de *pandas* para leer los datos en JSON de la API:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "43eb1c5b",
   "metadata": {},
   "outputs": [],
   "source": [
    "df = pd.read_json(url)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "9eb801a7",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Country</th>\n",
       "      <th>Slug</th>\n",
       "      <th>ISO2</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Republic of Kosovo</td>\n",
       "      <td>kosovo</td>\n",
       "      <td>XK</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Botswana</td>\n",
       "      <td>botswana</td>\n",
       "      <td>BW</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Central African Republic</td>\n",
       "      <td>central-african-republic</td>\n",
       "      <td>CF</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Hungary</td>\n",
       "      <td>hungary</td>\n",
       "      <td>HU</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Peru</td>\n",
       "      <td>peru</td>\n",
       "      <td>PE</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>243</th>\n",
       "      <td>Malta</td>\n",
       "      <td>malta</td>\n",
       "      <td>MT</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>244</th>\n",
       "      <td>San Marino</td>\n",
       "      <td>san-marino</td>\n",
       "      <td>SM</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>245</th>\n",
       "      <td>Gibraltar</td>\n",
       "      <td>gibraltar</td>\n",
       "      <td>GI</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>246</th>\n",
       "      <td>Uganda</td>\n",
       "      <td>uganda</td>\n",
       "      <td>UG</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>247</th>\n",
       "      <td>Vanuatu</td>\n",
       "      <td>vanuatu</td>\n",
       "      <td>VU</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>248 rows × 3 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                      Country                      Slug ISO2\n",
       "0          Republic of Kosovo                    kosovo   XK\n",
       "1                    Botswana                  botswana   BW\n",
       "2    Central African Republic  central-african-republic   CF\n",
       "3                     Hungary                   hungary   HU\n",
       "4                        Peru                      peru   PE\n",
       "..                        ...                       ...  ...\n",
       "243                     Malta                     malta   MT\n",
       "244                San Marino                san-marino   SM\n",
       "245                 Gibraltar                 gibraltar   GI\n",
       "246                    Uganda                    uganda   UG\n",
       "247                   Vanuatu                   vanuatu   VU\n",
       "\n",
       "[248 rows x 3 columns]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "89fcea72",
   "metadata": {},
   "source": [
    "## Explorar tabla\n",
    "- Cabecera\n",
    "- Cola\n",
    "- Descripción"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "d67bbd55",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Country</th>\n",
       "      <th>Slug</th>\n",
       "      <th>ISO2</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Republic of Kosovo</td>\n",
       "      <td>kosovo</td>\n",
       "      <td>XK</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Botswana</td>\n",
       "      <td>botswana</td>\n",
       "      <td>BW</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Central African Republic</td>\n",
       "      <td>central-african-republic</td>\n",
       "      <td>CF</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Hungary</td>\n",
       "      <td>hungary</td>\n",
       "      <td>HU</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Peru</td>\n",
       "      <td>peru</td>\n",
       "      <td>PE</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                    Country                      Slug ISO2\n",
       "0        Republic of Kosovo                    kosovo   XK\n",
       "1                  Botswana                  botswana   BW\n",
       "2  Central African Republic  central-african-republic   CF\n",
       "3                   Hungary                   hungary   HU\n",
       "4                      Peru                      peru   PE"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head ()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "c48d1fb4",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Country</th>\n",
       "      <th>Slug</th>\n",
       "      <th>ISO2</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>243</th>\n",
       "      <td>Malta</td>\n",
       "      <td>malta</td>\n",
       "      <td>MT</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>244</th>\n",
       "      <td>San Marino</td>\n",
       "      <td>san-marino</td>\n",
       "      <td>SM</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>245</th>\n",
       "      <td>Gibraltar</td>\n",
       "      <td>gibraltar</td>\n",
       "      <td>GI</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>246</th>\n",
       "      <td>Uganda</td>\n",
       "      <td>uganda</td>\n",
       "      <td>UG</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>247</th>\n",
       "      <td>Vanuatu</td>\n",
       "      <td>vanuatu</td>\n",
       "      <td>VU</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "        Country        Slug ISO2\n",
       "243       Malta       malta   MT\n",
       "244  San Marino  san-marino   SM\n",
       "245   Gibraltar   gibraltar   GI\n",
       "246      Uganda      uganda   UG\n",
       "247     Vanuatu     vanuatu   VU"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.tail ()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "1f2724ee",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Country</th>\n",
       "      <th>Slug</th>\n",
       "      <th>ISO2</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>248</td>\n",
       "      <td>248</td>\n",
       "      <td>248</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>unique</th>\n",
       "      <td>248</td>\n",
       "      <td>248</td>\n",
       "      <td>248</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>top</th>\n",
       "      <td>Monaco</td>\n",
       "      <td>virgin-islands</td>\n",
       "      <td>AD</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>freq</th>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "       Country            Slug ISO2\n",
       "count      248             248  248\n",
       "unique     248             248  248\n",
       "top     Monaco  virgin-islands   AD\n",
       "freq         1               1    1"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe ()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2cb3ca6c",
   "metadata": {},
   "source": [
    "## Acceso a datos"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "246eff79",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0            Republic of Kosovo\n",
       "1                      Botswana\n",
       "2      Central African Republic\n",
       "3                       Hungary\n",
       "4                          Peru\n",
       "                 ...           \n",
       "243                       Malta\n",
       "244                  San Marino\n",
       "245                   Gibraltar\n",
       "246                      Uganda\n",
       "247                     Vanuatu\n",
       "Name: Country, Length: 248, dtype: object"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['Country']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "d472a481",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'Angola'"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df['Country'][200]"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "5fe31178",
   "metadata": {},
   "source": [
    "## Tiempo real España"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "ca5dad73",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Country</th>\n",
       "      <th>CountryCode</th>\n",
       "      <th>Province</th>\n",
       "      <th>City</th>\n",
       "      <th>CityCode</th>\n",
       "      <th>Lat</th>\n",
       "      <th>Lon</th>\n",
       "      <th>Cases</th>\n",
       "      <th>Status</th>\n",
       "      <th>Date</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2020-01-22 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2020-01-23 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2020-01-24 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2020-01-25 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2020-01-26 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>794</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11451676</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2022-03-26 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>795</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11451676</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2022-03-27 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>796</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11451676</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2022-03-28 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>797</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11508309</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2022-03-29 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>798</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11508309</td>\n",
       "      <td>confirmed</td>\n",
       "      <td>2022-03-30 00:00:00+00:00</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>799 rows × 10 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "    Country CountryCode Province City CityCode    Lat   Lon     Cases  \\\n",
       "0     Spain          ES                         40.46 -3.75         0   \n",
       "1     Spain          ES                         40.46 -3.75         0   \n",
       "2     Spain          ES                         40.46 -3.75         0   \n",
       "3     Spain          ES                         40.46 -3.75         0   \n",
       "4     Spain          ES                         40.46 -3.75         0   \n",
       "..      ...         ...      ...  ...      ...    ...   ...       ...   \n",
       "794   Spain          ES                         40.46 -3.75  11451676   \n",
       "795   Spain          ES                         40.46 -3.75  11451676   \n",
       "796   Spain          ES                         40.46 -3.75  11451676   \n",
       "797   Spain          ES                         40.46 -3.75  11508309   \n",
       "798   Spain          ES                         40.46 -3.75  11508309   \n",
       "\n",
       "        Status                      Date  \n",
       "0    confirmed 2020-01-22 00:00:00+00:00  \n",
       "1    confirmed 2020-01-23 00:00:00+00:00  \n",
       "2    confirmed 2020-01-24 00:00:00+00:00  \n",
       "3    confirmed 2020-01-25 00:00:00+00:00  \n",
       "4    confirmed 2020-01-26 00:00:00+00:00  \n",
       "..         ...                       ...  \n",
       "794  confirmed 2022-03-26 00:00:00+00:00  \n",
       "795  confirmed 2022-03-27 00:00:00+00:00  \n",
       "796  confirmed 2022-03-28 00:00:00+00:00  \n",
       "797  confirmed 2022-03-29 00:00:00+00:00  \n",
       "798  confirmed 2022-03-30 00:00:00+00:00  \n",
       "\n",
       "[799 rows x 10 columns]"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "url_es = 'https://api.covid19api.com/country/spain/status/confirmed/live'\n",
    "df_es = pd.read_json(url_es)\n",
    "df_es"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "1108bf71",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 799 entries, 0 to 798\n",
      "Data columns (total 10 columns):\n",
      " #   Column       Non-Null Count  Dtype              \n",
      "---  ------       --------------  -----              \n",
      " 0   Country      799 non-null    object             \n",
      " 1   CountryCode  799 non-null    object             \n",
      " 2   Province     799 non-null    object             \n",
      " 3   City         799 non-null    object             \n",
      " 4   CityCode     799 non-null    object             \n",
      " 5   Lat          799 non-null    float64            \n",
      " 6   Lon          799 non-null    float64            \n",
      " 7   Cases        799 non-null    int64              \n",
      " 8   Status       799 non-null    object             \n",
      " 9   Date         799 non-null    datetime64[ns, UTC]\n",
      "dtypes: datetime64[ns, UTC](1), float64(2), int64(1), object(6)\n",
      "memory usage: 62.5+ KB\n"
     ]
    }
   ],
   "source": [
    "df_es.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "6d81e22c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Country</th>\n",
       "      <th>CountryCode</th>\n",
       "      <th>Province</th>\n",
       "      <th>City</th>\n",
       "      <th>CityCode</th>\n",
       "      <th>Lat</th>\n",
       "      <th>Lon</th>\n",
       "      <th>Cases</th>\n",
       "      <th>Status</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>0</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-26 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11451676</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11451676</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11451676</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11508309</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>Spain</td>\n",
       "      <td>ES</td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td></td>\n",
       "      <td>40.46</td>\n",
       "      <td>-3.75</td>\n",
       "      <td>11508309</td>\n",
       "      <td>confirmed</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>799 rows × 9 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                          Country CountryCode Province City CityCode    Lat  \\\n",
       "Date                                                                          \n",
       "2020-01-22 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2020-01-23 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2020-01-24 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2020-01-25 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2020-01-26 00:00:00+00:00   Spain          ES                         40.46   \n",
       "...                           ...         ...      ...  ...      ...    ...   \n",
       "2022-03-26 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2022-03-27 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2022-03-28 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2022-03-29 00:00:00+00:00   Spain          ES                         40.46   \n",
       "2022-03-30 00:00:00+00:00   Spain          ES                         40.46   \n",
       "\n",
       "                            Lon     Cases     Status  \n",
       "Date                                                  \n",
       "2020-01-22 00:00:00+00:00 -3.75         0  confirmed  \n",
       "2020-01-23 00:00:00+00:00 -3.75         0  confirmed  \n",
       "2020-01-24 00:00:00+00:00 -3.75         0  confirmed  \n",
       "2020-01-25 00:00:00+00:00 -3.75         0  confirmed  \n",
       "2020-01-26 00:00:00+00:00 -3.75         0  confirmed  \n",
       "...                         ...       ...        ...  \n",
       "2022-03-26 00:00:00+00:00 -3.75  11451676  confirmed  \n",
       "2022-03-27 00:00:00+00:00 -3.75  11451676  confirmed  \n",
       "2022-03-28 00:00:00+00:00 -3.75  11451676  confirmed  \n",
       "2022-03-29 00:00:00+00:00 -3.75  11508309  confirmed  \n",
       "2022-03-30 00:00:00+00:00 -3.75  11508309  confirmed  \n",
       "\n",
       "[799 rows x 9 columns]"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_es.set_index('Date')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "5fb69e45",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Date\n",
       "2020-01-22 00:00:00+00:00           0\n",
       "2020-01-23 00:00:00+00:00           0\n",
       "2020-01-24 00:00:00+00:00           0\n",
       "2020-01-25 00:00:00+00:00           0\n",
       "2020-01-26 00:00:00+00:00           0\n",
       "                               ...   \n",
       "2022-03-26 00:00:00+00:00    11451676\n",
       "2022-03-27 00:00:00+00:00    11451676\n",
       "2022-03-28 00:00:00+00:00    11451676\n",
       "2022-03-29 00:00:00+00:00    11508309\n",
       "2022-03-30 00:00:00+00:00    11508309\n",
       "Name: Cases, Length: 799, dtype: int64"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_es.set_index('Date')['Cases']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "bb11e87c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Date'>"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "df_es.set_index('Date')['Cases'].plot()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "6e49009f",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:title={'center':'Casos de Covid19 en España'}, xlabel='Date'>"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "df_es.set_index('Date')['Cases'].plot(title='Casos de Covid19 en España')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "591354b8",
   "metadata": {},
   "source": [
    "## Tiempo real Colombia"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "39f6e955",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:title={'center':'Casos de Covid19 en Colombia'}, xlabel='Date'>"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "url_co = 'https://api.covid19api.com/country/colombia/status/confirmed/live'\n",
    "df_co = pd.read_json(url_co)\n",
    "df_co.set_index('Date')['Cases'].plot(title='Casos de Covid19 en Colombia')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "20478c14",
   "metadata": {},
   "source": [
    "## Comparativa España-Colombia"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "bf1fd334",
   "metadata": {},
   "outputs": [],
   "source": [
    "casos_es = df_es.set_index('Date')['Cases']\n",
    "casos_co = df_co.set_index('Date')['Cases']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "f8dfd14b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Cases</th>\n",
       "      <th>Cases</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-26 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083291</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083643</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083939</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>6084240</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>6084551</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>799 rows × 2 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                              Cases    Cases\n",
       "Date                                        \n",
       "2020-01-22 00:00:00+00:00         0        0\n",
       "2020-01-23 00:00:00+00:00         0        0\n",
       "2020-01-24 00:00:00+00:00         0        0\n",
       "2020-01-25 00:00:00+00:00         0        0\n",
       "2020-01-26 00:00:00+00:00         0        0\n",
       "...                             ...      ...\n",
       "2022-03-26 00:00:00+00:00  11451676  6083291\n",
       "2022-03-27 00:00:00+00:00  11451676  6083643\n",
       "2022-03-28 00:00:00+00:00  11451676  6083939\n",
       "2022-03-29 00:00:00+00:00  11508309  6084240\n",
       "2022-03-30 00:00:00+00:00  11508309  6084551\n",
       "\n",
       "[799 rows x 2 columns]"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.concat([casos_es,casos_co],axis=1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "6554aafb",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Cases</th>\n",
       "      <th>Cases</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-26 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083291</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083643</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083939</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>6084240</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>6084551</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>799 rows × 2 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                              Cases    Cases\n",
       "Date                                        \n",
       "2020-01-22 00:00:00+00:00         0        0\n",
       "2020-01-23 00:00:00+00:00         0        0\n",
       "2020-01-24 00:00:00+00:00         0        0\n",
       "2020-01-25 00:00:00+00:00         0        0\n",
       "2020-01-26 00:00:00+00:00         0        0\n",
       "...                             ...      ...\n",
       "2022-03-26 00:00:00+00:00  11451676  6083291\n",
       "2022-03-27 00:00:00+00:00  11451676  6083643\n",
       "2022-03-28 00:00:00+00:00  11451676  6083939\n",
       "2022-03-29 00:00:00+00:00  11508309  6084240\n",
       "2022-03-30 00:00:00+00:00  11508309  6084551\n",
       "\n",
       "[799 rows x 2 columns]"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "vs = pd.concat([casos_es,casos_co],axis=1)\n",
    "vs"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "767a2fa2",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>España</th>\n",
       "      <th>Colombia</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-26 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083291</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083643</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>6083939</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>6084240</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>6084551</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>799 rows × 2 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                             España  Colombia\n",
       "Date                                         \n",
       "2020-01-22 00:00:00+00:00         0         0\n",
       "2020-01-23 00:00:00+00:00         0         0\n",
       "2020-01-24 00:00:00+00:00         0         0\n",
       "2020-01-25 00:00:00+00:00         0         0\n",
       "2020-01-26 00:00:00+00:00         0         0\n",
       "...                             ...       ...\n",
       "2022-03-26 00:00:00+00:00  11451676   6083291\n",
       "2022-03-27 00:00:00+00:00  11451676   6083643\n",
       "2022-03-28 00:00:00+00:00  11451676   6083939\n",
       "2022-03-29 00:00:00+00:00  11508309   6084240\n",
       "2022-03-30 00:00:00+00:00  11508309   6084551\n",
       "\n",
       "[799 rows x 2 columns]"
      ]
     },
     "execution_count": 22,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "vs.columns = ['España', 'Colombia']\n",
    "vs"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "ffb0bacb",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:title={'center':'España vs Colombia'}, xlabel='Date'>"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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uOaaa3j77bcZN+7IdevKo1xEhH/84x/06NGDlStXsmTJEsrLj/wjtWzZ8vDzYDBIOBymtLSUu+66i9dff53Vq1dzxx132BBJY5qDXcvhzR/AlDGwYxEE0iGQBuri9YpHr9ZEX9WUfiJyp4jcGbHZ1cDHqloUsawHMNef9m8R8J6qflin6BqBwsJCCgoKuPTSS3n44YePavG/9tpruK7L5s2b2bJlC4MHD6agoIBevXoRCAR4/vnncRynxuNXJPWuXbtSWFjI66/XfHXdGNPIlRbA3Ifh6QthzetQdshb7obADdfrkNGMupkYxTZT8YZhRi7bApxc1faNVeU++nHjxvGjH/2I8ePHU1paiqryj3/84/D6wYMHc8EFF7B3716efPJJMjIyuOuuu7jmmmt47bXXGDt2LG3atKnxnB07duSOO+5g+PDh9O/fn9NPPz1eb88Yk2zLnoMZP/ESugS9rhnUS/INkJJzxo4aNUor16P/6quvOPHEE49sk4ThlXVx6623cvnll3PttdfG7JixUPlzNMakiLkPw8z7ve4ZCYDrgNb8F3+kU58qdJftdqocedNoat1UFsukbIwxSZOzHl67GXK/9lrx9eyeqUmjTfSpzu5sNcbU6kAWPD8eivK8i60N7KKpTqMpamaMMU1KST68PNFL8hKIW5IHa9EbY0zi5XwFz/yHd5drsAU4ZXE9nbXojTEm0T78BYTLvO4aJ7blXKpiid4YYxJp00zYMguQuHbXRLJEXwd79uxhwoQJHH/88Zx00klceumlR5UwiJSVlcWwYceU76+XMWPGUHm4KcD06dNjXirZGBNns/8S1wuvVWm8ffR/HQRFObE7XpvucM/GalerKldffTW33HIL06ZNA2DFihXs3buXE044IXZx1MGVV17JlVdemZRzG2PqwXVhz2q/jEHiNN4WfSyTfBTHmzVrFunp6dx555HKDyNHjuTcc8/lnnvuYdiwYQwfPpxXXnnlmH1LS0u57bbbGD58OKeccgqzZs0CvCGYV111FVdccQUDBgzgscce4+9//zunnHIKZ555Jvv3HykE+sILL3D22WczbNgwFi1adHj/yZMnA/Duu+9yxhlncMopp3DRRRexd+/eBn8kxpgYKj0IH993uKxwIjXeRJ9ga9as4bTTTjtm+ZtvvsmKFStYuXIlM2fO5J577mH37t1HbfP4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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "vs.plot(title='España vs Colombia',kind='area')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "933b1f23",
   "metadata": {},
   "source": [
    "## Triple comparativa España-Colombia-Argentina"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "868a44b5",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:title={'center':'Casos de Covid19 en Argentina'}, xlabel='Date'>"
      ]
     },
     "execution_count": 41,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "url_ag = 'https://api.covid19api.com/country/argentina/status/confirmed/live'\n",
    "df_ag = pd.read_json(url_ag)\n",
    "df_ag.set_index('Date')['Cases'].plot(title='Casos de Covid19 en Argentina')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "id": "7fa4fa2a",
   "metadata": {},
   "outputs": [],
   "source": [
    "casos_es = df_es.set_index('Date')['Cases']\n",
    "casos_co = df_co.set_index('Date')['Cases']\n",
    "casos_ag = df_ag.set_index('Date')['Cases']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "id": "4e5cd39e",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Cases</th>\n",
       "      <th>Cases</th>\n",
       "      <th>Cases</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>11451676.0</td>\n",
       "      <td>6083643.0</td>\n",
       "      <td>9026075</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>11451676.0</td>\n",
       "      <td>6083939.0</td>\n",
       "      <td>9028730</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>11508309.0</td>\n",
       "      <td>6084240.0</td>\n",
       "      <td>9032162</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>11508309.0</td>\n",
       "      <td>6084551.0</td>\n",
       "      <td>9035127</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-31 00:00:00+00:00</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>9035127</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>800 rows × 3 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                Cases      Cases    Cases\n",
       "Date                                                     \n",
       "2020-01-22 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-23 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-24 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-25 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-26 00:00:00+00:00         0.0        0.0        0\n",
       "...                               ...        ...      ...\n",
       "2022-03-27 00:00:00+00:00  11451676.0  6083643.0  9026075\n",
       "2022-03-28 00:00:00+00:00  11451676.0  6083939.0  9028730\n",
       "2022-03-29 00:00:00+00:00  11508309.0  6084240.0  9032162\n",
       "2022-03-30 00:00:00+00:00  11508309.0  6084551.0  9035127\n",
       "2022-03-31 00:00:00+00:00         NaN        NaN  9035127\n",
       "\n",
       "[800 rows x 3 columns]"
      ]
     },
     "execution_count": 43,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "pd.concat([casos_es,casos_co,casos_ag],axis=1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "id": "cddd06de",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Cases</th>\n",
       "      <th>Cases</th>\n",
       "      <th>Cases</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>11451676.0</td>\n",
       "      <td>6083643.0</td>\n",
       "      <td>9026075</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>11451676.0</td>\n",
       "      <td>6083939.0</td>\n",
       "      <td>9028730</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>11508309.0</td>\n",
       "      <td>6084240.0</td>\n",
       "      <td>9032162</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>11508309.0</td>\n",
       "      <td>6084551.0</td>\n",
       "      <td>9035127</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-31 00:00:00+00:00</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>9035127</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>800 rows × 3 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                                Cases      Cases    Cases\n",
       "Date                                                     \n",
       "2020-01-22 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-23 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-24 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-25 00:00:00+00:00         0.0        0.0        0\n",
       "2020-01-26 00:00:00+00:00         0.0        0.0        0\n",
       "...                               ...        ...      ...\n",
       "2022-03-27 00:00:00+00:00  11451676.0  6083643.0  9026075\n",
       "2022-03-28 00:00:00+00:00  11451676.0  6083939.0  9028730\n",
       "2022-03-29 00:00:00+00:00  11508309.0  6084240.0  9032162\n",
       "2022-03-30 00:00:00+00:00  11508309.0  6084551.0  9035127\n",
       "2022-03-31 00:00:00+00:00         NaN        NaN  9035127\n",
       "\n",
       "[800 rows x 3 columns]"
      ]
     },
     "execution_count": 44,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "vs2 = pd.concat([casos_es,casos_co,casos_ag],axis=1)\n",
    "vs2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "id": "f673408a",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>España</th>\n",
       "      <th>Colombia</th>\n",
       "      <th>Argentina</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>11451676.0</td>\n",
       "      <td>6083643.0</td>\n",
       "      <td>9026075</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>11451676.0</td>\n",
       "      <td>6083939.0</td>\n",
       "      <td>9028730</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>11508309.0</td>\n",
       "      <td>6084240.0</td>\n",
       "      <td>9032162</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>11508309.0</td>\n",
       "      <td>6084551.0</td>\n",
       "      <td>9035127</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-31 00:00:00+00:00</th>\n",
       "      <td>NaN</td>\n",
       "      <td>NaN</td>\n",
       "      <td>9035127</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>800 rows × 3 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                               España   Colombia  Argentina\n",
       "Date                                                       \n",
       "2020-01-22 00:00:00+00:00         0.0        0.0          0\n",
       "2020-01-23 00:00:00+00:00         0.0        0.0          0\n",
       "2020-01-24 00:00:00+00:00         0.0        0.0          0\n",
       "2020-01-25 00:00:00+00:00         0.0        0.0          0\n",
       "2020-01-26 00:00:00+00:00         0.0        0.0          0\n",
       "...                               ...        ...        ...\n",
       "2022-03-27 00:00:00+00:00  11451676.0  6083643.0    9026075\n",
       "2022-03-28 00:00:00+00:00  11451676.0  6083939.0    9028730\n",
       "2022-03-29 00:00:00+00:00  11508309.0  6084240.0    9032162\n",
       "2022-03-30 00:00:00+00:00  11508309.0  6084551.0    9035127\n",
       "2022-03-31 00:00:00+00:00         NaN        NaN    9035127\n",
       "\n",
       "[800 rows x 3 columns]"
      ]
     },
     "execution_count": 45,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "vs2.columns = ['España', 'Colombia', 'Argentina']\n",
    "vs2"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "id": "282bd625",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:title={'center':'España, Colombia y Argentina'}, xlabel='Date'>"
      ]
     },
     "execution_count": 46,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "vs2.plot(title='España, Colombia y Argentina')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "93c78597",
   "metadata": {},
   "source": [
    "## Seleccionar más columnas"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "id": "2f1db58f",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Cases</th>\n",
       "      <th>Lon</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>2020-01-22 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-23 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-24 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-25 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2020-01-26 00:00:00+00:00</th>\n",
       "      <td>0</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-26 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-27 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-28 00:00:00+00:00</th>\n",
       "      <td>11451676</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-29 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2022-03-30 00:00:00+00:00</th>\n",
       "      <td>11508309</td>\n",
       "      <td>-3.75</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>799 rows × 2 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "                              Cases   Lon\n",
       "Date                                     \n",
       "2020-01-22 00:00:00+00:00         0 -3.75\n",
       "2020-01-23 00:00:00+00:00         0 -3.75\n",
       "2020-01-24 00:00:00+00:00         0 -3.75\n",
       "2020-01-25 00:00:00+00:00         0 -3.75\n",
       "2020-01-26 00:00:00+00:00         0 -3.75\n",
       "...                             ...   ...\n",
       "2022-03-26 00:00:00+00:00  11451676 -3.75\n",
       "2022-03-27 00:00:00+00:00  11451676 -3.75\n",
       "2022-03-28 00:00:00+00:00  11451676 -3.75\n",
       "2022-03-29 00:00:00+00:00  11508309 -3.75\n",
       "2022-03-30 00:00:00+00:00  11508309 -3.75\n",
       "\n",
       "[799 rows x 2 columns]"
      ]
     },
     "execution_count": 47,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df_es.set_index('Date')[['Cases','Lon']]"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "80de62ba",
   "metadata": {},
   "source": [
    "## Exportar datos"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "id": "dd729b31",
   "metadata": {},
   "outputs": [],
   "source": [
    "vs.to_csv('vs.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "id": "4ffe0715",
   "metadata": {},
   "outputs": [],
   "source": [
    "vs2.to_csv('vs2.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "id": "5b9fc731",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "grafico =vs.plot()\n",
    "fig = grafico.get_figure()\n",
    "fig.savefig('vs.png')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "id": "92ec39f1",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "grafico =vs2.plot()\n",
    "fig = grafico.get_figure()\n",
    "fig.savefig('vs2.png')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "391fc1e2",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.8"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}```

