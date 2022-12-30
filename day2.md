# Day 2 

### Problem 1
***
* Create Dockerfile 
---
```
FROM ubuntu:23.04

RUN apt update -y
RUN apt install nginx -y 

ADD index.tar /var/www/html
COPY index.html /var/www/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```
***
### Problem 2 
---
* Create Dockerfile for single stage
---
```
FROM node:alpine 

WORKDIR /app

COPY package*.json ./

RUN npm install 

COPY  . .

CMD [ "npm" , "start" ]
```




