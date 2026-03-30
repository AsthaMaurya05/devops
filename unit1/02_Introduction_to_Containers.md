# 📦 Introduction to Containers (with Docker Commands)

These notes explain containers in **easy language**, with **real-life examples**, and lots of **Docker commands you can practice**.

---

## 1) Why we needed containers (problem + real life)

Before containers, teams used to say:

> “It works on my laptop, but not on the server.”

Why it happens:
- Different OS (Windows vs Linux)
- Different versions (Python 3.10 vs 3.8)
- Missing libraries/config

**Real-life example:**
You made tea at home using your own kitchen setup (milk, sugar, stove). Now you go to a friend’s house, but their kitchen is different. Same recipe, different results.

**Container idea:**
A container is like carrying your **own mini-kitchen box** with everything needed for your “tea” (your app) so it tastes the same everywhere.

---

## 2) Virtualization vs Containerization (very simple)

Businesses wanted to:
- reduce hardware cost
- scale quickly
- deploy apps in a standard way

So two approaches became common:

### A) Virtual Machines (VMs) = “multiple full computers inside one computer”
- Uses a **hypervisor** to split one physical server into many VMs
- Each VM has its **own full OS**

✅ Advantages (from lecture): better isolation, resource usage, disaster recovery, security, cost saving

❌ Drawbacks (why containers happened):
- Heavy resource overhead (each VM has OS)
- Slow boot time
- Harder scaling
- Portability issues
- More management work

### B) Containers = “multiple isolated apps sharing one OS kernel”
Containers **do not carry a full OS**.
They share the **host OS kernel** and only bring what the app needs.

Why people love containers:
- Start in seconds
- Use less RAM/CPU
- Run many on one machine

**Real-life example:**
- VM = renting **separate full houses** for each family (expensive)
- Container = renting **separate rooms in the same building** (cheaper, fast)

---

## 3) Container runtime (what actually runs containers)

An **image** is just a read-only package (blueprint).
To actually run it, you need a **container runtime**.

> Container runtime = the software that creates/starts/stops containers.

### Types of runtimes

**High-level runtimes (you use directly / DevOps tools use):**
- Docker Engine
- containerd
- CRI-O (Kubernetes focused)

They handle: image pull, networking, storage, lifecycle.

**Low-level runtime (does the actual “run”):**
- runc (OCI compliant)

It interacts with Linux kernel features like namespaces and cgroups.

**Lunchbox analogy (from lecture):**
- Container image = packed lunchbox
- Container runtime = person who opens it, serves food, and cleans up

---

## 4) How containers stay isolated (Namespaces + cgroups)

### A) Namespaces = “isolation”
Namespaces make each container feel like it has its own system.

Common namespaces used:
- **PID namespace:** container has its own process IDs (inside container starts from PID 1)
- **Network namespace:** each container has its own IP and ports (internally)
- **Mount namespace:** container has its own filesystem view
- **UTS namespace:** container has its own hostname
- **User namespace (advanced):** maps container users to non-root on host (security)

**Train cabin analogy (from lecture):**
Same train engine (kernel), separate cabins (namespaces), passengers can’t see other cabins.

### B) cgroups = “resource limits and control”

> Namespaces isolate, cgroups control.

cgroups ensure one container cannot take all:
- CPU
- memory
- disk I/O

**Apartment electricity analogy (from lecture):**
Each apartment has a meter/limit so one tenant can’t use all power.

---

## 5) Images vs containers (blueprint vs running app)

### Container image
Image is a **read-only blueprint** that contains:
- minimal base OS
- app code
- dependencies
- runtime + config

Example from lecture:
- `python:3.11-slim` (already has minimal Linux + Python 3.11)

### Image layers (why downloads are fast)
Images are made of **layers**.
Each Dockerfile instruction creates a new layer.

Benefits of layers:
- Faster builds (cache)
- Smaller storage (layers are shared)
- Faster pulls (only missing layers download)

---

## 6) Image registry + Docker Hub (store and share images)

An **image registry** is like a central store for images.

In DevOps, registry is like:
- GitHub = for source code
- Registry = for container images

### Public vs private registries

**Public registry:** anyone can pull images (often free)

**Private registry:** company-only access
Examples: AWS ECR, Azure ACR, GitHub Container Registry (GHCR)

### Image naming format

`<registry>/<namespace>/<image>:<tag>`

Example:

`docker.io/manpreet/webapp:v1`

### Tags (versions)
Tags identify versions: `v1`, `v2`, `latest`, `1.0.3`, etc.

### Push vs pull (distribution flow)

Typical flow:
1) Developer builds image locally
2) Push image to registry
3) Server pulls image
4) Container runs from image

---

## 7) Docker architecture (who does what)

Main components:
- **Docker Client**: where you type commands (`docker run ...`)
- **Docker Daemon**: background service that builds/runs containers
- **Images**: blueprints
- **Containers**: running instances
- **Registry**: Docker Hub or private registry

**Simple understanding:**
Client asks → Daemon does the work → pulls/pushes from Registry.

---

## 8) Docker lifecycle (Build → Ship → Run)

Stages:
- **Build**: create an image
- **Ship**: push/pull via registry
- **Run**: start containers from images

Common container states:
- Created
- Running
- Paused
- Stopped

---

## 9) Docker commands you must practice (with meaning)

### A) Basic “Quick Start” commands

```bash
docker pull ubuntu
docker images
docker run ubuntu
docker run -it ubuntu /bin/bash
docker stop <container_id>
docker rm <container_id>
docker rmi ubuntu
docker system prune -a
docker system prune -a --volumes
```

What they do (simple):
- `pull` downloads an image
- `images` shows downloaded images
- `run` creates + starts a container
- `-it` gives you an interactive terminal
- `stop` stops a running container
- `rm` removes a container
- `rmi` removes an image
- `system prune` cleans unused stuff (careful)

⚠️ **Warning:** `docker system prune -a --volumes` can delete volumes (your saved data). Use only when you really want a clean system.

### B) Run an Nginx website container (classic demo)

```bash
docker pull nginx
docker run -d -p 8080:80 --name mynginx nginx
docker ps
docker stop mynginx
docker start mynginx
docker rm -f mynginx
docker rmi nginx
```

How it works:
- `-d` runs in background (detached)
- `-p 8080:80` maps **host port 8080** → **container port 80**
- `--name mynginx` gives an easy name

**Real-life example:**
Port mapping is like a building’s main gate number (host port) forwarding visitors to a flat door number (container port).

### C) Container interaction (debugging commands)

```bash
docker exec -it <container_id_or_name> bash
docker logs <container_id_or_name>
docker inspect <container_id_or_name>
docker stats
docker top <container_id_or_name>
```

Use cases:
- `exec` = go inside the running container
- `logs` = see app output
- `inspect` = full config (JSON)
- `stats` = live CPU/RAM usage
- `top` = processes inside the container

Example from lecture:

```bash
docker run -dit --name myubuntu ubuntu
docker exec -it myubuntu bash
```

### D) Volumes (persistent storage)

Volumes keep data safe even if the container is deleted.

```bash
docker volume create myvolume
docker volume ls
docker volume inspect myvolume
docker volume rm myvolume
```

**Real-life example:**
Container is a rented room, volume is your personal locker. You can change rooms, but locker data stays.

### E) Networks (containers discover each other)

Containers can be isolated but still communicate using Docker networks.

```bash
docker network ls
docker network create mynetwork
docker network inspect mynetwork
docker network rm mynetwork
```

### F) Cleanup commands (when your system is messy)

```bash
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
docker rmi $(docker images -q)
docker system prune -a
```

---

## 10) Practice tasks (from lecture)

### Task 1: Practice Linux commands inside Docker (Ubuntu interactive)

```bash
docker run -it ubuntu bash
exit
```

### Task 2: Troubleshoot a running container

```bash
docker exec -it <container_id_or_name> bash
docker logs <container_id_or_name>
docker top <container_id_or_name>
```

### Task 3: Create and verify a custom network

```bash
docker network create mynetwork
docker network ls
docker network inspect mynetwork
```

### Task 4: Deploy Apache (httpd) for a static website

Goal: run Apache in detached mode, map host `8081` → container `80`.

```bash
docker pull httpd
docker images
docker run -d --name apache-web -p 8081:80 httpd
docker ps
```

Open your browser:
- `http://localhost:8081`

---

## 11) Quick quiz (from lecture)

1) Primary purpose of an image registry?
- A) Execute containers
- B) Store and distribute container images
- C) Build container images
- D) Monitor performance

2) Which part of an image name tells the version?
- A) Registry
- B) Namespace
- C) Image name
- D) Tag

3) Which registry type is common in enterprises?
- A) Public
- B) Open
- C) Private
- D) Anonymous

4) In CI/CD, registry mainly acts as:
- A) Source code repo
- B) Testing environment
- C) Bridge between CI and CD
- D) Container runtime

---

## Summary (one page)

- VMs are heavy; containers are lightweight and fast.
- Containers use **namespaces** (isolation) and **cgroups** (limits).
- Image = blueprint, container = running instance.
- Registry (like Docker Hub) stores and shares images.
- Learn these commands first: `pull`, `images`, `run`, `ps`, `stop`, `rm`, `rmi`, `exec`, `logs`, `inspect`, `stats`, `volume`, `network`, `system prune`.