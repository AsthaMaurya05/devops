# 💾 Unit 2.5 — Docker Storage (Volumes vs Bind Mounts)

Containers are replaceable, so important data should be stored outside container layer.

---

## 1) Volumes (recommended)

Docker manages the volume location.

```bash
# create volume
docker volume create mydata

docker volume ls
docker volume inspect mydata

# use volume
docker run -it --rm -v mydata:/data ubuntu bash
# inside container:
echo "hello" > /data/a.txt
cat /data/a.txt
```

---

## 2) Bind mounts (map your folder)

You control the exact host folder path.

Windows example:

```bash
mkdir C:\app\data

docker run -it --rm -v C:\app\data:/data ubuntu bash
# inside container:
echo "Hello this is my first program" > /data/test.txt
cat /data/test.txt

echo "Second line added" >> /data/test.txt
cat /data/test.txt
```

---

## 3) `--mount` (clean syntax)

```bash
# bind mount
docker run -it --rm --mount type=bind,source="C:\app\data",target=/data ubuntu bash

# volume
docker run -it --rm --mount type=volume,source=mydata,target=/data ubuntu bash
```

---

## 4) Backing data on host

- Volumes: stored in Docker’s internal storage location
- Bind mounts: stored exactly where you mapped

---

## 5) Copy-on-write (CoW) mechanism (simple)

Docker images are read-only layers.
Container gets a writable layer on top.
If a container changes a file from the image, Docker copies it to writable layer and edits it there.

Check storage driver:

```bash
docker info
```
