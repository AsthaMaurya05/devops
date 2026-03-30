# 📦 Container Fundamentals (Hands-on with Docker)

These notes focus on **how containers work under the hood**, but explained in **easy language** with **Docker commands you can actually run**.

---

## 1) Container runtime (what runs the container)

You already know:
- **Image** = blueprint (read-only)
- **Container** = running instance of that blueprint

To turn an image into a running container, the system uses a **container runtime**.

> Container runtime = software that creates/starts/stops containers.

In Docker, you mostly interact with **Docker Engine**, which uses low-level runtime components behind the scenes.

**Real-life example:**
Image is like a packed lunchbox. Runtime is the person who opens it and serves the food.

---

## 2) Namespaces (isolation) — “separate cabins in the same train”

Containers are isolated, even though they share the same host kernel.

> Namespaces create the illusion that each container has its own machine.

### A) PID namespace (process isolation)

Run a container and check processes:

```bash
docker run -dit --name demo-pid ubuntu
docker exec demo-pid cat /proc/1/comm
docker top demo-pid
```

What you’ll notice:
- Inside the container, the “main” process looks like it starts from PID 1.
- The container cannot see the host’s full process list.

Useful commands for process view:

```bash
docker top demo-pid
docker inspect demo-pid
```

### B) Network namespace (network isolation)

Containers can run services on the same internal port without conflict because each container has its own network namespace.

Example (many containers can listen on port 80 internally):

```bash
docker run -d --name web1 nginx
docker run -d --name web2 nginx
docker ps
```

If you want to access from your laptop browser, you map host ports:

```bash
docker run -d --name web-8080 -p 8080:80 nginx
docker run -d --name web-8082 -p 8082:80 nginx
```

**Real-life example:**
Host port is the building’s main gate number; container port is the flat’s door number.

### C) Mount namespace (filesystem isolation)

Each container has its own filesystem view.

Try this:

```bash
docker run -it --rm ubuntu bash
echo "hello" > /tmp/inside-container.txt
cat /tmp/inside-container.txt
exit
```

When the container is removed, that file is gone (unless you used a volume/bind mount).

### D) UTS namespace (hostname)

```bash
docker run -it --rm --hostname mycontainer ubuntu hostname
```

---

## 3) cgroups (resource limits) — “apartment electricity meter”

Namespaces isolate.

> cgroups control resources so one container cannot eat all CPU/RAM.

### Common limits you can set with Docker

```bash
docker run -d --name limited --memory 512m --cpus 1.0 --pids-limit 100 nginx
```

Check live usage:

```bash
docker stats
```

**Real-life example:**
In an apartment building, one tenant can’t use all electricity because each flat has a meter/limit.

---

## 4) Images and layers (why builds/pulls are fast)

### Image layers
Images are built in layers.

Layer benefits:
- Faster builds (cache)
- Less storage (layers are shared)
- Faster pulls (only missing layers download)

Useful commands:

```bash
docker images
docker history nginx
docker inspect nginx
```

**Real-life example:**
Layers are like stacking LEGO blocks. If only the top block changes, you don’t rebuild the whole model.

---

## 5) Registries (Docker Hub / private registries)

A registry stores and distributes images.

**Naming format:**

`<registry>/<namespace>/<image>:<tag>`

Example:

`docker.io/library/nginx:latest`

Core commands:

```bash
docker login
docker pull nginx
docker tag myapp:1.0 username/myapp:1.0
docker push username/myapp:1.0
```

---

## 6) Lecture practice tasks (answers included)

### Task 1 (memory crash scenario)

Scenario: One faulty container crashes host due to high memory usage.

Answers:
- Missing/misconfigured feature: **resource limits**
- Kernel mechanism that should prevent it: **cgroups**
- Would namespaces alone solve it? **No** — namespaces isolate visibility, but they don’t limit RAM usage.

### Task 2 (three containers on one server)

Scenario:
- Container A = CPU heavy
- Container B = web server
- Container C = database

Answers:
- Prevent A from consuming all CPU: **cgroups** (Docker flags like `--cpus`)
- Ensure B can’t see C’s processes: **PID namespace**
- Allow all to use port 80 internally: **Network namespace**

---

## Summary

- **Namespaces** = isolation (process/network/filesystem/hostname)
- **cgroups** = resource limits (CPU/RAM/process count)
- **Image layers** = faster builds + less storage
- **Registry** = store/share images (Docker Hub / private)
