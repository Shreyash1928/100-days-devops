# Docker Fundamentals Notes

## What is Docker?

Docker is an open-source containerization platform that allows developers to package applications and their dependencies into lightweight, portable containers.

---

# Why Docker?

Before Docker:

* Works on my machine but not on production.
* Dependency conflicts.
* Difficult deployments.
* Large virtual machines.

With Docker:

* Consistent environments.
* Fast deployment.
* Lightweight.
* Portable.
* Easy scaling.

---

# Docker Architecture

```
                Docker Hub
                     │
          docker pull / docker push
                     │
                     ▼
+--------------------------------------+
|          Docker Engine               |
|                                      |
| Docker Client <----> Docker Daemon   |
|        │                             |
|        ▼                             |
|    Images -----> Containers          |
+--------------------------------------+
```

---

## Docker Client

The Docker Client is the command-line interface used to communicate with the Docker Daemon.

Example:

```bash
docker run nginx
```

---

## Docker Daemon

The Docker Daemon (`dockerd`) is responsible for:

* Building images
* Running containers
* Managing networks
* Managing volumes
* Pulling images
* Pushing images

---

## Docker Engine

Docker Engine consists of:

* Docker Client
* Docker Daemon
* REST API

---

## Docker Hub

Docker Hub is a cloud-based registry used to store and share Docker images.

Examples:

* nginx
* ubuntu
* alpine
* mysql
* redis

---

## Docker Image

A Docker Image is:

* Read-only
* Immutable
* Blueprint for containers
* Made up of layers

Example:

```bash
docker pull nginx
```

---

## Docker Container

A container is:

* Running instance of an image
* Isolated
* Lightweight
* Portable

Example:

```bash
docker run nginx
```

---

# Image vs Container

| Image          | Container        |
| -------------- | ---------------- |
| Blueprint      | Running Instance |
| Read-only      | Writable         |
| Static         | Dynamic          |
| Stored on disk | Running process  |

---

# Container Lifecycle

```
Image
  │
docker run
  │
Running
  │
docker stop
  │
Stopped
  │
docker start
  │
Running
  │
docker rm
  │
Deleted
```

---

# Docker Image Layers

Each Dockerfile instruction creates a new layer.

Example:

```
FROM ubuntu
RUN apt update
RUN apt install nginx
COPY . .
CMD ["nginx"]
```

Each instruction above becomes a layer.

---

# Benefits of Layering

* Faster builds
* Less storage
* Layer reuse
* Efficient downloads

---

# Interview Questions

### What is Docker?

Docker is a containerization platform that packages applications along with their dependencies.

---

### Difference between VM and Docker?

Virtual Machines virtualize hardware and include a guest OS.

Docker virtualizes at the operating system level and shares the host kernel.

---

### Difference between Image and Container?

Image is the blueprint.

Container is the running instance.

---

### What happens during docker run?

* Image is checked locally.
* Pulled if not available.
* Container is created.
* Writable layer is added.
* Process starts.

---

### What is Docker Hub?

Docker Hub is the default public registry for Docker images.

---

### What is Docker Inspect?

Displays detailed JSON information about a container or image.

---

### What is Docker Exec?

Runs commands inside an already running container.

