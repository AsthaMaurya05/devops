# Spring Boot + PostgreSQL using Docker Compose

## Introduction

Docker Compose is used to manage multi-container applications using a single YAML configuration file.

In this project:
- Spring Boot acts as backend application
- PostgreSQL acts as relational database

Both containers communicate using Docker networking.

---

# Services Used

## 1. Spring Boot Service

```yaml
springboot-app:
  image: eclipse-temurin:17
```

Provides Java runtime environment for Spring Boot applications.

---

## 2. PostgreSQL Service

```yaml
postgres-db:
  image: postgres:15
```

Provides PostgreSQL relational database server.

---

# Features Used

- Multi-container deployment
- Docker networking
- Environment variables
- Persistent storage
- Service dependency management

---

# Environment Variables

## Spring Boot Configuration

```yaml
SPRING_DATASOURCE_URL: jdbc:postgresql://postgres-db:5432/mydb
SPRING_DATASOURCE_USERNAME: postgres
SPRING_DATASOURCE_PASSWORD: postgres
```

Used to connect Spring Boot application with PostgreSQL database.

---

## PostgreSQL Configuration

```yaml
POSTGRES_DB: mydb
POSTGRES_USER: postgres
POSTGRES_PASSWORD: postgres
```

Used to configure PostgreSQL database.

---

# Docker Compose Networking

Docker Compose automatically creates internal networking.

Containers communicate using service names.

Example:

```text
postgres-db:5432
```

---

# Volumes

```yaml
volumes:
  - postgres-data:/var/lib/postgresql/data
```

Provides persistent PostgreSQL data storage.

---

# depends_on

```yaml
depends_on:
  - postgres-db
```

Ensures database starts before application container.

---

# Note

The browser shows `ERR_EMPTY_RESPONSE` because:
- Spring Boot container only contains Java runtime
- No actual Spring Boot web application is deployed
- PostgreSQL is a database service and not an HTTP web server

Containers are still running correctly.

---

# Advantages

- Easy deployment
- Simplified configuration
- Better portability
- Persistent storage
- Efficient multi-container management

---

# Important Viva Questions

## 1. Why is Docker Compose used?
Docker Compose is used to manage multi-container applications.

---

## 2. Why are environment variables used?
Environment variables are used to configure application and database settings dynamically.

---

## 3. What is the purpose of volumes?
Volumes provide persistent database storage.

---

## 4. How do containers communicate in Docker Compose?
Containers communicate using service names through Docker networking.

---

## 5. Why does the browser show ERR_EMPTY_RESPONSE?
Because no actual Spring Boot web application is deployed inside the Java runtime container.

---

# Conclusion

Docker Compose simplifies deployment and management of Spring Boot and PostgreSQL multi-container applications.