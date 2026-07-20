# 🧪 Day 4 - Docker Volumes Lab

## 🎯 Objective

The objective of this lab is to understand how Docker stores data and how Docker Volumes help preserve data even after a container is removed.

---

# Lab 1 - Verify Data Loss Without a Volume

### Step 1

Run an Ubuntu container.

```bash
docker run -it --name ubuntu-temp ubuntu:24.04 bash
```

---

### Step 2

Create a directory and file.

```bash
mkdir demo

echo "Hello DevOps" > demo/info.txt

cat demo/info.txt
```

Expected Output

```text
Hello DevOps
```

Exit the container.

```bash
exit
```

---

### Step 3

Remove the container.

```bash
docker rm ubuntu-temp
```

---

### Step 4

Create a new container.

```bash
docker run -it ubuntu:24.04 bash
```

Check for the file.

```bash
ls demo
```

Expected Result

```text
ls: cannot access 'demo': No such file or directory
```

### Observation

The file disappeared because it was stored inside the writable layer of the deleted container.

---

# Lab 2 - Create a Docker Volume

Create a named volume.

```bash
docker volume create devops-volume
```

Verify:

```bash
docker volume ls
```

Expected Output

```text
DRIVER    VOLUME NAME

local     devops-volume
```

Inspect the volume.

```bash
docker volume inspect devops-volume
```

Observe:

* Name
* Driver
* Mountpoint

---

# Lab 3 - Persist Data Using a Docker Volume

Run Ubuntu with the volume attached.

```bash
docker run -it \
--name volume-test \
-v devops-volume:/data \
ubuntu:24.04 bash
```

Inside the container:

```bash
echo "Docker Volumes are Persistent" > /data/file.txt

cat /data/file.txt
```

Expected Output

```text
Docker Volumes are Persistent
```

Exit the container.

```bash
exit
```

Remove it.

```bash
docker rm volume-test
```

Create another container using the same volume.

```bash
docker run -it \
-v devops-volume:/data \
ubuntu:24.04 bash
```

Verify.

```bash
cat /data/file.txt
```

Expected Output

```text
Docker Volumes are Persistent
```

### Observation

The file still exists because it is stored in the Docker Volume instead of the container.

---

# Lab 4 - Bind Mount

Create a folder on the host.

```bash
mkdir ~/docker-demo
```

Run Ubuntu.

```bash
docker run -it \
-v ~/docker-demo:/data \
ubuntu:24.04 bash
```

Inside the container:

```bash
echo "Hello Host Machine" > /data/test.txt
```

Exit.

```bash
exit
```

On the host machine:

```bash
cat ~/docker-demo/test.txt
```

Expected Output

```text
Hello Host Machine
```

### Observation

The file exists both on the host and inside the container because both share the same directory.

---

# Lab 5 - Live Website Editing with Nginx

Move into your Day1 project.

```bash
cd ~/Desktop/Devops/Day1
```

Run Nginx using a bind mount.

```bash
docker run -d \
--name nginx-volume \
-p 8081:80 \
-v $(pwd):/usr/share/nginx/html \
nginx
```

Open your browser.

```text
http://localhost:8081
```

Edit the HTML.

```bash
vi index.html
```

or

```bash
code index.html
```

Refresh the browser.

### Observation

Changes appear immediately without rebuilding the Docker image.

---

# Lab 6 - Inspect Mounted Volumes

Run:

```bash
docker inspect nginx-volume
```

Locate:

```text
Mounts
```

Observe:

* Source
* Destination
* Type
* ReadOnly

---

# Lab 7 - Docker Disk Usage

Check Docker storage.

```bash
docker system df
```

Observe:

* Images
* Containers
* Volumes
* Build Cache

---

# Lab 8 - Remove Unused Volumes

Delete unused volumes.

```bash
docker volume prune
```

Verify:

```bash
docker volume ls
```

---

# Challenge

Create a volume called:

```text
portfolio-data
```

Store three files inside it:

```text
resume.pdf

notes.txt

projects.md
```

Delete the container.

Create a new container using the same volume.

Verify all files still exist.

---

# Lab Summary

After completing this lab, you should be able to:

* Create Docker Volumes
* Inspect Docker Volumes
* Mount Volumes
* Persist Application Data
* Create Bind Mounts
* Understand the Difference Between Volumes and Bind Mounts
* Inspect Mounted Storage
* Clean Up Unused Storage
* Explain Docker Persistent Storage in an Interview

---

# Interview Questions

1. Why does data disappear after deleting a container?

2. What is a Docker Volume?

3. What is the difference between a Docker Volume and a Bind Mount?

4. Why are Volumes preferred for databases?

5. Where are Docker Volumes stored on Linux?

6. Can multiple containers use the same Docker Volume?

7. How do you back up a Docker Volume?

8. What is the purpose of Bind Mounts during development?

---

# 🎯 Day 4 Outcome

By completing these labs, you have learned one of the most important production concepts in Docker—**persistent storage**. This knowledge is essential for deploying databases, CI/CD tools like Jenkins, monitoring tools like Grafana and Prometheus, and other stateful applications where data must survive container restarts and recreation.
