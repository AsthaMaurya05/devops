# Docker GitHub Actions Integration

## What is Docker GitHub Actions Integration?

Docker can be integrated with GitHub Actions to automate:

- Docker image building
- Docker image testing
- Container execution
- CI/CD pipelines

Whenever code is pushed, GitHub Actions can automatically run Docker workflows. :contentReference[oaicite:0]{index=0}

---

# Workflow Objective

In this workflow:

1. Checkout repository code
2. Build Docker image
3. Verify image creation

This demonstrates a basic CI pipeline using Docker and GitHub Actions.

---

# Project Structure

Example structure:

```text
repository/
│
├── app.py
├── requirements.txt
├── Dockerfile
│
└── .github/
    └── workflows/
        └── ci-cd.yml
```

---

# Application File

Example Flask application:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Docker CI/CD!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

Example adapted from practical sheet. :contentReference[oaicite:1]{index=1}

---

# Dockerfile

Example Dockerfile:

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python","app.py"]
```

---

# GitHub Actions Workflow

Workflow file location:

```text
.github/workflows/ci-cd.yml
```

Example workflow:

```yaml
name: CI-CD Pipeline

on:
  push:
    branches:
      - main

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Build Docker Image
        run: docker build -t my-docker-app .

      - name: List Docker Images
        run: docker images
```

Adapted from practical document. :contentReference[oaicite:2]{index=2}

---

# Workflow Explanation

## Trigger

```yaml
on:
  push:
```

Runs workflow when code is pushed.

---

## Checkout Step

```yaml
uses: actions/checkout@v4
```

Downloads repository code.

---

## Docker Build Step

```yaml
docker build
```

Creates Docker image.

---

## Docker Images Step

```yaml
docker images
```

Lists available images.

---

# Advantages

- Automated builds
- Continuous integration
- Faster validation
- Docker workflow automation
- Better deployment readiness

---

# Important Viva Questions

## Why integrate Docker with GitHub Actions?

To automate Docker build and CI/CD pipelines.

---

## Which command builds Docker image?

```bash
docker build -t image-name .
```

---

## What does actions/checkout do?

Downloads repository source code.

---

## Where are workflow files stored?

```text
.github/workflows/
```

---

## Which event triggers this workflow?

```yaml
push
```

---

# Conclusion

Docker GitHub Actions integration automates container build workflows and supports continuous integration pipelines.

