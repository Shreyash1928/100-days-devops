# 🐳 Docker Volumes - Commands Cheat Sheet

This document contains the most commonly used Docker Volume commands along with practical examples.

---

# List Docker Volumes

Displays all available Docker volumes.

```bash
docker volume ls
```

---

# Create a Docker Volume

Creates a named Docker volume.

```bash
docker volume create devops-data
```

Example Output:

```text
devops-data
```

---

# Inspect a Volume

Displays detailed information about a Docker volume.

```bash
docker volume inspect devops-data
```

Example Output:

```text
[
  {
    "Name": "devops-data",
    "Driver": "local",
    "Mountpoint": "/var/lib/docker/volumes/devops-data/_data"
  }
]
```

---

# Remove a Volume

Delete a Docker volume.

```bash
docker volume rm devops-data
```

---

# Remove Unused Volumes

Deletes all unused Docker volumes.

```bash
docker volume prune
```

Skip confirmation:

```bash
docker volume prune -f
```

---

# Run a Container with a Named Volume

```bash
docker run -it \
--name ubuntu-volume \
-v devops-data:/data \
ubuntu:24.04 bash
```

Inside the container:

```bash
echo "Hello DevOps" > /data/info.txt
```

---

# Run Another Container Using the Same Volume

```bash
docker run -it \
-v devops-data:/data \
ubuntu:24.04 bash
```

Verify:

```bash
cat /data/info.txt
```

The file still exists because it is stored in the Docker volume.

---

# Bind Mount Example

Create a host directory:

```bash
mkdir ~/docker-demo
```

Run:

```bash
docker run -it \
-v ~/docker-demo:/data \
ubuntu:24.04 bash
```

Inside the container:

```bash
echo "Docker Bind Mount" > /data/test.txt
```

Exit and verify on the host:

```bash
cat ~/docker-demo/test.txt
```

---

# Read-Only Bind Mount

```bash
docker run -it \
-v ~/docker-demo:/data:ro \
ubuntu:24.04 bash
```

The container can read the files but cannot modify them.

---

# Display Mounted Volumes

```bash
docker inspect ubuntu-volume
```

Look for:

```text
Mounts
```

---

# Display Container Filesystem Changes

```bash
docker diff ubuntu-volume
```

Shows files that have been:

* Added
* Modified
* Deleted

---

# Backup a Docker Volume

```bash
docker run --rm \
-v devops-data:/source \
-v $(pwd):/backup \
ubuntu \
tar czf /backup/devops-backup.tar.gz -C /source .
```

A compressed backup archive will be created in the current directory.

---

# Restore a Docker Volume

```bash
docker run --rm \
-v devops-data:/target \
-v $(pwd):/backup \
ubuntu \
bash -c "cd /target && tar xzf /backup/devops-backup.tar.gz"
```

---

# Check Docker Disk Usage

```bash
docker system df
```

Displays usage of:

* Images
* Containers
* Volumes
* Build Cache

---

# Remove Stopped Containers

```bash
docker container prune
```

---

# Remove Unused Images

```bash
docker image prune
```

---

# Remove Everything Unused

```bash
docker system prune
```

Remove all unused resources including images:

```bash
docker system prune -a
```

---

# Common Docker Volume Commands

| Command                 | Description               |
| ----------------------- | ------------------------- |
| `docker volume ls`      | List volumes              |
| `docker volume create`  | Create a volume           |
| `docker volume inspect` | View volume details       |
| `docker volume rm`      | Remove a volume           |
| `docker volume prune`   | Remove unused volumes     |
| `docker run -v`         | Mount a volume            |
| `docker inspect`        | View mounted volumes      |
| `docker diff`           | Show filesystem changes   |
| `docker system df`      | Display Docker disk usage |

---

# Best Practices

* Use **Named Volumes** for databases and production applications.
* Use **Bind Mounts** during development for live code changes.
* Back up important volumes regularly.
* Avoid storing critical data only in a container's writable layer.
* Remove unused volumes periodically to free disk space.

---

# Interview Commands to Remember

```bash
docker volume ls
docker volume create devops-data
docker volume inspect devops-data
docker volume rm devops-data
docker volume prune
docker run -v devops-data:/data ubuntu
docker inspect <container-name>
docker system df
docker diff <container-name>
```

These are the commands most commonly used while working with Docker volumes in development and production environments.
