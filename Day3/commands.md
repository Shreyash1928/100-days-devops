# commands.md

## List Networks

```bash
docker network ls
```

---

## Inspect Network

```bash
docker network inspect bridge
```

---

## Create Network

```bash
docker network create devops-network
```

---

## Remove Network

```bash
docker network rm devops-network
```

---

## Connect Container

```bash
docker network connect devops-network ubuntu1
```

---

## Disconnect Container

```bash
docker network disconnect devops-network ubuntu1
```

---

## Remove Unused Networks

```bash
docker network prune
```

---

## Run Container in Custom Network

```bash
docker run -dit --name ubuntu1 --network devops-network ubuntu:24.04
```

```bash
docker run -dit --name ubuntu2 --network devops-network ubuntu:24.04
```

---

## Enter Running Container

```bash
docker exec -it ubuntu1 bash
```

---

## View Container IP

```bash
docker inspect ubuntu1
```

---

# lab.md

# 🧪 Lab 1 – Explore Docker Networks

### Step 1

View available networks.

```bash
docker network ls
```

---

### Step 2

Inspect the default bridge network.

```bash
docker network inspect bridge
```

Observe:

* Subnet
* Gateway
* Connected Containers

---

# 🧪 Lab 2 – Create a Custom Network

```bash
docker network create devops-network
```

Verify:

```bash
docker network ls
```

---

# 🧪 Lab 3 – Connect Two Ubuntu Containers

```bash
docker run -dit --name ubuntu1 --network devops-network ubuntu:24.04
```

```bash
docker run -dit --name ubuntu2 --network devops-network ubuntu:24.04
```

---

# 🧪 Lab 4 – Test Communication

Enter the first container:

```bash
docker exec -it ubuntu1 bash
```

Install ping:

```bash
apt update
apt install iputils-ping -y
```

Ping the second container:

```bash
ping ubuntu2
```

Expected result:

```
PING ubuntu2 (...) ...
64 bytes from ubuntu2 ...
```

This demonstrates Docker's built-in DNS.

---

# 🧪 Lab 5 – Nginx and Alpine Communication

Create a new network:

```bash
docker network create web-network
```

Run Nginx:

```bash
docker run -dit --name nginx-server --network web-network nginx
```

Run Alpine:

```bash
docker run -it --network web-network alpine sh
```

Install curl:

```sh
apk add curl
```

Access the Nginx server:

```sh
curl http://nginx-server
```

You should receive the default Nginx HTML page.

---

# 🎯 Lab Outcome

After completing these labs, you will be able to:

* Understand Docker networking
* Create and inspect networks
* Connect multiple containers
* Verify communication using Docker DNS
* Troubleshoot container networking
* Understand how microservices communicate in Docker
