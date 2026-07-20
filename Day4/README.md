# 🚀 Day 4 – Docker Volumes & Persistent Storage

## 🎯 Objective

The objective of Day 4 is to understand how Docker manages data and how to persist application data beyond the lifecycle of a container.

By the end of this session, I will understand why data stored inside a container is temporary and how Docker Volumes and Bind Mounts solve this problem.

---

# 📚 Topics Covered

* Docker Storage
* Writable Container Layer
* Docker Volumes
* Named Volumes
* Anonymous Volumes
* Bind Mounts
* Volume Lifecycle
* Volume Management
* Volume Backup & Restore
* Persistent Storage Best Practices

---

# 📖 Why Persistent Storage?

Containers are designed to be **ephemeral**, meaning they can be created, stopped, removed, and recreated at any time.

If important application data is stored only inside the container, it will be lost when the container is deleted.

Docker provides **Volumes** and **Bind Mounts** to persist data independently of the container.

---

# 🏗️ Architecture

```text
                 Docker Host

        +---------------------------+
        |                           |
        |     Docker Volume         |
        |      (Persistent Data)    |
        |            ▲              |
        |            │              |
        +------------│--------------+
                     │
              Mounted into
                     │
                     ▼
        +---------------------------+
        |      Docker Container     |
        |                           |
        |      /data                |
        |      app.log              |
        |      database.db          |
        +---------------------------+
```

---

# 🧪 Practical Exercises

During Day 4, I will:

* Create Docker Volumes
* Inspect Volumes
* Attach Volumes to Containers
* Verify Data Persistence
* Create Bind Mounts
* Compare Volumes and Bind Mounts
* Understand Real-world Storage Use Cases

---

# 💻 Commands Practiced

```bash
docker volume ls
docker volume create
docker volume inspect
docker volume rm
docker volume prune

docker run -v
docker inspect
```

---

# 🎯 Learning Outcomes

After completing Day 4, I will be able to:

* Explain Docker storage architecture.
* Understand the writable layer of containers.
* Create and manage Docker Volumes.
* Mount host directories using Bind Mounts.
* Preserve application data after container removal.
* Decide when to use Volumes or Bind Mounts.

---

# 🌍 Real-World Use Cases

Docker Volumes are commonly used for:

* MySQL Databases
* PostgreSQL Databases
* MongoDB
* Jenkins
* SonarQube
* Nexus Repository
* Grafana
* Prometheus
* Redis

Without persistent storage, all application data would be lost whenever the container is removed.

---

# 📌 Key Takeaways

* Containers are temporary.
* Volumes provide persistent storage.
* Bind Mounts connect host directories to containers.
* Docker manages volumes automatically.
* Volumes are preferred for production workloads.

---

# 📅 Progress

| Day     | Topic                    | Status    |
| ------- | ------------------------ | --------- |
| ✅ Day 1 | Dockerize Static Website | Completed |
| ✅ Day 2 | Docker Fundamentals      | Completed |
| ✅ Day 3 | Docker Networking        | Completed |
| ✅ Day 4 | Docker Volumes & Storage | Completed |

---

# 📖 What's Next?

**Day 5 – Docker Compose**

Topics include:

* Multi-container Applications
* docker-compose.yml
* Nginx + MySQL + Application Stack
* Service Communication
* Environment Variables
* Compose Commands

---

## 🎯 Summary

Day 4 focuses on one of Docker's most important production features—**persistent storage**.

Understanding Docker Volumes and Bind Mounts is essential for deploying stateful applications such as databases, CI/CD servers, monitoring tools, and enterprise applications. This knowledge forms a strong foundation before moving on to Docker Compose and multi-container deployments.
