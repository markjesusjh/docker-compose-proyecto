# Utilizar una imagen específica de Node que incluya npm y otras herramientas necesarias
FROM node:14 AS build

# Definir el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar únicamente los archivos de descripción de paquetes (package.json y package-lock.json)
COPY package*.json ./

# Instalar las dependencias
RUN npm install

# Copiar el resto de los archivos del proyecto
COPY . .

# Construir la aplicación
RUN npm run build

# Etapa de producción
FROM node:14 AS production

# Definir el directorio de trabajo
WORKDIR /app

# Copiar los archivos de construcción de la etapa de construcción
COPY --from=build /app/build ./build

# Instalar solo las dependencias de producción
RUN npm install --only=production

# Exponer el puerto en el que se ejecutará la aplicación
EXPOSE 8000

# Comando para iniciar la aplicación en modo producción
CMD ["npm", "start"]
