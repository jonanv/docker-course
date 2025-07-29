# Docker

## Commands Docker
```docker
docker pull hello-word                 # Descargar imagen

docker container run hello-word        # Correr la imagen en un contenedor
docker run hello-word                  # Correr la imagen en un contenedor
docker container --help                # Muestra comandos de docker container
docker container ls                    # Muestra el listado de container corriendo
docker container ls -a                 # Muestra todos los contenedores
docker container ls -all               # Muestra todos los contenedores
docker container ps                    # Muestra el listado de container corriendo forma antigua
docker container rm <container-id>     # Eliminar un contenedor por ID
docker container rm 606 504            # Eliminar dos contenedores por ID con los 3 primeros numeros
docker container prune                 # Elimina TODOS los contenedores

docker images                          # Ver todas la imagenes
docker images -a                       # Ver todas la imagenes
docker images --all                    # Ver todas la imagenes
docker images --help                   # Ver ayudas de images
docker image --help                    # Ver ayudas de image
docker image ls                        # Ver todas la imagenes
docker image rm <container-id>         # Eliminar una imagen por ID
docker image rm 606 504                # Eliminar dos imagenes por ID con los 3 primeros numeros
docker image prune                     # Elimina TODAS las imagenes



```