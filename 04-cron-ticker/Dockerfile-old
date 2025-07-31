# /app /usr /lib
FROM node:19.2-alpine3.16
# FROM --platform=linux/amd64 node:19.2-alpine3.16
# FROM --platform=$BUILDPLATFORM node:19.2-alpine3.16

# cd app
WORKDIR /app

# Dest /app
COPY ["package.json", "./"]

# Instalar dependencias
RUN npm install

# Dest /app
COPY ["app.js", "./"]

# Dest /tests
COPY [".", "./"]

# Realizar testing
RUN npm run test

# Eliminar archivos y directorios no necesarios en PRODUCCION
# RUN rm -rf tests
# RUN rm -rf node_modules
RUN rm -rf tests && rm -rf node_modules

# Unicamente las dependencias de PRODUCCION
RUN npm install --prod

# Comando run de la imagen
CMD ["node", "app.js"]