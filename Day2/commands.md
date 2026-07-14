# Docker Commands Cheat Sheet

## Docker Version

```bash
docker version
```

---

## Docker Information

```bash
docker info
```

---

## List Images

```bash
docker images
```

---

## Pull Image

```bash
docker pull nginx
```

```bash
docker pull ubuntu:24.04
```

---

## Run Container

```bash
docker run nginx
```

Interactive:

```bash
docker run -it ubuntu:24.04 bash
```

Detached:

```bash
docker run -d nginx
```

Port Mapping:

```bash
docker run -d -p 8080:80 nginx
```

Name Container:

```bash
docker run --name webserver nginx
```

---

## Running Containers

```bash
docker ps
```

All Containers:

```bash
docker ps -a
```

---

## Stop Container

```bash
docker stop <container-name>
```

---

## Start Container

```bash
docker start <container-name>
```

---

## Restart Container

```bash
docker restart <container-name>
```

---

## Remove Container

```bash
docker rm <container-name>
```

Force Remove:

```bash
docker rm -f <container-name>
```

---

## Remove Image

```bash
docker rmi <image-name>
```

---

## Container Logs

```bash
docker logs <container-name>
```

Live Logs:

```bash
docker logs -f <container-name>
```

---

## Execute Command

```bash
docker exec -it <container-name> bash
```

For Alpine:

```bash
docker exec -it <container-name> sh
```

---

## Inspect Container

```bash
docker inspect <container-name>
```

---

## View Image History

```bash
docker history <image-name>
```

---

## Resource Usage

```bash
docker stats
```

---

## Search Docker Hub

```bash
docker search nginx
```

---

## Login to Docker Hub

```bash
docker login
```

---

## Tag Image

```bash
docker tag local-image username/image:latest
```

---

## Push Image

```bash
docker push username/image:latest
```

---

## Pull Image

```bash
docker pull username/image:latest
```

---

## Clean Up

Remove stopped containers:

```bash
docker container prune
```

Remove unused images:

```bash
docker image prune
```

Remove unused resources:

```bash
docker system prune
```

Remove everything unused:

```bash
docker system prune -a
```
