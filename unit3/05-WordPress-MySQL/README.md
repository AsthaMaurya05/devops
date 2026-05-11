# WordPress + MySQL using Docker Compose

## Introduction

Docker Compose is used to manage multi-container applications using a single YAML configuration file.

In this project:
- WordPress acts as frontend application
- MySQL acts as backend database

Both containers communicate through Docker networking.

---

# Services Used

## 1. WordPress Service

```yaml
wordpress:
  image: wordpress:latest
```

Runs WordPress web application.

---

## 2. MySQL Service

```yaml
db:
  image: mysql:5.7
```

Runs MySQL database server.

---

# Features Used

- Multi-container deployment
- Docker networking
- Environment variables
- Persistent volumes
- Service dependency management

---

# Environment Variables

## WordPress Configuration

```yaml
WORDPRESS_DB_HOST: db:3306
WORDPRESS_DB_USER: wpuser
WORDPRESS_DB_PASSWORD: wppass
WORDPRESS_DB_NAME: wpdb
```

Used to connect WordPress with MySQL database.

---

## MySQL Configuration

```yaml
MYSQL_DATABASE: wpdb
MYSQL_USER: wpuser
MYSQL_PASSWORD: wppass
MYSQL_ROOT_PASSWORD: rootpass
```

Used to configure MySQL database and credentials.

---

# Docker Compose Networking

Docker Compose automatically creates internal networking.

Containers communicate using:
- service names
- internal DNS

Example:

```text
db:3306
```

---

# Volumes

```yaml
volumes:
  - db-data:/var/lib/mysql
```

Provides persistent database storage.

---

# depends_on

```yaml
depends_on:
  - db
```

Ensures database container starts before WordPress container.

---

# Advantages

- Easy deployment
- Simplified configuration
- Better portability
- Persistent database storage
- Faster setup of web applications

---

# Important Viva Questions

## 1. Why is Docker Compose used?
Docker Compose is used to manage multi-container applications.

---

## 2. What is the role of environment variables?
Environment variables are used to configure services dynamically.

---

## 3. Why are volumes important?
Volumes provide persistent storage for database data.

---

## 4. How does WordPress connect to MySQL?
Using Docker internal networking and service names.

---

## 5. What is the purpose of depends_on?
It controls startup order between services.

---

# Conclusion

Docker Compose simplifies deployment and management of WordPress and MySQL multi-container applications.