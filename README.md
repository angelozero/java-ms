# microservice
## tecnologias utilizadas
- api rest
- java 20 
- spring boot
- postgre sql
- node js
- express js
- mongo db
- rabbit mq
- docker
- docker compose
- heroku
![arch](https://i.postimg.cc/fTwRWWCf/Screenshot-2023-06-08-at-22-18-39.png)

---

### 01 - Criando bases de dados e mensageria no Docker
#### - PostgreSQL - connection with [DBeaver Community](https://dbeaver.io/download/)
```shell
docker run --name auth-db -p 5432:5432 -e POSTGRES_DB=auth-db -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=terra postgres
```
```shell
docker run --name product-db -p 5433:5432 -e POSTGRES_DB=product-db -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=terra postgres
```

#### - MongoDB - connection with [MongoDB Compass](https://www.mongodb.com/try/download/shell)
```shell
docker run --name sales-db -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=terra mongo:4.4.6
```

#### - RabbitMQ - connection via your [Localhost Browser](http://localhost:15672/) (User: guest / Password: guest)
```shell
docker run --name sales-rabbit -p 5672:5672 -p 25676:25676 -p 15672:15672 rabbitmq:3.12-management
```

#### - Docker Compose - iniciando os 3 serviços ( PostgreSQL + MongoDB + RabbitMQ )
```yml
version: "3"
services:

    auth-db:
        image: postgres
        container_name: auth-db
        restart: always
        environment:
          - POSTGRES_DB=auth-db
          - POSTGRES_USER=admin
          - POSTGRES_PASSWORD=terra
        ports: 
          - 5442:5432

    product-db:
        image: postgres
        container_name: product-db
        restart: always
        environment:
          - POSTGRES_DB=auth-db
          - POSTGRES_USER=admin
          - POSTGRES_PASSWORD=terra
        ports: 
          - 5452:5432

    sales-db:
        image: mongo:4.4.6
        container_name: sales-db
        restart: always
        environment:
          - MONGO_INITDB_ROOT_USERNAME=admin
          - MONGO_INITDB_ROOT_PASSWORD=terra
        ports: 
          - 27017:27017
          - 28017:28017

    sales-rabbitmq:
        image: rabbitmq:3.12-management
        container_name: sales-rabbitmq
        ports:
          - 5672:5672
          - 25676:25676
          - 15672:15672
```
---
