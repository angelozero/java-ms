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

### 01 - Criando as bases de dados no Docker ( Docker + PostgreSQL )
```shell
docker run --name auth-db -p 5432:5432 -e POSTGRES_DB=auth-db -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=terra postgres
```
```shell
docker run --name product-db -p 5433:5432 -e POSTGRES_DB=product-db -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=terra postgres
```
