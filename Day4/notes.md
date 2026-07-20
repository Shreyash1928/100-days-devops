# 📘 Docker Volumes & Persistent Storage Notes

# What is Docker Storage?

Every Docker container needs a place to store data.

Docker provides different storage mechanisms depending on how long the data should live.

By default, all files created inside a container are stored in the container's **writable layer**.

---

# Container Writable Layer

Every Docker container consists of:

* Read-only image layers
* One writable container layer

```text
                Docker Image
        ----------------------------
        Layer 1
        Layer 2
        Layer 3
        ----------------------------
               Writable Layer
                    │
                    ▼
            Running Container
```

The writable layer is created when the container starts.

All files created, modified, or deleted inside the container are stored here.

---

# Problem with Writable Layer

The writable layer belongs only to that specific container.

When the container is removed:

```bash
docker rm my-container
```

the writable layer is deleted as well.

This means:

* Files disappear
* Databases disappear
* Logs disappear
* User uploads disappear

This is why Docker containers are called **ephemeral**.

---

# What is a Docker Volume?

A Docker Volume is a Docker-managed storage location that exists independently of containers.

Unlike the writable layer, volumes remain available even after containers are deleted.

Volumes provide persistent storage for applications.

---

# Docker Volume Architecture

```text
                Docker Host

          +----------------------+
          |      Volume          |
          |   devops-volume      |
          +----------+-----------+
                     │
                     │ Mounted
                     ▼
          +----------------------+
          |     Container        |
          |                      |
          |      /data           |
          |                      |
          +----------------------+
```

The container uses the volume, but the volume is stored separately.

---

# Why Do We Need Volumes?

Without volumes:

* Container removed
* Data removed

With volumes:

* Container removed
* Data remains
* New container can reuse the same data

This is essential for databases and applications that store user data.

---

# Types of Docker Storage

## 1. Writable Layer

* Temporary
* Deleted with container
* Managed automatically

---

## 2. Named Volume

Created and managed by Docker.

Example:

```bash
docker volume create devops-data
```

Advantages:

* Persistent
* Easy to manage
* Production ready
* Recommended for databases

---

## 3. Anonymous Volume

Docker automatically creates a volume without a name.

Example:

```bash
docker run -v /data nginx
```

Disadvantages:

* Difficult to identify
* Harder to reuse
* Usually temporary

---

## 4. Bind Mount

Maps a host directory directly into a container.

Example:

```bash
docker run -v ~/project:/app nginx
```

Here,

Host:

```text
~/project
```

Container:

```text
/app
```

Both point to the same files.

Changes made on one side immediately appear on the other.

---

# Docker Volume vs Bind Mount

| Docker Volume              | Bind Mount         |
| -------------------------- | ------------------ |
| Managed by Docker          | Managed by Host    |
| Portable                   | Host dependent     |
| Better security            | Full host access   |
| Recommended for Production | Mostly Development |
| Easy Backup                | Manual Backup      |

---

# Docker Volume Lifecycle

```text
Create Volume
      │
      ▼
Attach to Container
      │
      ▼
Container Uses Data
      │
      ▼
Container Removed
      │
      ▼
Volume Still Exists
      │
      ▼
Attach to New Container
```

---

# Docker Volume Commands

Create

```bash
docker volume create my-volume
```

List

```bash
docker volume ls
```

Inspect

```bash
docker volume inspect my-volume
```

Remove

```bash
docker volume rm my-volume
```

Delete Unused Volumes

```bash
docker volume prune
```

---

# Where Are Volumes Stored?

On Linux:

```text
/var/lib/docker/volumes/
```

Docker manages this directory automatically.

Users normally should not modify these files manually.

---

# Real-World Examples

## MySQL

```bash
docker run -d \
-v mysql-data:/var/lib/mysql \
mysql
```

Database remains even if the container is deleted.

---

## Jenkins

```bash
docker run -d \
-v jenkins-data:/var/jenkins_home \
jenkins/jenkins:lts
```

Build history remains.

---

## MongoDB

```bash
docker run -d \
-v mongo-data:/data/db \
mongo
```

Database persists.

---

# Interview Questions

## What is a Docker Volume?

A Docker Volume is a Docker-managed persistent storage mechanism used to store application data independently of containers.

---

## Why use Docker Volumes?

To preserve application data even after a container is removed.

---

## What happens if a container is deleted?

* Writable layer is deleted.
* Volumes remain.
* Bind-mounted host files remain.

---

## Difference between Volume and Bind Mount?

Volumes are managed by Docker and are recommended for production.

Bind Mounts directly expose host directories and are commonly used during development.

---

## Why are Volumes important?

Without persistent storage, applications such as databases, Jenkins, and monitoring tools would lose all their data whenever a container is recreated.

---

# Key Takeaways

✅ Containers are temporary.

✅ Writable layers are temporary.

✅ Volumes provide persistent storage.

✅ Bind Mounts connect host directories.

✅ Volumes are preferred for production environments.

✅ Every DevOps Engineer should understand Docker storage before learning Docker Compose and Kubernetes.
