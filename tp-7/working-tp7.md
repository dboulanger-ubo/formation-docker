
docker
- sqlite
- 2 images (backend / client)
- 2 services
- partage du `dist` en volume partagé

```
cd tp-7/
docker build -t tp7-backend:1.0.0 -f docker/Dockerfile_backend .
docker build -t tp7-client:1.0.0 -f docker/Dockerfile_client .
docker compose -f docker/docker-compose.yml up -d
```
_Résultat OK_ : Todo App sur http://localhost:3000/


docker_02
- sqlite
- un seul Dockerfile (le client est exposé par le backend via le dossier dist)
- construction de l'image directement via le docker-compose (attention au context et à la localisation du Dockerfile)
- un seul service exposé (le backend - nommé web)
- `cp` du `/client/dist/*` sous `/backend/src/static/` directement dans le Dockerfile
  
```
cd tp-7/
docker compose -f docker/docker-compose.yml up -d
```
_Résultat OK_ : Todo App sur http://localhost:3001/


docker_03
- mariadb
