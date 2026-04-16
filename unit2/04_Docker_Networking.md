# 🌐 Unit 2.4 — Docker Networking

Docker networking decides how containers talk to each other and how we access them from host.

---

## 1) Bridge network (default)

Bridge is the default network on a single machine.

```bash
docker network ls
docker network inspect bridge
```

### User-defined bridge (recommended)
On a user-defined bridge, Docker provides **DNS by container name**.

```bash
docker network create my-bridge

docker run -d --name web --network my-bridge nginx

docker run -it --rm --network my-bridge alpine sh
# inside alpine:
apk add --no-cache bind-tools
nslookup web
```

---

## 2) DNS inside Docker

Simple rule:
- Same user-defined network = containers can reach each other by name.

Example idea:
- `web` container can be reached using hostname `web` from another container on same network.

---

## 3) Linking containers (`--link`) (old way)

`--link` is legacy (not recommended now), but you may still see it.

```bash
docker run -d --name db mysql:8 -e MYSQL_ROOT_PASSWORD=root123

docker run -it --rm --link db:mysql ubuntu bash
```

---

## 4) Port mapping (host <-> container)

```bash
docker run -d --name nginx-web -p 8080:80 nginx
```

This is how browser reaches a container app.

---

## 5) Host network

Container uses the host network directly.

```bash
# mostly useful on Linux
docker run --network host nginx
```

Note: On Docker Desktop (Windows/Mac), host networking can behave differently.

---

## 6) Overlay network (multi-host)

Overlay is used for multi-machine container networking (commonly with Swarm).

```bash
docker swarm init

docker network create -d overlay my-overlay
```
