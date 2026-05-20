# Java Maven CI using GitHub Actions

## What is Java Maven CI?

Java Maven CI uses **GitHub Actions** to automate Java application build and testing.

Continuous Integration (CI) automatically:

- builds Java project
- installs dependencies
- runs tests
- creates build artifacts

whenever code changes are pushed to GitHub.

---

# Why Use Maven in CI?

Maven helps automate:

- dependency management
- project compilation
- testing
- packaging

Common Maven commands:

```bash
mvn clean install
mvn test
```

---

# Java CI Workflow Components

A Java Maven workflow usually contains:

1. Checkout Repository
2. Setup JDK
3. Cache Maven Dependencies
4. Build Application
5. Run Tests
6. Upload Build Artifacts

These steps are commonly used in CI pipelines. :contentReference[oaicite:1]{index=1}

---

# Example Workflow

Example `ci.yml`:

```yaml
name: Java CI with Maven

on:
  push:
    branches:
      - main

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          java-version: '21'
          distribution: 'temurin'

      - name: Build Project
        run: mvn clean install
```

---

# Setup Java Step

GitHub Actions uses:

```yaml
actions/setup-java
```

Example:

```yaml
uses: actions/setup-java@v4
```

Purpose:

- install JDK
- configure Java environment

---

# Maven Build Step

Command:

```bash
mvn clean install
```

Purpose:

- clean old builds
- download dependencies
- compile source code
- execute tests
- package application

---

# Run Tests

Command:

```bash
mvn test
```

Purpose:

Executes unit tests.

---

# Upload Artifacts

GitHub Actions can store build outputs.

Action:

```yaml
actions/upload-artifact
```

Example:

```yaml
- name: Upload Artifact
  uses: actions/upload-artifact@v4
```

---

# Advantages

- Automated Java builds
- Faster testing
- Consistent CI process
- Dependency automation
- Artifact storage

---

# Important Viva Questions

## What is Java Maven CI?

Automated Java build and testing pipeline using Maven and GitHub Actions.

---

## Which action installs Java?

```yaml
actions/setup-java
```

---

## Which Maven command executes tests?

```bash
mvn test
```

---

## What does `mvn clean install` do?

Compiles, tests, packages, and installs project.

---

## What is artifact upload?

Saving generated build files for later download or deployment.

---

# Conclusion

Java Maven CI automates Java project building, testing, and artifact generation using GitHub Actions workflows.