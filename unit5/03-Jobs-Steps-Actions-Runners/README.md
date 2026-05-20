# Jobs, Steps, Actions and Runners

## Key Components of GitHub Actions

GitHub Actions workflows are built using several important components:

- Jobs
- Steps
- Actions
- Runners

These components define how automation workflows execute. :contentReference[oaicite:0]{index=0}

---

# 1. Jobs

A **job** is a group of tasks executed inside a workflow.

Each workflow can contain one or multiple jobs.

Example:

```yaml
jobs:
  build:
  test:
```

Characteristics:

- Jobs run independently.
- Jobs run in parallel by default.
- Jobs can depend on other jobs.

---

## Job Example

```yaml
jobs:

  build:

    runs-on: ubuntu-latest

    steps:
      - run: echo "Building Application"
```

---

# Job Dependencies

Jobs can wait for another job using:

```yaml
needs:
```

Example:

```yaml
jobs:

  build:
    runs-on: ubuntu-latest

  deploy:
    needs: build
    runs-on: ubuntu-latest
```

Here:

- Build job executes first.
- Deploy job runs after build completes.

---

# 2. Steps

Steps define individual commands executed inside a job.

Each job contains one or more steps.

Example:

```yaml
steps:
  - name: Print Message
    run: echo "Hello GitHub Actions"
```

Characteristics:

- Steps run sequentially.
- Each step performs one task.
- Can use commands or reusable actions.

---

## Step Example

```yaml
steps:

  - name: Install Dependencies
    run: npm install

  - name: Run Tests
    run: npm test
```

---

# 3. Actions

Actions are reusable workflow components.

Instead of writing everything manually, predefined actions can be used.

Syntax:

```yaml
uses:
```

Example:

```yaml
uses: actions/checkout@v4
```

Popular actions:

| Action | Purpose |
|---------|----------|
| actions/checkout | Clone repository |
| actions/setup-java | Configure Java |
| actions/cache | Dependency caching |
| upload-artifact | Store build files |

---

## Example Action

```yaml
steps:

  - name: Checkout Code
    uses: actions/checkout@v4
```

Purpose:

Downloads repository source code.

---

# 4. Runners

Runners are machines that execute workflows.

Each job requires a runner.

Defined using:

```yaml
runs-on:
```

Example:

```yaml
runs-on: ubuntu-latest
```

---

## Types of Runners

### GitHub Hosted Runner

Managed by GitHub.

Supported environments:

- Ubuntu
- Windows
- macOS

Example:

```yaml
runs-on: ubuntu-latest
```

---

### Self Hosted Runner

Managed by user or organization.

Used for:

- custom hardware
- internal environments
- private infrastructure

---

# Complete Example

```yaml
name: Example Workflow

on:
  push:

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Print Message
        run: echo "Workflow Running Successfully"
```

---

# Important Viva Questions

## What is a job?

A group of tasks executed inside a workflow.

---

## What are steps?

Individual instructions executed inside a job.

---

## What is an action?

Reusable workflow component used inside steps.

---

## What does `actions/checkout@v4` do?

Clones repository code into workflow environment.

---

## What is a runner?

Machine that executes GitHub Actions workflows.

---

## Difference between GitHub-hosted and self-hosted runners?

GitHub-hosted → managed by GitHub.

Self-hosted → managed by user.

---

# Conclusion

Jobs, steps, actions, and runners are core building blocks of GitHub Actions workflows and together automate CI/CD pipelines.

