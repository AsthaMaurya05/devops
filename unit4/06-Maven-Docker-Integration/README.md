# Maven Docker Integration

## Overview

This module demonstrates how to integrate Maven with Docker to build, package, and deploy Java applications in containers.

## Integration Approaches

### 1. Building Docker Image from Maven Build
Use Maven to compile and package the application, then Docker to containerize it.

### 2. Maven Plugin for Docker
Use plugins like Spotify Docker Maven Plugin or Jib to build Docker images directly from Maven.

### 3. Multi-stage Docker Builds
Optimize Docker images by building in one container and running in another.

## Spotify Docker Maven Plugin

Configuration in pom.xml:

```xml
<plugin>
  <groupId>com.spotify</groupId>
  <artifactId>docker-maven-plugin</artifactId>
  <version>1.2.2</version>
  <configuration>
    <imageName>myapp:${project.version}</imageName>
    <baseImage>java:8</baseImage>
    <entryPoint>["java", "-jar", "/${project.build.finalName}.jar"]</entryPoint>
    <resources>
      <resource>
        <targetPath>/</targetPath>
        <directory>${project.build.directory}</directory>
        <include>${project.build.finalName}.jar</include>
      </resource>
    </resources>
  </configuration>
</plugin>
```

## Google Jib

Containerize Java applications without Docker daemon:

```xml
<plugin>
  <groupId>com.google.cloud.tools</groupId>
  <artifactId>jib-maven-plugin</artifactId>
  <version>3.1.0</version>
  <configuration>
    <to>
      <image>myregistry/myapp:${project.version}</image>
    </to>
  </configuration>
</plugin>
```

## Dockerfile Best Practices

- Use official base images
- Minimize layer count
- Use .dockerignore
- Run as non-root user
- Set proper environment variables

## Maven Build and Docker

Typical workflow:

1. `mvn clean package` - Build JAR/WAR
2. `docker build -t myapp:1.0 .` - Build Docker image
3. `docker run -p 8080:8080 myapp:1.0` - Run container

## Multi-stage Docker Builds

```dockerfile
# Build stage
FROM maven:3.8 AS builder
WORKDIR /build
COPY pom.xml .
RUN mvn dependency:resolve
COPY src src
RUN mvn clean package -DskipTests

# Runtime stage
FROM openjdk:11-slim
COPY --from=builder /build/target/*.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]
```

## Maven Command Line Docker Build

```bash
mvn clean package docker:build    # Build Docker image
mvn clean package docker:push     # Push to registry
```

## Integration Benefits

- Consistent builds across environments
- Automated container creation
- Dependency management
- Version control
- Easy deployment
