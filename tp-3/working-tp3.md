## Test 1

Dockerfile
```
FROM node

WORKDIR /app

COPY package.json .
COPY server.js .

RUN npm install

ENTRYPOINT ["npm", "start"]
```

Commandes
```
docker build -t tp3-node:1.0.0 .
docker run -p 8080:8080 tp3-node:1.0.0
```
_Résultat OK_ : localhost:8080 Affiche Hello world