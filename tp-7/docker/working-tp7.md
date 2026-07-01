

```
cd tp-7/
docker build -t tp7-backend:1.0.0 -f docker/Dockerfile_backend .
docker build -t tp7-client:1.0.0 -f docker/Dockerfile_client .
docker compose -f docker/docker-compose.yml up -d
```