# Docker Networking Notes

# What is Docker Networking?

Docker Networking allows multiple containers to communicate securely with each other while remaining isolated from the host system and other networks.

Every container gets its own network namespace.

---

# Types of Docker Networks

## 1. Bridge Network

The default Docker network.

* Default network for standalone containers
* Containers communicate using IP addresses
* Suitable for single-host deployments

Example:

```bash
docker network inspect bridge
```

---

## 2. Host Network

The container shares the host's network stack.

Advantages:

* Better performance
* No NAT
* No port mapping

Disadvantages:

* Less isolation
* Linux only

---

## 3. None Network

The container has no network connectivity.

Example:

```bash
docker run --network none nginx
```

---

## 4. Custom Bridge Network

Recommended for most Docker applications.

Advantages:

* Automatic DNS
* Better isolation
* Easier container communication
* Production-friendly

Create:

```bash
docker network create devops-network
```

---

# Docker DNS

When containers are connected to the same custom bridge network, Docker automatically creates DNS entries.

Instead of:

```text
172.18.0.2
```

you can simply use:

```text
ubuntu2
```

Example:

```bash
ping ubuntu2
```

---

# Container Communication

```
Container A
      │
      │
 Docker Network
      │
      │
Container B
```

If both containers belong to the same custom network, they can communicate directly.

---

# Port Mapping vs Docker Networking

Port Mapping

* Used for communication between the host and a container.
* Example:

```bash
docker run -p 8080:80 nginx
```

Docker Networking

* Used for communication between containers.
* No exposed ports are required.

---

# Real-world Example

```
Client
   │
   ▼
NGINX Container
   │
   ▼
Backend API Container
   │
   ▼
Database Container
```

All containers communicate through Docker networking.

---

# Interview Questions

## What is Docker Networking?

Docker Networking provides isolated communication between Docker containers.

---

## Why create a Custom Bridge Network?

* Better security
* Automatic DNS
* Easier communication
* Production best practice

---

## Difference between Bridge and Host Network?

Bridge Network

* Isolated 
* Uses NAT
* Requires port mapping

Host Network

* Shares host networking
* Faster
* Less secure

---

## What is Docker DNS?

Docker automatically resolves container names to IP addresses inside a custom bridge network.
