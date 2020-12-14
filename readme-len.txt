Mision TIC 2020
13-dic-2020
Ciclo 3
Fastapi

Se creo en python el siguiente codigo en el main.py para poder usar el fastAPI

from fastapi import FastAPI

app = FastAPI()

@app.get("/")
async def root():
  return {"message": "Hello FastAPI"}

Probar fastAPI desde los primeros pasos y se debe ejecutar el uvicorn que crea un servidor web
para dar respuesta a las pruebas que se realizaran en el localhost
el "app" en el código de python es el objeto que se instacio en el codigo de python para hacer uso de este servidor
el parametro reload indica que si detecta cambios en la configuración o archivos los recarga el mismo
en este caso el archivo que va estar pendeinte es el "main" con el objeto "app" que en el comando se ve "main:app"

estando dentro de la carpeta del proyecto y donde reside el main.py desde línea de comando se ejecuta:

C:\Users\ITSTKCOBO2300\Documents\cajero_api>uvicorn main:app --reload
←[32mINFO←[0m:     Uvicorn running on ←[1mhttp://127.0.0.1:8000←[0m (Press CTRL+C to quit)

al subir el uvicorn tomo el localhost y el puerto en donde va a contestar las peticiones desde el navegador "http://127.0.0.1:8000"

←[32mINFO←[0m:     Started reloader process [←[36m←[1m25316←[0m] using ←[36m←[1mstatreload←[0m
←[31mERROR←[0m:    Error loading ASGI app. Attribute "app" not found in module "main".

En este punto no se había actualizafo el main.py en python y cuando se guardo en VScode se da cuenta del cambio y ejecuta
de manera automática:

←[33mWARNING←[0m:  StatReload detected file change in 'main.py'. Reloading...
←[32mINFO←[0m:     Started server process [←[36m25160←[0m]
←[32mINFO←[0m:     Waiting for application startup.
←[32mINFO←[0m:     Application startup complete.
←[32mINFO←[0m:     127.0.0.1:58627 - "←[1mGET / HTTP/1.1←[0m" ←[32m200 OK←[0m


En este punto ya el uvicorn esta ejecutando como un servidor o listener http y ha instanciado lo de main.py y ha creado un objeto
app que esta atento a que cuando desde el navegar se ingrese a la raíz y venga un comando get debe retornar el mensaje "message": "Hello FastAPI"

Esto paso en el navegador en chrome con el mesnaje respectivo:

http://localhost:8000/
{"message":"Hello FastAPI"}

En firefox ademas de la respuesta habilito otras pestañas así:

En la pestaña cabecera se observa:
content-length: 27
content-type: application/json
date: Mon, 14 Dec 2020 02:02:17 GMT
server: uvicorn

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: es-ES,es;q=0.8,en-US;q=0.5,en;q=0.3
Connection: keep-alive
Host: localhost:8000
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:83.0) Gecko/20100101 Firefox/83.0

En la pestaña Datos sin procesar
{"message":"Hello FastAPI"}

En la pestaña JSON:
{"message":"Hello FastAPI"}


Cuando se quiere listar la base de datos que es un diccionario en memoria se obtine el resultado
{"message":{"camilo24":{"username":"camilo24","password":"root","balance":12000},"andres18":{"username":"andres18","password":"hola","balance":34000},"orlando61":{"username":"orlando61","password":"1959","balance":134000},"jacqueline62":{"username":"jacqueline62","password":"1962","balance":2234000},"sonia65":{"username":"sonia65","password":"1965","balance":3646000}}}
si se ve en formato json:
{"message":{"camilo24":{"username":"camilo24","password":"root","balance":12000},"andres18":{"username":"andres18","password":"hola","balance":34000},"orlando61":{"username":"orlando61","password":"1959","balance":134000},"jacqueline62":{"username":"jacqueline62","password":"1962","balance":2234000},"sonia65":{"username":"sonia65","password":"1965","balance":3646000}}} 
El código agregado en el main.py fue:
from db.user_db import database_users
@app.get("/users")
async def users():
  return {"message": database_users}
En el navegador la petición fue:
http://localhost:8000/users









************
************
************
************


Pruebas para crear un webserver local y accederlo con localhost

Se crea la carpeta, se accede a ella y se da el comando:

c:\...>python -m http.server

En el navegador se da localhost:8000 y muestra
Directory listing for /
Archivo de texto.txt
Contenido/
Imagen.JPG
readme-len.txt

el "/" es la carpeta que se creo webServer

al darle click en el navegador a la carpeta contenido:

Directory listing for /Contenido/

en la consola cmd del servidor http se puede ver los siguientes mensajes:


C:\Users\ITSTKCOBO2300\Documents\temp\webServer>python -m http.server
Serving HTTP on :: port 8000 (http://[::]:8000/) ...
::1 - - [13/Dec/2020 19:55:50] "GET / HTTP/1.1" 200 -
::1 - - [13/Dec/2020 19:59:40] "GET /Contenido/ HTTP/1.1" 200 -

lo que va entre comillas es la petición y luego sale el código resultado de la petición

al tratar de acceder a un archivo inexistente se genera el error en el navegador:

Error response
Error code: 404

Message: File not found.

Error code explanation: HTTPStatus.NOT_FOUND - Nothing matches the given URI.

en la consola donde se abrio el servidor estos fueron los mensajes:

C:\Users\ITSTKCOBO2300\Documents\temp\webServer>python -m http.server
Serving HTTP on :: port 8000 (http://[::]:8000/) ...
::1 - - [13/Dec/2020 19:55:50] "GET / HTTP/1.1" 200 -
::1 - - [13/Dec/2020 19:59:40] "GET /Contenido/ HTTP/1.1" 200 -
::1 - - [13/Dec/2020 20:03:21] "GET /Imagen.JPG HTTP/1.1" 200 -
::1 - - [13/Dec/2020 20:04:09] "GET /readme-len.txt HTTP/1.1" 200 -
::1 - - [13/Dec/2020 20:04:19] code 404, message File not found
::1 - - [13/Dec/2020 20:04:19] "GET /readme-len1.txt HTTP/1.1" 404 -

Keyboard interrupt received, exiting.

C:\Users\ITSTKCOBO2300\Documents\temp\webServer>




