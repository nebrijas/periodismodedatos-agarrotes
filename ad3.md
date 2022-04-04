# Actividad Dirigida 3
En esta actividad dirigida haremos uso de la [API de Covid-19](https://covid19api.com/#subscribe "API Covid") creada por Kyle Redelinghuys, a través de la cual se puede consultar información en tiempo real de la evolución de la pandemia COVID-19.

Los pasos que se seguirán en este código serán los siguientes:
1. Instalación de la librería pandas y configuración
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

## Instalación de la librería pandas y configuración
Lo primero que debemos hacer es instalar la librería [pandas](https://pandas.pydata.org "pandas") que se trata de una herramienta de análisis y manipulación de datos en código abierto construida sobre el lenguaje de programación Python. Para ello, haremos uso de la orden ```!pip install pandas```, ya que el ```pip``` es un gestor de paquetes estándar para este lenguaje que permite que se instalen y gestionen paquetes que no forman parte de la biblioteca estándar de Python.

Tras este primer paso, lo siguiente será configurar e introducir la librería de pandas en este código y darle a pandas el alias de pd a través de la orden ```import pandas as pd```.

## Variables
En este segundo paso, lo primero que debemos hacer es definir la [URL](https://api.covid19api.com/countries "URL") en la que queremos hacer web scraping y obtener los datos. En este caso utilizaremos la orden ```url = 'https://api.covid19api.com/countries'``` para racabar la lista de países en los que se muestra la evolución en tiempo real de la pandemia.

## Creación de *Dataframe*


