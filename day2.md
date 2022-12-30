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
React app image single stage: 683mb,
React app image Multi stage: 41mb

----
### Problem 3 
- ipvlan: IPvlan networks give users total control over both IPv4 and IPv6 addressing. The VLAN driver builds on top of that in giving operators complete control of layer 2 VLAN tagging and even IPvlan L3 routing for users interested in underlay network integration. 

- macvlan: Macvlan networks allow you to assign a MAC address to a container, making it appear as a physical device on your network. The Docker daemon routes traffic to containers by their MAC addresses. Using the macvlan driver is sometimes the best choice when dealing with legacy applications that expect to be directly connected to the physical network, rather than routed through the Docker host’s network stack.

- network plugins: You can install and use third-party network plugins with Docker. These plugins are available from Docker Hub or from third-party vendors.

