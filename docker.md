# Docker

**Ejemplo de uso**<br>
Para este ejemplo vamos a instalar un servidor web de nginx
`sudo docker run nginx:1.17-alpine`, lo que estamos haciendo es pedirle una version especifica de nginx, y como no tenemos la imagen en nuestra maquina lo que va hacer es descargarla

podemos cerrar el sevidor con "ctrl+c"

y si queremos volver a ejecutarlo pero en un puerto diferente, lo hacemos de la siguiente manera `sudo docker run -p 80:80 nginx:1.17-alpine`.

>Dockerhub: este el el registry(repositorio), donde se encuentran todas las imagenes de docker disponibles.

>Nota: al ejecutar los procesos de docker recuerda que los puertos deben ser mayor al 1024, por que estos estan recervados para el propio sistema de la pc

## Comandos Docker
|Comando|Descripcion|
|-|-|
|**docker** _image ls_| nos muestra una **lista** de las imagenes que tenemos descargados en nuestra maquina local.|
|**docker** _pull nombreImagen:version_|nos permite **descargar** una imagen de algun _registry_(repositorio de docker), si no le especificamos la version docker descarlara la mas reciente.|
|**docker** _rmi nombreImagen_|elimina las imagenes de tu pc local|
|**docker** _run nombreImagen_ | nos permite correr la imagen que seleccionemos, si no esta descargada en nuestro pc doker lo descargara automaticamente|
|**docker** _run **-d** nombreImagen_| le indicamos que corra el proceso en segundo plano, o en un proceso aparte.|
|**docker** _ps_| nos permite visualizar los procesos o imagenes que se estan ejecutando.|
|**docker** _run **--name** nombreProceso nombreImagen_| este sera un nombre que nos permitira identificar el proceso, sino lo especificamos docker le asignara cualquiera|
|**docker** _logs nomberProceso_| nos permite visualizar los mensajes (logs) que deberia mostrarnos al momento de ejecutar la imagen|
|**docker** _top nombreProceso_| nos permite visualizar los procesos que se estan ejecutando de manera interna en el contenedor|
|**docker** _stop nombreProceso_|detiene el proceso o la imagen que se esta ejecutando, tambien es posible pasarle el **ID** del proceso en lugar del nombre que configuramos; El hecho que detengamos el proceso no quiere decir que el proceso ya no exista.|
|**docker** _ps **-a**_|nos muestra todos los procesos activos asi como los procesos detenidos|
|**dcoker** _rm nombreProceso_|este comando si elimana el procesos que le indiquemos |
|**docker** _run **--rm** nombreImagen_| con esta etiqueta, le indica al proceso que cuando lo detengamos se elimine automaticamente|
|**docker** _run -p puertoPC:puertoContenedor_|permite que enlacemos un puerto de nuestro pc con el puerto de nuestro contenedor|
|**docker** _exec nombreProceso comando_|nos permite hacer ejecucion de comandos (comandos linux por o general) dentro de nuestro contenedor|
|**docker** _exec **-it** nombreProceso bash_|mantiene una sesion interactiva con la terminal y el contenedor de docker|
|**docker** _run **-v rutaDirPc:rutaDirDocker** nombreImagen_| esto enlaza un volumen de memoria de docker con un volumen de memoria de nuestra maquina local|
|**docker** _network ls_| lista las redes que tengo intalado en mi maquina local|


## Construcion de Imagenes

Para empezar debemos crear el archivo `Dockerfile`

|Comando|Descripcion|
|-|-|
|FROM _nombreImagen_|sirve para desarrollar nuestra imagen, pero que se va basar en otra imagen de docker -> va dentro del Dockerfile|
|RUN|nos permite correr comandos dentro de las imagenes, estos comandos van a ser propios de la instalacion-> va dentro del Dockerfile|
|CMD|este tambien nos permite ejecutar comandos, pero son comandos para la ejecucion del contenedor|
|EXPOSE _puerto_|permite exponer los puertos|
|WORKDIR _rutaDirectorio_|permite establecer un directorio de trabajo, aqui se van a ejecutar todos lo camandos de docker y los archivos con lo que quiera interactuar|
|ADD _archivoCopiar rutaDeCopiado_|copia archivos de nuestra pc local a nuestro contenedor, esta atmbien te permite copiar archivos desde una **url** o servidores remotos, tambien permite copiar archivos comprimidos|
|COPY _archivoCopiar rutaDeCopiado_|**solo** copia archivos de nuestra pc local a nuestro contenedor|
|ENV _NOMBREVAR=valor_|permie configurar variables de entorno|
|-|-|
|**docker** _build_| permite crear imagnes a partir del docker file|
|**docker**_build **-t** nombreTag:version rutaDir_|esto nos permite darle un nombre y una version a nuestra imagen|

## Docker Compose

El docker compose sirve para ejecutar multiples servicios con un unico comando atravez del archivo `docker-compose.yml`.

Esto puede entenderse como una alternativa al `docker run`

```yml
version:"3" #especifica la version del docker-compose  

services: #permite crear contenedores y conectarlos entre si
  web: #indica el nombre del servicio (puede ser cualquiera)
    build: . #especifica la ruta del Dockerdile
    image: 'hola-docker:1.3' #indicamos el nombre de la imagen
    ports: #expone los puertos del contenedor a la pc
      - "5000:5000"
    enviorment: #configura las variables entorno
      MSG: 'saludo a todos' 
```
Para levantar nuestro servicio podemos usar el comando `docker-compose up` en la ruta donde se encuentra nuestro `docker-compose.yml`

si lo que queremos es que se ejecute en **segundo plano**, le pasamos lo siguiente `docker-compose up -d`

para detener el servicio podemos usar `docker-compose down`

si se han realizado cambios en nuestro **Dockerfile** podemos usar el comando `docker-compose up -d --build` para que vuelva a construir la imagen antes que se ejecuten los servicios.

### Agregamos un nuevo servicio
```yml
version:"3"

services:
  web:
    ...
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: example

```
>Nota: dcoker-comopose suele configurarnos una red por defecto para que se comuniquen los servicios de neustros contenedores

### Variables de entorno
Para poder pasarle variables de entorno a nuestro archivo `.yml`, primero creamos el archivo `.env`, dentro digitamos las variables y para pasarselo a nuestro `docker-compose` usamola siguiente convencion `${NOMBRE_VARIABLE}` 

```yml
    ...
  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: ${DB_PASS}

```
### Volumenes
```yml
version:"3"  

services: 
  web: 
    ...
    volumes:
      - .:/app   #/dirPcLocal:/dirContenedor 
  db:
    ...
    volumes:
      - data:/var/lib/postgresql/data 

volumes: #creamos un volumen de memoria en nuestro contenedor 
  data:
    driver: local
  
```