# Etapa 1: Construcción de la aplicación
FROM node:14 AS build

# Crear y definir el directorio de trabajo
WORKDIR /app

# Copiar el package.json y el package-lock.json (si existe)
COPY package*.json ./

# Instalar las dependencias
RUN npm install

# Copiar el resto del código de la aplicación
COPY . .

# Construir la aplicación
RUN npm run build

# Etapa 2: Servir la aplicación con nginx
FROM nginx:alpine

# Eliminar archivos por defecto de nginx
RUN rm -rf /usr/share/nginx/html/*

# Copiar los archivos construidos de la etapa anterior a la carpeta de nginx
COPY --from=build /app/dist /usr/share/nginx/html

# Exponer el puerto 8000
EXPOSE 8000

# Comando para iniciar nginx
CMD ["nginx", "-g", "daemon off;"]
