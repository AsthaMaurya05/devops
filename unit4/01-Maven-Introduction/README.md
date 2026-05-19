# Maven Introduction

## What is Maven?

Apache Maven is a build automation and project management tool primarily used for Java projects.

It helps developers:
- compile code
- manage dependencies
- run tests
- package applications
- deploy software

Maven uses a standard project structure and XML-based configuration file called `pom.xml`.

---

# Why Build Tools Are Needed

Before Maven, developers faced many problems:

- Manual compilation using `javac`
- Dependency conflicts
- Inconsistent builds
- Repetitive testing and packaging tasks

Maven automates all these tasks.

---

# Features of Maven

- Dependency management
- Build lifecycle management
- Plugin support
- Standard directory structure
- Project packaging
- Integration with CI/CD tools
- Docker integration

---

# Advantages of Maven

- Reduces manual work
- Simplifies dependency handling
- Ensures consistent builds
- Supports large projects
- Improves project maintainability

---

# Maven Architecture

Maven works using:
- POM (Project Object Model)
- Repositories
- Plugins
- Lifecycle phases

---

# Maven Repositories

## 1. Local Repository

Stored in:

```text
~/.m2/repository
```

Contains downloaded dependencies on local system.

---

## 2. Central Repository

Official Maven repository available online.

---

## 3. Remote Repository

Organization-specific repository shared across teams.

---

# Common Maven Commands

## Check Maven Version

```bash
mvn -version
```

---

## Compile Project

```bash
mvn compile
```

---

## Run Tests

```bash
mvn test
```

---

## Package Application

```bash
mvn package
```

---

## Install to Local Repository

```bash
mvn install
```

---

# Important Viva Questions

## 1. What is Maven?
Maven is a build automation and dependency management tool for Java projects.

---

## 2. What is the purpose of Maven?
To automate project build, dependency management, testing, and deployment.

---

## 3. What is POM in Maven?
POM stands for Project Object Model and is represented using `pom.xml`.

---

## 4. What are Maven repositories?
Repositories store project dependencies and build artifacts.

---

## 5. What is the default local Maven repository location?

```text
~/.m2/repository
```

---

# Conclusion

Maven simplifies Java project development through build automation, dependency management, and standardized project structure.