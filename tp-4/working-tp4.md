## Test Registry
```
# récupère l'image sur docker hub
docker pull registry

# lancer un registry local
docker run -d -p 5000:5000 --restart always --name tp4-registry registry

# pousser tp1 sur registry local
docker tag tp1-hello localhost:5000/tp1
docker push localhost:5000/tp1

docker build -t localhost:5000/tp1:1.0.1 .
docker push localhost:5000/tp1:1.0.1


# voir les repo
http://localhost:5000/v2/_catalog


```



## TP4 - Test 1

```
RUN apt update
RUN apt install iputils-ping -y
```


```
cd tp3
docker run --name tp3-node-ping -d -p 8080:8080 tp3-node:1.0.2-ping
cd ../postgres
docker run --name tp4-postgres-ping -d -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword
docker network create tp4-network
docker network connect tp4-network tp3-node
docker network connect tp4-network tp4-postgres

# test
docker exec -it tp4-postgres /bin/bash
ping tp3-node
docker exec -it tp3-node /bin/bash
ping tp4-postgres

```