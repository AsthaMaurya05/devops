# Containers

## Introduction

Containers are lightweight virtualization technologies that allow multiple isolated applications to run on a single operating system.

Containers package:
- Application code
- Dependencies
- Libraries
- Runtime environment

This makes applications portable and consistent across different systems.

---

# What is a Container?

A container is an isolated environment that shares the host operating system kernel while running applications independently.

Containers are widely used in DevOps and cloud computing because they are:
- Lightweight
- Fast
- Portable
- Scalable

---

# Features of Containers

- OS-level virtualization
- Lightweight compared to Virtual Machines
- Fast startup time
- Efficient resource utilization
- Portable across environments
- Isolation between applications

---

# Containers vs Virtual Machines

| Feature | Containers | Virtual Machines |
|---|---|---|
| Virtualization Type | OS-level virtualization | Hardware-level virtualization |
| Size | Lightweight | Heavy |
| Startup Time | Seconds | Minutes |
| Resource Usage | Low | High |
| OS Requirement | Shares host kernel | Separate guest OS |
| Performance | Faster | Slower compared to containers |

---

# Working of Containers

Containers use:
- Namespaces → for process isolation
- Control Groups (cgroups) → for resource limits
- Container Runtime → to run containers

The host operating system kernel is shared among all containers.

---

# Advantages of Containers

- Faster deployment
- Better resource utilization
- Easy scalability
- Consistent development environment
- Simplified application deployment
- High portability

---

# Containers and Microservices

Containers are commonly used to deploy microservices.

Each microservice can run inside its own container with:
- Required dependencies
- Runtime environment
- Libraries

Benefits:
- Independent deployment
- Fault isolation
- Better scalability
- Faster updates

---

# Docker and Kubernetes

## Docker
Docker is a containerization platform used to:
- Build containers
- Run containers
- Manage container images

---

## Kubernetes
Kubernetes is a container orchestration tool used to:
- Manage multiple containers
- Auto-scale applications
- Self-heal failed containers
- Handle container networking

---

# Real-World Uses of Containers

Containers are widely used in:
- Cloud applications
- CI/CD pipelines
- Microservices architecture
- DevOps automation
- Scalable web applications

Companies using containers:
- Netflix
- Amazon
- Google
- Spotify

---

# Important Viva Questions

## 1. What is a container?
A container is a lightweight isolated environment used to run applications along with their dependencies.

---

## 2. Why are containers lightweight?
Because they share the host operating system kernel instead of running a separate OS.

---

## 3. What is the difference between containers and VMs?
Containers share the host OS kernel while VMs use separate guest operating systems.

---

## 4. What is Docker?
Docker is a platform used for containerization.

---

## 5. What is Kubernetes?
Kubernetes is a container orchestration platform used to manage multiple containers.

---

## 6. Why are containers useful in microservices?
Containers provide portability, scalability, and isolation for microservices deployment.

---

# Conclusion

Containers provide lightweight, fast, and portable application deployment environments. They are a core technology in modern DevOps and microservices architecture.

