# Day 2 

### Problem 1
***
* Create Dockerfile 
```
FROM ubuntu:23.04

RUN apt update -y
RUN apt install nginx -y 

ADD index.tar /var/www/html
COPY index.html /var/www/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### Problem 2 
---
* Create Dockerfile for single stage
```
FROM node:alpine 

WORKDIR /app

COPY package*.json ./

RUN npm install 

COPY  . .

CMD [ "npm" , "start" ]
```
=

* Create Dockerfile for Multi stage

```
FROM node:alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm install 

COPY  . .

RUN npm run build 

FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html 

EXPOSE 80

CMD ["nginx", "-g" , "deamon off"]
```
```
docker build -t react_app_multistage:V1 .
docker run -d --name gasser_react_multistage3 -p 80:80 react_app_multistage:V1 
```
React app image single stage: 683mb
React app image Multi stage: 41mb
