# 🚀 Day 2 – Docker Fundamentals & Container Management

## 📌 Objective

The goal of Day 2 was to understand how Docker works internally and gain hands-on experience managing Docker images and containers using commonly used Docker CLI commands.

---

## 📖 Topics Covered

* Docker Architecture
* Docker Engine
* Docker Client
* Docker Daemon
* Docker Images
* Docker Containers
* Docker Hub
* Container Lifecycle
* Docker CLI
* Docker Logs
* Docker Inspect
* Docker Exec
* Docker History
* Docker Statistics

---

## 🛠️ Practical Commands

* View Docker version
* Display Docker information
* Pull Docker images
* Create containers
* Start containers
* Stop containers
* Restart containers
* Remove containers
* Remove images
* View logs
* Execute commands inside running containers
* Inspect container details
* Monitor resource usage

---

## 📚 Key Learnings

* Docker packages applications with all their dependencies.
* Docker images are read-only templates.
* Containers are running instances of images.
* Containers are lightweight compared to virtual machines.
* Docker Hub acts as a central registry for Docker images.
* Every Docker image consists of multiple read-only layers.
* Containers have their own isolated filesystem, networking, and processes.

---

## 💻 Hands-on Exercise

### Pull Ubuntu Image

```bash
docker pull ubuntu:24.04
```

### Run Ubuntu Container

```bash
docker run -it ubuntu:24.04 bash
```

### Explore Container

```bash
cat /etc/os-release
hostname
pwd
ls
mkdir demo
cd demo
echo "Hello DevOps" > test.txt
cat test.txt
exit
```

### Inspect Running Container

```bash
docker inspect <container-name>
```

### Execute Command in Running Container

```bash
docker exec -it <container-name> bash
```

---

## 🎯 Outcome

At the end of Day 2, I understood:

* Docker Architecture
* Image vs Container
* Docker Container Lifecycle
* Basic Container Management
* Docker Troubleshooting Commands

---

## 📅 Progress

* ✅ Day 1 – Dockerize Static Website
* ✅ Day 2 – Docker Fundamentals & Container Management

---

**Next Goal:** Docker Networking, Volumes, and Persistent Storage.
