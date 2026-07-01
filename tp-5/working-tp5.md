
postgreSQL
```
docker run --name tp5-postgres --env PGDATA=/var/lib/postgresql/17/docker --volume ./data:/var/lib/postgresql: -d -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres
```
_Résultat OK_ : les données sont dans le volume

```
CREATE TABLE table_test(  
    id int NOT NULL PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    name VARCHAR(255)
);
COMMENT ON TABLE table_test IS 'table de test';
COMMENT ON COLUMN table_test.name IS 'nom';
INSERT INTO table_test ("test1");
```
```
cd /data/17
ls -al docker/
```
ls: impossible d'ouvrir le répertoire 'docker/': Permission non accordée

=> répertpoire accessible que en root (protection)
=> changer les droits sur le montage changerait aussi les droits sur container : mauvaise 


```
sudo su
ls -al docker/
```

Test de reconstruction 
```
docker rm -f tp5-postgres
docker run --name tp5-postgres --env PGDATA=/var/lib/postgresql/17/docker --volume ./data:/var/lib/postgresql: -d -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres


formation@eiuta25:~/Documents/formation-docker/tp-5/postgres/data/17$ docker run --name tp5-postgres --env PGDATA=/var/lib/postgresql/17/docker --volume ./data:/var/lib/postgresql: -d -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres
docker: invalid spec: ./data:/var/lib/postgresql:: empty section between colons

Run 'docker run --help' for more information
formation@eiuta25:~/Documents/formation-docker/tp-5/postgres/data/17$ cd ../../
formation@eiuta25:~/Documents/formation-docker/tp-5/postgres$ docker run --name tp5-postgres --env PGDATA=/var/lib/postgresql/17/docker --volume ./data:/var/lib/postgresql: -d -p 5432:5432 -e POSTGRES_PASSWORD=mysecretpassword postgres
docker: invalid spec: ./data:/var/lib/postgresql:: empty section between colons

Run 'docker run --help' for more information
```


node

Dockerfile
```
FROM node
WORKDIR /app
COPY package.json .
RUN npm install
ENTRYPOINT ["npm", "start"]
```
```
docker build -t tp5-node:1.0.0 .
docker run --name tp5-node --volume ./volume:/app -d tp5-node:1.0.0
```

Ne démarre pas car le volume sur /app à supprimé TOUT le reste
=> placer le volume autre part

package.json
```
...
    "scripts": {
        "start": "node src/server.js"
    },
...
```

Commandes
```
docker build -t tp5-node:1.0.0 .
docker run --name tp5-node -p 8080:8080 --volume ./volume:/app/src -d tp5-node:1.0.0
docker exec -it tp5-node /bin/bash
$ echo test > src/README.txt
$ ls src/
```
_Résultat OK_ : 
- se lance et affiche "Hello World" sur `localhost:8080`
- le README.txt se retrouve dans `/volume`

