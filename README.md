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

```