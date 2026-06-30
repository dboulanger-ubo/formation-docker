## Test 1

Dockerfile
```
FROM alpine:3.23.5

WORKDIR /home/app

COPY run.sh .

ENTRYPOINT ["./run.sh"]
```

Commandes
```
docker build -t tp2-run:1.0.0.
docker run tp2-run:1.0.0
```

docker: Error response from daemon: failed to create task for container: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: exec: "./run.sh": **permission denied**

## Test 2

Dockerfile
```
FROM alpine:3.23.5

WORKDIR /home/app

COPY run.sh .

ENTRYPOINT ["/bin/sh", "run.sh"]
```

Commandes
```
docker build -t tp2-run:1.0.1.
docker run tp2-run:1.0.1
```
_Résultat OK_ : Affiche
```
/home:
app

/home/app:
run.sh
```

