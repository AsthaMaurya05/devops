# Practical 01 — Docker + GitHub Actions CI/CD Pipeline

## Aim

To create a Dockerized Python Flask application and automate its build process using GitHub Actions Continuous Integration (CI).

---

## Problem Statement

Build a simple Flask application using Docker and configure GitHub Actions workflow to automatically build the Docker image whenever code is pushed to GitHub repository.

---

## Solution

### Step 1 — Create Flask Application

Created a simple Python Flask web application.

**app.py**

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Docker CI/CD!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)
```

---

### Step 2 — Create Requirements File

**requirements.txt**

```txt
Flask
```

---

### Step 3 — Create Dockerfile

Created Dockerfile for containerizing the Flask application.

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python","app.py"]
```

---

### Step 4 — Build Docker Image

Command used:

```bash
docker build --no-cache -t my-docker-app .
```

---

### Step 5 — Run Docker Container

Command used:

```bash
docker run -p 5000:5000 my-docker-app
```

Output:

```text
Running on http://127.0.0.1:5000
```

Browser Output:

```text
Hello from Docker CI/CD!
```

---

### Step 6 — Create GitHub Actions Workflow

Created workflow file:

```text
.github/workflows/ci-cd.yml
```

Workflow automatically runs on every push to GitHub.

**ci-cd.yml**

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
```

---

### Step 7 — Push Project to GitHub

Commands used:

```bash
git init
git add .
git commit -m "Add Docker GitHub Actions workflow"
git branch -M main
git remote add origin https://github.com/AsthaMaurya05/my-docker-app.git
git push -u origin main
```

---

### Step 8 — Verify GitHub Actions Workflow

After pushing code:

- Workflow triggered automatically.
- GitHub Actions pipeline executed successfully.
- Docker image build completed successfully.

---

## Screenshots

### Project Structure

![Project Structure](screenshots/folder-structure.png)

### VS Code Project

![VSCode Project](screenshots/vscode-project.png)

### Docker Build

![Docker Build](screenshots/docker-build.png)

### Docker Run

![Docker Run](screenshots/docker-run.png)

### Browser Output

![Browser Output](screenshots/browser-output.png)

### Git Push

![Git Push](screenshots/git-push.png)

### Workflow Triggered

![Workflow Triggered](screenshots/workflow-triggered.png)

### Workflow Success

![Workflow Success](screenshots/workflow-success.png)

### Build Logs

![Build Logs](screenshots/build-logs.png)

---

## Result

Successfully built and containerized a Flask application using Docker and automated the Docker image build process using GitHub Actions CI/CD workflow.
