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
docker build -t tp3-node:1.0.2-ping .
docker run --name tp3-node-ping -d -p 8080:8080 tp3-node:1.0.2-ping
cd ../postgres
docker build -t tp4-postgres:1.0.0-ping .
docker run --name tp4-postgres-ping -d -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword tp4-postgres:1.0.0-ping
docker network create tp4-network
docker network connect tp4-network tp3-node-ping
docker network connect tp4-network tp4-postgres-ping
```


# test
```
$ docker exec -it tp4-postgres-ping /bin/bash
$ ping tp3-node-ping 
PING tp3-node-ping (172.19.0.2) 56(84) bytes of data.
64 bytes from tp3-node-ping.tp4-network (172.19.0.2): icmp_seq=1 ttl=64 time=0.132 ms
64 bytes from tp3-node-ping.tp4-network (172.19.0.2): icmp_seq=2 ttl=64 time=0.057 ms
64 bytes from tp3-node-ping.tp4-network (172.19.0.2): icmp_seq=3 ttl=64 time=0.082 ms
64 bytes from tp3-node-ping.tp4-network (172.19.0.2): icmp_seq=4 ttl=64 time=0.080 ms

```
```
$ docker exec -it tp3-node-ping /bin/bash
$ ping tp4-postgres-ping 
PING tp4-postgres-ping (172.19.0.3) 56(84) bytes of data.
64 bytes from tp4-postgres-ping.tp4-network (172.19.0.3): icmp_seq=1 ttl=64 time=0.041 ms
64 bytes from tp4-postgres-ping.tp4-network (172.19.0.3): icmp_seq=2 ttl=64 time=0.085 ms
64 bytes from tp4-postgres-ping.tp4-network (172.19.0.3): icmp_seq=3 ttl=64 time=0.079 ms
64 bytes from tp4-postgres-ping.tp4-network (172.19.0.3): icmp_seq=4 ttl=64 time=0.081 ms

```

Correction (associer au network au run)
```
docker run --name tp3-node-ping -d -p 8080:8080 --network tp4-network tp3-node:1.0.2-ping
docker run --name tp4-postgres-ping -d -e POSTGRES_PASSWORD=mysecretpassword --network tp4-network tp4-postgres:1.0.0-ping
```