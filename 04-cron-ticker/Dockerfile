# Dependencias de desarrollo
FROM node:19.2-alpine3.16 as dependencies
WORKDIR /app
COPY package.json ./
RUN npm install

# Build y Tests
FROM node:19.2-alpine3.16 as builder
WORKDIR /app
COPY --from=dependencies /app/node_modules ./node_modules
COPY . .
RUN npm run test

# Dependencias de producción
FROM node:19.2-alpine3.16 as prod-dependencies
WORKDIR /app
COPY package.json ./
RUN npm install --prod

# Ejecutar la APP
FROM node:19.2-alpine3.16 as runner
WORKDIR /app
COPY --from=prod-dependencies /app/node_modules ./node_modules
COPY app.js ./
COPY tasks/ ./tasks
CMD ["node", "app.js"]