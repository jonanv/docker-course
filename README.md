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

docker container run -d                         # Correr contenedor del modo desenlazado (detach)
docker container run --detach                   # Correr contenedor del modo desenlazado (detach)
docker container run -p 8080:80                 # Correr contenedor publicado en el puerto 8080 de mi equipo y lo expone en el 80 del contenedor (equipo:contenedor)
docker container run --publish 8080:80          # Correr contenedor publicado en el puerto 8080 de mi equipo y lo expone en el 80 del contenedor (equipo:contenedor)
docker container stop <cotainer-id>             # Detener contenedor por ID
docker container stop <cotainer-name>           # Detener contenedor por nombre
docker container start <cotainer-id>            # Iniciar contenedor por ID
docker container start <cotainer-name>          # Iniciar contenedor por nombre
docker container run --name <container-name>    # Asignar nombre al contenedor

docker container run --name some-postgres -dp 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres # Asginar variables de entorno (env list)

docker container run \
--name some-postgres \
-dp 5432:5432 \
-e POSTGRES_PASSWORD=mysecretpassword \
postgres:14-alpine3.17                          # Asginar variables de entorno (env list)

docker container logs <contaner-id>             # Muestra los logs de un contenedor
docker container logs --follow <contaner-id>    # Muestra los logs de un contenedor y seguir nuevos logs

docker stats                                    # Muestra estadisticas del consumo de memoria

docker image tag SOURCE[:TAG] TARGET_IMAGE[:TAG]    # Renombrar una imagen local
docker tag IMAGE NEW_IMAGE                          # Renombrar una imagen local
docker tag <Tag Actual> <USUARIO>/<NUEVO NOMBRE>    # Renombrar una imagen local

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



```