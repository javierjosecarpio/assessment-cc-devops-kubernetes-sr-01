# Etapa 1: Construir la aplicación React
FROM node:15-alpine as build

# Instalar Python y herramientas de construcción
RUN apk add --no-cache python3 make g++

WORKDIR /app

# Copiar package.json y package-lock.json
COPY package.json ./
COPY package-lock.json ./

# Instalar dependencias
RUN npm install

# Copiar el resto del código fuente de la aplicación
COPY . .

# Construir la aplicación
RUN npm run build

# Etapa 2: Servir la aplicación usando Nginx
FROM nginx:stable-alpine

# Copiar los archivos estáticos construidos desde la etapa de construcción
COPY --from=build /app/build /usr/share/nginx/html

# Exponer el puerto 80
EXPOSE 80

# Iniciar Nginx
CMD ["nginx", "-g", "daemon off;"]
