# Introduction to GitHub Actions

## What is GitHub Actions?

GitHub Actions is a **CI/CD (Continuous Integration / Continuous Deployment)** platform provided by GitHub.

It helps automate software workflows directly inside a GitHub repository.

Using GitHub Actions, developers can:

- Build applications
- Run tests
- Deploy applications
- Automate repetitive tasks

GitHub Actions workflows are written using **YAML files**. :contentReference[oaicite:0]{index=0}

---

# What is CI/CD?

## Continuous Integration (CI)

Continuous Integration means automatically:

- building code
- testing code
- validating changes

whenever developers push code.

Example:

Developer pushes code → automatic build → automatic tests.

---

## Continuous Deployment (CD)

Continuous Deployment means automatically deploying applications after successful build and testing.

Example:

Code Push → Build → Test → Deploy.

---

# Why Use GitHub Actions?

Advantages:

- Integrated with GitHub
- Supports CI/CD automation
- Easy workflow configuration
- Supports Docker, Maven, NodeJS, Python, Java
- Cross-platform runners

---

# Workflow Automation

A workflow is an automated process.

Workflow files are:

- written in YAML
- stored inside:

```text
.github/workflows/
```

A workflow contains:

- Events
- Jobs
- Steps
- Actions

Example structure from lecture notes: :contentReference[oaicite:1]{index=1}

```yaml
name: My First Workflow

on: push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Run Script
        run: echo "Hello World"
```

---

# Components of GitHub Actions

## 1. Events

Events decide **when workflow starts**.

Examples:

- push
- pull_request
- schedule
- workflow_dispatch

---

## 2. Jobs

Jobs define **what work will be done**.

A workflow may contain multiple jobs.

Jobs run in parallel by default.

Example:

```yaml
jobs:
  build:
  test:
```

---

## 3. Steps

Steps define **how a job executes**.

Each job contains sequential steps.

Example:

```yaml
steps:
  - name: Hello
    run: echo "Hello World"
```

---

## 4. Actions

Actions are reusable workflow components.

Example:

```yaml
uses: actions/checkout@v4
```

---

## 5. Runners

Runners execute workflows.

Types:

- GitHub-hosted runners
- Self-hosted runners

GitHub supports:

- Ubuntu
- Windows
- macOS :contentReference[oaicite:2]{index=2}

---

# Basic Workflow Example

```yaml
name: First CI Workflow

on: push

jobs:
  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - name: Print Message
        run: echo "GitHub Actions Working Successfully"
```

---

# Important Viva Questions

## What is GitHub Actions?

GitHub Actions is a CI/CD automation platform integrated with GitHub.

---

## Where are workflow files stored?

```text
.github/workflows/
```

---

## Which language is used to define workflows?

YAML.

---

## What is a runner?

A server that executes GitHub Actions workflows.

---

## Difference between CI and CD?

CI → automatic build/testing.

CD → automatic deployment.

---

# Conclusion

GitHub Actions automates software workflows using YAML-based pipelines and supports CI/CD directly inside GitHub repositories.

