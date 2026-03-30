# 🐳 Docker: Complete Guide (Easy Notes + Commands)

This file is a **complete but simple** Docker guide. It explains **how Docker works** and gives you the **commands you’ll use in labs and real jobs**.

---

## 1) What is Docker (in one line)

Docker is a tool that helps you **build**, **share**, and **run** applications in **containers**.

> Container = your app + everything it needs, packed together.

**Real-life example:**
Shipping a cake is hard if everyone uses different ovens. Docker is like shipping the cake in a sealed box with instructions so it tastes the same everywhere.

---

## 2) Docker architecture (who does what)

Docker has 3 important parts:
- **Docker Client**: you type commands (`docker run`, `docker build`)
- **Docker Daemon (dockerd)**: does the real work in background
- **Registry (Docker Hub / private)**: stores images

**Simple flow:**
Client asks → Daemon builds/pulls/runs → Registry stores images.

---

## 3) What happens when you run a container

Example:

```bash
docker run -d -p 8080:80 nginx
```

Internally (easy version):
1) Docker checks if `nginx` image exists locally
2) If not, Docker pulls it from Docker Hub
3) Docker creates a container from that image
4) Docker starts the container
5) Port mapping forwards your laptop’s `8080` to container’s `80`

---

## 4) First commands to check Docker is working

```bash
docker version
docker info
docker ps
docker images
```

---

## 5) Docker CLI basics (must-know commands)

### A) Image commands

```bash
docker pull ubuntu
docker images
docker rmi ubuntu
docker inspect ubuntu
docker history ubuntu
docker search nginx
```

### B) Container commands

```bash
docker run -d --name web nginx
docker ps
docker ps -a
docker stop web
docker start web
docker rm web
docker logs web
docker exec -it web sh
docker inspect web
```

### C) System/cleanup commands

```bash
docker system df
docker system prune
docker system prune -a
docker system prune -a --volumes
```

⚠️ `docker system prune -a --volumes` can delete stored data in volumes.

---

## 6) The most important command: `docker run` (flags you’ll use)

Think of `docker run` like “start a mini-computer for my app”.

Common flags:
- `--name` → easy container name
- `-d` → run in background
- `-it` → interactive terminal
- `-p host:container` → port mapping
- `-e KEY=VALUE` → environment variables
- `-v source:target` → volume/bind mount
- `--network` → connect to a network

Example (single line, works in PowerShell too):

```bash
docker run -d --name myapp -p 8080:3000 -e DB_HOST=db.local -v mydata:/app/data --network mynet myimage:1.0
```

---

## 7) Docker Hub / Registry (ship images)

### Image naming format

`<registry>/<namespace>/<image>:<tag>`

Example:

`docker.io/library/ubuntu:20.04`

### Push an image (basic workflow)

```bash
docker login
docker tag myapp:1.0 username/myapp:1.0
docker push username/myapp:1.0
```

Now anyone can pull it:

```bash
docker pull username/myapp:1.0
```

---

## 8) Docker objects (what Docker manages)

Docker mainly manages:
- **Images** (blueprints)
- **Containers** (running apps)
- **Networks** (container communication)
- **Volumes** (persistent data)

---

## 9) Networks (containers talk to each other)

Default network is usually `bridge`, but custom networks are cleaner.

```bash
docker network ls
docker network create mynet
docker network inspect mynet
```

Run two containers on same network:

```bash
docker run -d --name web --network mynet nginx
docker run -d --name db --network mynet postgres
```

Why custom network is useful:
- containers can resolve each other by name (like `db`)
- better isolation than dumping everything into default network

---

## 10) Volumes (data should not disappear)

Containers are easy to delete/recreate. Your data should survive.

> Volume = Docker-managed storage that stays even if the container is removed.

Commands:

```bash
docker volume create mydata
docker volume ls
docker volume inspect mydata
docker volume rm mydata
docker volume prune
```

Use a volume with a container:

```bash
docker run -d --name web -v mydata:/usr/share/nginx/html nginx
```

**Real-life example:**
Container is your rented room; volume is your personal locker.

---

## 11) Docker layers (why builds are fast)

Images are built in **layers**.

Useful commands:

```bash
docker history myimage:1.0
docker inspect myimage:1.0
```

Simple rule:
- if a Dockerfile line changes, that layer and the layers after it rebuild
- unchanged layers are reused from cache

---

## 12) Dockerfile basics (build your own image)

Dockerfile = recipe to build an image.

Minimal example:

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```

Build it:

```bash
docker build -t myapp:1.0 .
docker images
```

Run it:

```bash
docker run -d --name myapp -p 5000:5000 myapp:1.0
docker logs myapp
```

---

## 13) Mini end-to-end workflow (build → ship → run)

```bash
docker build -t myflaskapp:1.0 .
docker run -d --name myflask -p 5000:5000 myflaskapp:1.0
docker tag myflaskapp:1.0 username/myflaskapp:1.0
docker login
docker push username/myflaskapp:1.0
```

On another machine:

```bash
docker pull username/myflaskapp:1.0
docker run -d -p 5000:5000 username/myflaskapp:1.0
```

---

## 14) Best practices (short + exam-friendly)

- Prefer **official images** (more trusted)
- Always use **tags** (don’t depend on `latest` only)
- Keep images small (use `slim`, clean caches)
- Put frequently changing files later in Dockerfile (better build cache)
- Use volumes for data (don’t store DB data inside container layer)
- Use `docker logs`, `docker exec`, `docker inspect` for troubleshooting

---

## Summary

- Docker = build, ship, run containers.
- Learn these first: `pull`, `images`, `run`, `ps`, `logs`, `exec`, `inspect`, `network`, `volume`, `system prune`, `build`, `tag`, `push`.
