# Monolithic vs Microservices

## Introduction

Software architecture has evolved significantly over time:

- 1980s–1990s → Monolithic applications on physical servers
- 2000s → N-tier applications with virtualization
- Present → Microservices running in containers using Docker and Kubernetes

Microservices architecture became popular because modern applications require scalability, flexibility, and faster deployment.

---

# Monolithic Architecture

A monolithic application is built as a single unified application where all components are tightly coupled.

It mainly contains:
- User Interface (UI)
- Business Logic
- Database Access Layer

All modules are developed and deployed together.

---

## Example of Monolithic Application

An E-commerce application where:
- Frontend
- Backend
- Authentication
- Payment
- Database

are combined into one large application.

---

# Advantages of Monolithic Architecture

- Simple deployment
- Easy debugging and testing
- Faster internal communication
- Suitable for small applications

---

# Disadvantages of Monolithic Architecture

- Difficult to scale specific modules
- Large codebase becomes hard to manage
- Technology upgrades become difficult
- One failure can affect entire application
- Slower development for large teams

---

# Microservices Architecture

Microservices architecture divides an application into multiple small independent services.

Each service:
- Performs a specific business task
- Runs independently
- Communicates using APIs
- Can use its own database

---

## Example of Microservices

An online shopping platform may contain:
- User Service
- Product Service
- Payment Service
- Order Service
- Recommendation Service

Each service works independently.

---

# Advantages of Microservices

| Advantage | Description |
|---|---|
| Scalability | Services can scale independently |
| Independent Deployment | Update one service without affecting others |
| Fault Isolation | Failure in one service does not stop entire system |
| Technology Flexibility | Different technologies can be used |
| Faster Development | Teams can work independently |
| Easier Maintenance | Small services are easier to manage |

---

# Disadvantages of Microservices

- Complex architecture
- Difficult service communication
- More deployment management
- Monitoring becomes challenging
- Requires container orchestration tools

---

# Monolithic vs Microservices

| Feature | Monolithic | Microservices |
|---|---|---|
| Architecture | Single application | Multiple independent services |
| Scalability | Entire app scaled together | Individual services scaled |
| Deployment | Single deployment | Independent deployment |
| Fault Isolation | Low | High |
| Flexibility | Less flexible | Highly flexible |
| Maintenance | Difficult for large apps | Easier due to smaller services |
| Technology Stack | Usually single stack | Multiple stacks possible |

---

# Role of Containers in Microservices

Microservices are commonly deployed using containers such as Docker.

Benefits:
- Lightweight deployment
- Faster startup time
- Isolation between services
- Better resource utilization
- Easy scalability

Kubernetes is often used to manage multiple containers.

---

# Real-World Examples

- Netflix
- Amazon
- Flipkart
- Swiggy
- Zomato

These platforms use microservices to handle millions of users efficiently.

---

# Important Viva Questions

## 1. What is a monolithic application?
A monolithic application is a single unified application where all components are tightly coupled and deployed together.

---

## 2. What are microservices?
Microservices are small independent services that work together to form an application.

---

## 3. Why are microservices preferred over monolithic architecture?
Because they provide scalability, flexibility, independent deployment, and fault isolation.

---

## 4. What is fault isolation in microservices?
Failure of one service does not affect the complete application.

---

## 5. Why are containers used in microservices?
Containers provide lightweight, isolated, and portable environments for running services.

---

# Conclusion

Monolithic architecture is simple and suitable for small applications, while microservices architecture is better for large-scale modern applications requiring scalability, flexibility, and faster deployment.
