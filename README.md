# Api & Pipeline


url aplicacion :  

# INSTALACION [HEROKU-SERVIDOR][CON DOCKER]
debe tener una cuenta creada en heroku y descargar el cliente de heroku luego:
    heroku login
    heroku container:login
    heroku create nombre_app  #o el nombre que desee
    heroku container:push web -a  nombre_app
    heroku container:release web -a  nombre_app  #esto despliega


# INSTALACION [LINUX-MACOS][CON DOCKER][LOCALMENTE]
1: tener instalado docker-compose

clonar el proyecto y en la carpeta ejecutar
> docker-compose up

Este comando creara contenedores donde encontraremos 3 servicios : El Api principal, Un Manager de works y un worker, 
los cuales son necesarios para desarrollar el pipeline completo 


# INSTALACION [LINUX][SIN DOCKER][LOCALMENTE]
requisitos:
1: tener instalado python 3
2: tener instalada la libreria para creacion de entornos virtuales en python3 en caso de no tenerla ejecutar sudo apt-get install python3-venv
clonar el proyecto en su repositorio local y desplazarse hasta ese directorio , posteriormente crear un entorno virtual para instalar las dependencias 

> python3 -m venv venv

luego debera activar el entorno virtual anteriormente creado

> . venv/bin/activate  o bien usando el comando   source venv/bin/activate


una vez activado el entorno virtual debera instalar las dependencias por lo que en la raiz del proyecto ejecutar el siguiente comando

> pip install -r requirements.txt o bien  el comando   pip3 install -r requirements.txt


una vez instaladas las dependencias correr el script main.py  

> python /pipeline_challenge/main.py
> python /job_manager/manager.py
> python /job_worker/job_worker.py

una vez ejecutado cualquier de los metodos, ya sea con docker o con python directamente, tendremos expuestas 4 url para 
realizar las pruebas : 

> http://0.0.0.0:8000/docs#/ -- Url de la API principal
> http://0.0.0.0:8220/docs#/ -- Url del Easyjobs , manejador de workers
> http://0.0.0.0:8221/docs -- Url del work ( esta vista no muestra nada, su trabajo lo recibe el manejador)
> http://0.0.0.0:8000/graphql -- Url de GraphQL para probar consultas



# TESTS [LINUX][SIN DOCKER][LOCALMENTE]

una vez instalada las dependencias y el entorno virtual si realizo la instalacion
sin docker ejecutar en la raiz del proyecto el siguiente comando

> coverage run -m pytest /pipeline_challenge/tests


# TESTS [LINUX][CON DOCKER][LOCALMENTE]

si tiene el container corriendo (si siguio la guia para instalarlo localmente con docker)
entonces podra entrar al contenedor con el siguiente comando

para ver los containers activos corriendo
> docker ps 

de este resultado tome el id del container y ejecute 
> docker exec -ti id_container[pipeline_challenge] bash

una vez aqui podra ejecutar el comando de tests 

> coverage run -m pytest tests


en caso de tener el puerto ocupado ejecutar:
sudo lsof -t -i tcp:8000 | xargs kill -9


ejecutar GRAPHQL
> ruta http://localhost:8000/graphql 
        query{
            allDelegaciones{
              id
              delegacion
            }
        }


URLS desplegadas en HEROKU

https://api-challenge-pipeline.herokuapp.com/docs
https://manager-pipeline-challenge.herokuapp.com/docs
https://api-challenge-pipeline.herokuapp.com/graphql
