# Actividad dirigida 2

En esta actividad dirigida importaremos de la edición digital del diario español [El País](https://elpais.com/ "El País") la tabla de [El medallero de Tokio 2020](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/ "Tabla Tokio 2020")

Los pasos que se seguirán en este código serán los siguientes:
1. Importar librerías
2. Variables
3. Hacemos la pregunta
4. Bucle para obtener los datos

## Importar librerías

En primer lugar haremos uso de la librería [requests](https://docs.python-requests.org/en/latest/ "requests") para bajarnos la página web desde la que queremos obtener y descargar los datos. Tras ello, importaremos la segunda librería llamada [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/ "bs4") con el objetivo de analizar los datos que ya nos hemos descargado en el paso previo.

## Variables

### Definimos URL y realizamos la petición a la web

En este paso, lo primero que debemos hacer es definir la [URL](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/ "Tabla Tokio 2020") en la que queremos hacer web scraping y obtener los datos. Después, a través de la orden ```req = requests.get(URL)``` realizamos la petición a la web, en caso de que la página no pueda ser leída, es decir, que sea ```req.status_code != 200``` el código imprimirá "No se puede hacer Web Scraping en [URL](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/ "URL"). En cambio, si conseguimos obtener los datos de esta página, es decir, siempre y cuando sea ```req.status_code == 200```, el código imprimirá "Vamos a por ello".

### De requests a BeutifulSoup

Tras el paso anterior, lo siguiente será pasar el contenido HTML de la web a un objeto [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/ "bs4") a través de la orden ```html = BeautifulSoup(req.text, "html.parser")```. Esto quiere decir, que Beautiful Soup es una librería Python que permite extraer información de contenido en [formato HTML o XML](https://j2logo.com/python/web-scraping-con-python-guia-inicio-beautifulsoup/ "Web scraping con Python")

### Variables de datos

En este apartado, lo que hacemos es definir las variables paises, oros, platas, bronces y totales; y después las identificamos con la función ```find_all()``` que sirve para obtener todas las etiquetas que cumplan con las condiciones del objeto HTML y después, tras obtenerlas, esta función se encarga de devolverlas.

## Hacemos la pregunta

En este siguiente paso, realizamos la siguiente pregunta a quién este haciendo uso del código:"¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?". En el caso de que la persona pulse la tecla s, entonces significará que sí quiere conocer estos datos, por lo que el código imprimirá "De acuerdo".

## Bucle para obtener los datos

Finalmente, con el objetivo de obtener los datos, realizaremos un bucle for, es decir, repetiremos el bloque de instrucciones un total de 20 veces, ya que estas iteraciones han sido determinadas previamente a través de la orden ```for i in range (20):```. En este caso, una vez se haya realizado el bucle, el código imprimirá ```%d``` que hace referencia a los números del ranking y la ```%s``` que se utiliza para dar formato a las cadenas de texto. Ambos valores se asocian a través de una tupla utilizando el operador %. Además, la orden ```[i+1]``` se utiliza para que el bucle vaya corriendo y no se quede estancado en ningún valor hasta que bucle finalice y se rompa. 


```
from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:
  print('Qué lástima, y...')
```
