# 🐳 Unit 2.1 — Basic Docker Commands

These are the commands we use daily to work with images and containers.

---

## 1) Docker version + info

```bash
docker --version
docker info
```

---

## 2) Images (pull, list, inspect)

### Pull image from Docker Hub

```bash
docker pull httpd
docker pull nginx
docker pull ubuntu
```

### List images

```bash
docker images
# same:
docker image ls
```

### Check image history (layers)

```bash
docker history httpd
docker history --no-trunc nginx
```

### Inspect image details

```bash
docker image inspect nginx
```

---

## 3) Containers (run, ps, exec)

### Run a container
Syntax:

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

Common options:
- `-it` interactive
- `-d` background
- `--name` container name
- `--rm` auto delete after exit

Examples:

```bash
# simple run
docker run --rm ubuntu echo "Hello, World!"

# run container in background
docker run -d --name web nginx

# interactive container
docker run -it --rm ubuntu bash

# named container example
docker run --name my-container httpd
```

### What is running?

```bash
docker ps
```

### All containers (running + stopped)

```bash
docker ps -a
```

### Exec (enter container and run commands)

```bash
# shell inside container (nginx uses sh)
docker exec -it web sh

# if image has bash
docker exec -it my-container bash
```

---

## 4) Container lifecycle

```bash
# start a stopped container
docker start web

# stop a running container
docker stop web

# restart
docker restart web

# pause/unpause
docker pause web
docker unpause web
```

---

## 5) Logs + inspect (basic troubleshooting)

```bash
docker logs web
docker logs -f web

docker inspect web
```

---

## 6) Remove containers and images

### Remove container

```bash
# remove stopped container
docker rm web

# force remove (stops if running)
docker rm -f web
```

### Remove image

```bash
docker rmi httpd

# force remove
docker rmi -f <image_id>
```

---

## 7) Quick cleanup (use carefully)

```bash
# remove stopped containers
docker container prune

# remove unused images
docker image prune

# remove unused volumes (be careful)
docker volume prune

# overall cleanup (be careful)
docker system prune
```
