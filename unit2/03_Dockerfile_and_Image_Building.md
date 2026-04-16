# 🧱 Unit 2.3 — Dockerfile + Image Building

This section is about **how to create your own image**.

---

## 1) Core concepts (image layering)

Docker images are made of **layers**.
- Each layer is cached
- If nothing changes, Docker reuses old layers (fast builds)

Commands to see layers:

```bash
docker history nginx
docker image inspect nginx
```

---

## 2) Build context + `.dockerignore`

### Build context
When you run `docker build .`, the `.` is the **build context**.
That means Docker can only `COPY` files that are inside this folder.

### `.dockerignore`
It tells Docker what to skip sending in the build context.

Example `.dockerignore`:

```dockerignore
.git
node_modules
*.log
.env
__pycache__
venv
.venv
```

---

## 3) Dockerfile basic instructions

### Most used instructions
- `FROM` base image
- `RUN` run command while building
- `COPY` copy files from context to image
- `ADD` like COPY + extra features (tar extract / URL). Normally prefer `COPY`.
- `WORKDIR` set working directory
- `ENV` set env variables in image
- `EXPOSE` documents the port used by the app
- `CMD` default command (easy to override)
- `ENTRYPOINT` main command (container behaves like an executable)
- `VOLUME` declare mount point for persistent data

---

## 4) Example Dockerfile (simple nginx site)

Create `Dockerfile`:

```dockerfile
FROM nginx:alpine
WORKDIR /usr/share/nginx/html
COPY index.html .
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

Create `index.html`:

```html
<h1>Hello from Unit 2</h1>
```

Build + run:

```bash
docker build -t my-web:1.0 .
docker run -d --name my-web -p 8080:80 my-web:1.0
```

---

## 5) `docker build` process (in detail)

When we run:

```bash
docker build -t myapp:1.0 .
```

Docker does:
1. Sends build context
2. Reads Dockerfile top-to-bottom
3. Builds layers (uses cache)
4. Creates final image

Useful flags:

```bash
# detailed output
docker build --progress=plain -t myapp:1.0 .

# force rebuild
docker build --no-cache -t myapp:1.0 .

# different Dockerfile name
docker build -f Dockerfile.prod -t myapp:prod .
```

---

## 6) Tagging / versioning

```bash
# tag at build
docker build -t myapp:1.0 .

# add another tag
docker tag myapp:1.0 myapp:latest

docker images
```

Good habit: use proper versions like `1.0`, `1.1`, `2026-04-03`.

---

## 7) `CMD` vs `ENTRYPOINT` (simple)

- `CMD` = default command, can be replaced
- `ENTRYPOINT` = fixed main command

Override CMD example:

```bash
docker run --rm ubuntu echo "override"
```

Override ENTRYPOINT (when needed):

```bash
docker run --entrypoint sh -it myimage
```
