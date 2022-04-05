# Actividad dirigida 2

En esta actividad dirigida hemos realizado unos ejercicios colectivos de Web Scraping sobre la tabla de [El medallero de Tokio 2020](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/ "Tabla Tokio 2020") de la edición digital del diario español [El País](https://elpais.com/ "El País").

Para obtener toda la información hemos usado el siguiente código que aparece debajo y hemos llevado a cabo una serie de pasos que están explicados en el notebook [scraping.ipynb](https://github.com/nebrijas/periodismodedatos-agarrotes/blob/main/scraping.ipynb "scraping.ipynb")


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
