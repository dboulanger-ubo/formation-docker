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
```


**voir les repo** : 
http://localhost:5000/v2/_catalog

