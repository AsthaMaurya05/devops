# Docker Compose Basics

## Introduction

Docker Compose is a tool used to define and manage multi-container Docker applications using a YAML configuration file.

Instead of running multiple `docker run` commands manually, Docker Compose allows the complete application stack to be managed using a single file.

---

# Why Docker Compose?

Modern applications usually contain multiple services such as:
- Frontend
- Backend
- Database
- Cache

Managing them manually becomes difficult.

Docker Compose helps by:
- Managing multiple containers
- Creating networks automatically
- Handling dependencies
- Simplifying deployment

---

# Key Features

- Multi-container management
- Declarative configuration
- Automatic networking
- Service dependency management
- Scalability support
- Reproducible environments

---

# Docker Compose File

Docker Compose uses a file named:

```yaml
docker-compose.yml
```

Basic structure:

```yaml
version: "3.9"

services:
  web:
    image: nginx
```

---

# Important Components

## 1. version
Defines Docker Compose file version.

```yaml
version: "3.9"
```

---

## 2. services
Defines containers used in the application.

```yaml
services:
  web:
    image: nginx
```

---

## 3. ports
Maps host port to container port.

```yaml
ports:
  - "8080:80"
```

Format:

```text
HostPort:ContainerPort
```

---

## 4. volumes
Used for persistent storage.

```yaml
volumes:
  - data:/var/lib/mysql
```

---

## 5. depends_on
Controls startup order.

```yaml
depends_on:
  - db
```

---

# Basic Docker Compose Example

```yaml
version: "3.9"

services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

---

# Common Docker Compose Commands

## Start Services

```bash
docker compose up
```

Start in background:

```bash
docker compose up -d
```

---

## Stop Services

```bash
docker compose down
```

---

## View Running Containers

```bash
docker compose ps
```

---

## View Logs

```bash
docker compose logs
```

Live logs:

```bash
docker compose logs -f
```

---

## Scale Services

```bash
docker compose up --scale web=3
```

---

# Practical Steps

## Step 1: Create docker-compose.yml

```yaml
version: "3.9"

services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

---

## Step 2: Run Docker Compose

```bash
docker compose up -d
```

---

## Step 3: Verify Running Containers

```bash
docker compose ps
```

---

## Step 4: Open Browser

Visit:

```text
http://localhost:8080
```

---

# Screenshots

## Docker Compose Up

Add screenshot here:

```md
![Docker Compose Up](screenshots/docker-compose-up.png)
```

---

## Running Containers

```md
![Docker Compose PS](screenshots/docker-compose-ps.png)
```

---

## Nginx Running in Browser

```md
![Nginx Output](screenshots/nginx-browser-output.png)
```

---

# Advantages of Docker Compose

- Simplifies multi-container deployment
- Easy configuration management
- Better reproducibility
- Faster development setup
- Automatic networking

---

# Important Viva Questions

## 1. What is Docker Compose?
Docker Compose is a tool used to manage multi-container Docker applications using YAML files.

---

## 2. What is the default Docker Compose file name?
`docker-compose.yml`

---

## 3. What is the purpose of depends_on?
It controls service startup order.

---

## 4. What is port mapping?
Port mapping connects host ports to container ports.

---

## 5. Which command starts all services?
```bash
docker compose up
```

---

# Conclusion

Docker Compose simplifies deployment and management of multi-container applications using a single YAML configuration file.


