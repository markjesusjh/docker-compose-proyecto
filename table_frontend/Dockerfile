#choose the proper node image.... https://
FROM node:18-alpine as build_image
WORKDIR /app/react-app

#copy package.json
COPY package.json .

#install all our packages
RUN npm install

#copy all our remaining files
COPY . . 

#finally build our project
RUN npm run build 

FROM node:18-alpine as PRODUCTION_IMAGE
WORKDIR /app/react-app

#here, we are copying 
COPY --from=BUILD_IMAGE /app/react-app/dist/ /app/react-app/dist/
EXPOSE 8000

COPY package.json .
COPY vite.config.ts .
RUN npm install typescript
EXPOSE 8000
CMD ["npm", "run", "preview"]

#i love cloud computing ;)