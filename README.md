### Instrucciones para poder compilar y desplegar la aplicacion tanto en local como en la nube (AWS)


## Compilar de forma local 
1. Docker-compose build (construye las imagenes)
2. Docker-compose up (levanta los contenedores)
3. Se puede chequear directamente desde las urls pertinentes para poder ver tanto el backend como el frontend.
- Antes de gestionar estos pasos realizar la copia del repositorio correspodiente o descargarlo en zip.


## Desplegar en AWS Elastic Beanstalk:

1. Empaquetar la aplicacion:
- Crea un archivo ZIP que contenga:
Dockerfile
docker-compose.yml
Carpeta app/ (con el codigo)

2. Crear un entorno Elastic Beanstalk
- En la consola de AWS, ve a Elastic
- Crea un nuevo entorno
- Selecciona "Aplicacion web" y la plataforma "Docker"

3. Subir el ZIP: 
- Sube el archivo ZIP que se creo anteriormente
- Elastic Beanstalk se encagará de construir y desplegar la aplicación. 


# Consideracion adicional

- Se puede personalizar la configuracion del entorno en la consola de AWS.
- Para configuraciones mas avanzadas se utilizan archivos .ebextensions
- Al igual que tambien se puede gestionar un archivo Dockerrun.aws.json, este archivo depende del tipo de plataforma y configuracion que se utilice en Beanstalk.

# Breve explicacion del archvo Dockerrun.aws.json

- Si se usa Docker compose: NO se necesita el archivo. Elastic puede leer directamente la configuracion de la aplicacion desde el archivo docker-compose.yml por ende no seria necesario el archivo aws.json
- En el caso de que no se utilice Docker compose si se necesita el archivo Dockerrun.aws.json para definir como se debe ejecutar el contenedor Docker.

* En resumen y segun mi experiencia y conocimientos se debe priorizar Docker compose, si es posible utilizar docker compose para poder definir la aplicacion, esto simplifica mucho el trabajo asi como tambien ayuda a evitar le uso del archivo Dockerrun, en el caso de ser necesario, utilizar Dockerrun para configuraciones especificas de Elastic Beanstalk.


# Ejemplo de Dockerrun.aws.json 

{
    "AWSEBDockerrunVersion": 2,
    "containerDefinitions": [
        {
            "name": "web",
            "image": "docker-image-name",
            "essential": true,
            "portMappings": [
                {
                    "hostPort": 80,
                    "containerPort": 8000
                }
            ]
        }
    ]
}