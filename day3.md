# Day 3

### Problem 1
***
* Create docker-compose file 
```
version: '3'
services:
  gasser-service:
    container_name: react_app
    image: react_app_multistage:V1.3
    ports:
      - "3001:80"
      
```

### Problem 2 
---
* Create Dockerfile for python 
```
FROM python:latest

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD [ "python" ,"app.py"]
```
---
* Create Docker Compose 

```
version: '3'
services:
  flask-service:
    container_name: flask_app
    image: python_flask:V1.3
    ports:
      - "5000:5000"
    links:
      - redis
   

  redis:
    image: "redis:alpine"
```
* <span style="color:red">some **Warning!**</span>.
* <span style="color:red">it works only with the redis container ip not the localhost i dont know why 😮‍💨</span>.

