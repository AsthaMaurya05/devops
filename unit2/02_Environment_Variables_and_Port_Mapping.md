# 🌍 Unit 2.2 — Environment Variables + Port Mapping

This part is important because most real containers need **config** and **network access**.

---

## 1) Environment variables (`-e`)

Environment variables are **key=value** settings used by apps.

Why we use them:
- Same image can behave differently without rebuilding
- Easy to pass configs at runtime

### Set one variable

```bash
docker run --rm -e MY_VAR=value ubuntu env
```

### Interactive example

```bash
docker run -it --rm -e MY_NAME=Harpreet ubuntu bash
# inside container:
echo $MY_NAME
```

### Multiple variables

```bash
docker run --rm -e APP_ENV=production -e APP_VERSION=1.0 nginx env
```

### Pass variables using `--env-file`
Create `.env` file:

```bash
# .env
DB_HOST=localhost
DB_USER=root
DB_PASS=secret
```

Run:

```bash
docker run --rm --env-file .env ubuntu env
```

---

## 2) Port mapping (`-p`)

Without port mapping, the container app is usually not reachable from browser.

### Syntax

```bash
docker run -p <HOST_PORT>:<CONTAINER_PORT> IMAGE
```

### Nginx example

```bash
docker run -d --name nginx-web -p 8080:80 nginx
```

Flow in simple words:
`Browser -> localhost:8080 -> Docker host -> container:80`

### MySQL example (host port different)

```bash
docker run -d --name mysql-test -p 3307:3306 -e MYSQL_ROOT_PASSWORD=root123 mysql:8

# enter container
docker exec -it mysql-test bash
```

---

## 3) Quick small demo (httpd page update)

```bash
docker pull httpd

docker run -d --name my-apache -p 8080:80 httpd

docker exec -it my-apache bash -c "echo '<h1>Hello from Docker Apache!</h1>' > /usr/local/apache2/htdocs/index.html"

# check in terminal
curl http://localhost:8080

# stop + remove
docker stop my-apache
docker rm my-apache
```
