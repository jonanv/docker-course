# Docker

## Commands Docker
```docker
docker pull hello-word                      # Descargar imagen

docker container run hello-word             # Correr la imagen en un contenedor
docker run hello-word                       # Correr la imagen en un contenedor
docker run <image-name>                     # Correr la imagen en un contenedor
docker container --help                     # Muestra comandos de docker container
docker container ls                         # Muestra el listado de container corriendo
docker container ls -a                      # Muestra todos los contenedores
docker container ls -all                    # Muestra todos los contenedores
docker container ps                         # Muestra el listado de container corriendo forma antigua
docker container rm <container-id>          # Eliminar un contenedor por ID
docker container rm 606 504                 # Eliminar dos contenedores por ID con los 3 primeros numeros
docker container prune                      # Elimina TODOS los contenedores

docker images                               # Ver todas la imagenes
docker images -a                            # Ver todas la imagenes
docker images --all                         # Ver todas la imagenes
docker images --help                        # Ver ayudas de images
docker image --help                         # Ver ayudas de image
docker image ls                             # Ver todas la imagenes
docker image rm <container-id>              # Eliminar una imagen por ID
docker image rm <container-id> -f           # Eliminar una imagen por ID de manera forzada
docker image rm <container-id> --force      # Eliminar una imagen por ID de manera forzada
docker image rm 606 5f7                     # Eliminar dos imagenes por ID con los 3 primeros numeros
docker image prune                          # Elimina TODAS las imagenes
docker image prune -a                       # Elimina TODAS las imagenes no usadas

docker build -t getting-started .           # Construir y asignar un tag a la imagen 
                                            #   -t : Asigna el tag name 
                                            #   . : Indica a dónde buscar el archivo DockerFile

docker container run -d                         # Correr contenedor del modo desenlazado (detach)
docker container run --detach                   # Correr contenedor del modo desenlazado (detach)
docker container run -p 8080:80                 # Correr contenedor publicado en el puerto 8080 de mi equipo y lo expone en el 80 del contenedor (equipo:contenedor)
docker container run --publish 8080:80          # Correr contenedor publicado en el puerto 8080 de mi equipo y lo expone en el 80 del contenedor (equipo:contenedor)
docker container stop <cotainer-id>             # Detener contenedor por ID
docker container stop <cotainer-name>           # Detener contenedor por nombre
docker container start <cotainer-id>            # Iniciar contenedor por ID
docker container start <cotainer-name>          # Iniciar contenedor por nombre
docker container run --name <container-name>    # Asignar nombre al contenedor

docker container run --name some-postgres -dp 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres # Asginar variables de entorno (env)

docker container run \
--name some-postgres \
-dp 5432:5432 \
-e POSTGRES_PASSWORD=mysecretpassword \
postgres:14-alpine3.17                          # Asginar variables de entorno (env)

docker container logs <contaner-id>             # Muestra los logs de un contenedor
docker container logs --follow <contaner-id>    # Muestra los logs de un contenedor y seguir nuevos logs

docker stats                                    # Muestra estadisticas del consumo de memoria

docker image tag SOURCE[:TAG] TARGET_IMAGE[:TAG]    # Renombrar una imagen local
docker tag IMAGE NEW_IMAGE                          # Renombrar una imagen local
docker tag <Tag Actual> <USUARIO>/<NUEVO NOMBRE>    # Renombrar una imagen local
```

# Docker -it (interactive terminal)
```docker
docker exec -it CONTAINER EXECUTABLE                # Iniciar un comando shell dentro del contenedor (interactive terminal)
docker exec -it <NAME o ID> bash                    # Iniciar un comando shell dentro del contenedor (interactive terminal)
docker exec -it <NAME o ID> /bin/sh                 # Iniciar un comando shell dentro del contenedor (interactive terminal)
```

# Docker volume
```docker
# Hay 3 tipos de volumenes

## Named Volumes
### Este es el volumen más usado.
docker volume create <volume-name>                # Crear un nuevo volumen
docker volume ls                                  # Listar los volumenes
docker volume inspect <volume-name>               # Inspeccionar el volumen específico
docker volume prune                               # Remueve todos los volúmenes no usados
docker volume rm <volume-name>                    # Remueve uno o más volúmenes especificados
docker run -v todo-db:/etc/todos getting-started  # Usar un volumen al correr un contenedor

## Bind volumes - Vincular volúmenes
### Bind volumes trabaja con paths absolutos
docker run \
-dp 3000:3000 \
-w /app \
-v "$(pwd):/app" \
node:18-alpine \
sh -c "yarn install && yarn run dev"

# -w /app: Working directory: donde el comando empezará a correr.
# -v “$(pwd):/app”: Volumen vinculado: vinculamos el directorio del host con el directorio /app del contenedor
# node:18-alpine: Imagen a usar 
# sh -c "yarn install && yarn run dev": Comando Shell: Iniciamos un shell y ejecutamos yarn install y luego correr el yarn run dev

## Anonymous Volumes
### Volúmenes donde sólo se especifica el path del contenedor y Docker lo asigna automáticamente en el host
docker run -v /var/lib/mysql/data
```

# Docker network
```docker
# Regla de oro:
## Si dos o más contenedores están en la misma red, podrán hablar entre sí. Si no lo están, no podrán.

docker network                                      # Ver comandos de network
docker network create <todo-app>                    # Crear una nueva red
docker network ls                                   # Listar todas la redes creadas
docker network inspect <NAME o ID>                  # Inspeccionar una red
docker network prune                                # Borrar todas las redes no usadas
docker network connect --help                       # Opciones de network connect
docker network connect <todo-app> <container-id>    # Conectar un contenedor con id a una red (todo-app)
docker network connect todo-app 6lp                 # Conectar un contenedor con id a una red (todo-app)

# Correr una imagen y unirla a la red
docker run -d \
--network todo-app --network-alias mysql \
-v todo-mysql-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=secret \
-e MYSQL_DATABASE=todos \
mysql:8.0

# -e: Variable de entorno: MySQL necesita definir el root password y el nombre de la base de datos.
# -v todo-mysql-data:/var/lib/mysql: Volumen con nombre hacia donde MySQL graba la base de datos.
# --network-alias: Crea un nombre nuestra aplicación solo necesita conectarse a un host llamado mysql y se comunicará con la base de datos.

# Puertos y Paths
# Cuando vean cosas como: -p 6000:6379
# Recuerden que es
# HOST : CONTAINER
```


# Examples Docker container
```docker
# postgres
docker container run \
--name some-postgres \
-dp 5432:5432 \
-e POSTGRES_PASSWORD=mysecretpassword \
postgres:14-alpine3.17

# maridb
docker container run \
--name world-db \
-dp 3307:3306 \
--env MARIADB_USER=example-user \
--env MARIADB_PASSWORD=user-password \
--env MARIADB_ROOT_PASSWORD=root-secret-password \
--env MARIADB_DATABASE=world-db \
mariadb:jammy

# maridb con volume y network 
docker container run \
--name world-db \
-dp 3307:3306 \
--env MARIADB_USER=example-user \
--env MARIADB_PASSWORD=user-password \
--env MARIADB_ROOT_PASSWORD=root-secret-password \
--env MARIADB_DATABASE=world-db \
--volume world-db:/var/lib/mysql \
--network world-app \
mariadb:jammy

# phpmyadmin con network
docker container run \
--name phpmyadmin \
-d \
--env PMA_ARBITRARY=1 \
-p 8070:80 \
--network world-app \
phpmyadmin:5.2.0-apache

# nest-app con bind volume
docker container run \
--name nest-app \
-w /app \
-dp 80:3000 \
-v %cd%:/app 
node:16-alpine3.16 \
sh -c "yarn install && start:dev"

# Laboratorio postgres y pgadmin
docker container run \
-d \
--name postgres-db \
--env POSTGRES_PASSWORD=123456 \
-v postgres-db:/var/lib/postgresql/data \
postgres:15.1

docker container run \
--name pgAdmin \
--env PGADMIN_DEFAULT_PASSWORD=123456 \
--env PGADMIN_DEFAULT_EMAIL=superman@google.com \
-dp 8080:80 
dpage/pgadmin4:6.17
```

# Docker compose docker-compose.yml
Docker Compose es una herramienta que se desarrolló para ayudar a definir y compartir aplicaciones de varios contenedores. Ejemplo: de docker-compose.yml

```docker
# Versión a usar en el docker-compose
version: '3'

services:
    # Nombre del servicio
    anylistapp:
        # Depende de otro servicio
        depends_on:
            - db

        # Construcción de imagen
        build:
            # Path del dockerfile (./path/)
            context: .
            dockerfile: Dockerfile
        
        # Nombre del a imagen a usar
        image: node:18-alpine

        # Ejecutar un comando shell dentro
        command: sh -c "yarn install && yarn run dev"

        # Directorio a de trabajo dentro del contenedor
        working_dir: /app

        # Nombre del contenedor
        container_name: AnylistApp

        # Reiniciar el contenedor si se detiene
        restart: always

        # Puertos: MI_EQUIPO : CONTENEDOR
        ports:
            - 8080:3000
```

docker-compose.yml del laboratorio postgres y pgadmin
```docker
version: '3'

services:
  db:
    container_name: postgres_database
    image: postgres:15.1
    volumes:
      - postgres-db:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=123456

  pgAdmin:
    depends_on:
      - db
    image: dpage/pgadmin4:6.17
    ports:
      - "8080:80"
    environment:
      - PGADMIN_DEFAULT_PASSWORD=123456 
      - PGADMIN_DEFAULT_EMAIL=superman@google.com 

volumes:
  postgres-db:
    external: true
```

## Docker composer commands
```docker
docker compose up -d            # Levantar y ejecutar el comando
docker compose logs -f          # Revisar logs de los contenedores levantados con el compose
docker compose down             # Limpiar todo, los contenedores se detendrán y la red se removerá
```
## Nomenclatura docker compose
Nomenclatura de los contenedores usados en el docker compose
```docker
<project-name>_<service-name>_<replica-number>

Ejemplo:
posgres-pgadmin_pgAdmin_1
```

## Best Practices
Escaneo de imagen
Después de construir una imagen, es buena práctica
realizar un scan en ella para buscar vulnerabilidades.
```docker
docker scan getting-started
docker scan getting-started:1.0.0
```

# Docker build
```docker

```

# KUBERNETS
```docker

```