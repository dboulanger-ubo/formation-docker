
## Test 1

Dockerfile 
```
FROM alpine:3.23.5
CMD echo "Hello world"
```
**WARNING**: JSONArgsRecommended: JSON arguments recommended for CMD to prevent unintended behavior related to OS signals

Commandes
```
docker build -t tp1-hello:latest .
docker run tp1-hello:latest
```
_Résultat OK_ : Affiche "Hello world"


## Test 2

Dockerfile 
```
FROM alpine:3.23.5
CMD ["echo","Hello world"]
```

Commandes
```
docker build -t tp1-hello:latest .
docker run tp1-hello:latest
```
_Résultat OK_ : Affiche "Hello world"


## Test 3

Dockerfile 
```
FROM alpine:3.23.5
ENTRYPOINT ["echo","Hello world"]
```

Commandes
```
docker build -t tp1-hello:latest .
docker run tp1-hello:latest
```
_Résultat OK_ : Affiche "Hello world"


## Test 4

Dockerfile 
```
FROM alpine:3.23.5
ENTRYPOINT ["echo"]
CMD ["Hello world"]
```

Commandes
```
docker build -t tp1-hello:latest .
docker run tp1-hello:latest
```
_Résultat OK_ : Affiche "Hello world"

Commandes
```
docker run tp1-hello:latest "OK"
```
_Résultat OK_ : Affiche "OK"

- **ENTRYPOINT** : 1 seul, non modifiable
- **CMD** : surchargeable

