# Node.js + MongoDB using Docker Compose

## Introduction

Docker Compose allows multiple containers to run together using a single YAML configuration file.

In this project:
- Node.js container acts as application service
- MongoDB container acts as database service

Both services communicate using Docker Compose networking.

---

# Services Used

## 1. Node.js Service

Used as application container.

```yaml
app:
  image: node:18
```

---

## 2. MongoDB Service

Used as database container.

```yaml
mongo:
  image: mongo:6
```

---

# Features Used

- Multi-container deployment
- Docker Compose networking
- Environment variables
- Persistent volumes
- Service dependency management

---

# Environment Variables

```yaml
environment:
  - MONGO_URL=mongodb://mongo:27017/mydb
```

Explanation:
- `mongo` is the MongoDB service name
- `27017` is MongoDB default port
- `mydb` is database name

---

# depends_on

```yaml
depends_on:
  - mongo
```

Ensures MongoDB container starts before Node.js container.

---

# Volumes

```yaml
volumes:
  - mongo-data:/data/db
```

Used for persistent MongoDB data storage.

---

# Docker Compose Networking

Docker Compose automatically creates:
- internal network
- DNS-based communication

Containers communicate using service names.

Example:

```text
mongodb://mongo:27017/mydb
```

---

# Advantages

- Easy multi-container management
- Simplified networking
- Better scalability
- Portable development environment
- Faster deployment

---

# Important Viva Questions

## 1. Why is Docker Compose used?
Docker Compose is used to manage multi-container applications.

---

## 2. What is the role of depends_on?
It controls startup order between services.

---

## 3. Why are volumes used?
Volumes provide persistent data storage.

---

## 4. How do containers communicate in Docker Compose?
Containers communicate using service names through Docker networking.

---

## 5. What is the default MongoDB port?
27017

---

# Conclusion

Docker Compose simplifies deployment and management of Node.js and MongoDB multi-container applications.


