# 📦 Unit 2.6 — Registries (Docker Hub, GHCR, Private) + Authentication

A registry is where images are stored so we can pull/push them.

---

## 1) Docker Hub

Login:

```bash
docker login
```

Tag + push:

```bash
# build local
docker build -t myapp:1.0 .

# tag for Docker Hub (replace username)
docker tag myapp:1.0 <dockerhub_username>/myapp:1.0

# push
docker push <dockerhub_username>/myapp:1.0

# pull
docker pull <dockerhub_username>/myapp:1.0
```

---

## 2) GitHub Container Registry (GHCR)

Format:

`ghcr.io/<OWNER>/<IMAGE>:<TAG>`

Login with token (safe way):

```bash
# PowerShell
$env:GH_TOKEN = "<your_token_here>"
$env:GH_USER  = "<github_username_or_org>"
$env:GH_TOKEN | docker login ghcr.io -u $env:GH_USER --password-stdin
```

Build + push:

```bash
docker build -t ghcr.io/<OWNER>/myapp:1.0 .
docker push ghcr.io/<OWNER>/myapp:1.0

docker pull ghcr.io/<OWNER>/myapp:1.0
```

---

## 3) Private registry (local demo)

Run a registry container:

```bash
docker run -d --name registry -p 5000:5000 registry:2
```

Tag + push to it:

```bash
docker build -t myapp:1.0 .
docker tag myapp:1.0 localhost:5000/myapp:1.0

docker push localhost:5000/myapp:1.0

docker pull localhost:5000/myapp:1.0
```

---

## 4) Authentication & access tokens

### Docker Hub tokens
Instead of using your password everywhere, you can use an access token.

```bash
docker login
```

### GitHub token (PAT) for GHCR
Good habits:
- don’t write tokens in Dockerfile
- don’t commit tokens in `.env`
- prefer `--password-stdin` so it doesn’t show in history

```bash
$env:GH_TOKEN | docker login ghcr.io -u $env:GH_USER --password-stdin
```
