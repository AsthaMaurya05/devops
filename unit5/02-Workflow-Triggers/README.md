# Workflow Triggers

## What are Workflow Triggers?

Workflow triggers decide **when a GitHub Actions workflow should run**.

Triggers are defined using the:

```yaml
on:
```

keyword inside workflow files. :contentReference[oaicite:0]{index=0}

---

# Common Workflow Triggers

## 1. Push Trigger

Runs workflow whenever code is pushed to repository.

Example:

```yaml
on:
  push:
```

Specific branch:

```yaml
on:
  push:
    branches:
      - main
```

Use case:

- automatic builds
- automatic testing
- CI pipelines

---

## 2. Pull Request Trigger

Runs workflow when a pull request is created or updated.

Example:

```yaml
on:
  pull_request:
```

Specific branch:

```yaml
on:
  pull_request:
    branches:
      - main
```

Use case:

- validate code before merging
- run tests on PRs

---

## 3. Schedule Trigger

Runs workflow automatically at scheduled times.

Uses **cron syntax**.

Example:

```yaml
on:
  schedule:
    - cron: '0 0 * * *'
```

Example meaning:

Runs every day at midnight.

Use case:

- backup jobs
- scheduled testing
- maintenance tasks

---

## 4. Manual Workflow Trigger

Allows workflows to be started manually.

Keyword:

```yaml
workflow_dispatch
```

Example:

```yaml
on:
  workflow_dispatch:
```

Use case:

- manual deployments
- on-demand builds
- debugging pipelines

---

# Multiple Triggers

GitHub Actions supports multiple triggers.

Example:

```yaml
on:
  push:
    branches:
      - main

  pull_request:
    branches:
      - main
```

Workflow runs for:

- push events
- pull request events

---

# Trigger Example

```yaml
name: CI Workflow

on:
  push:
    branches:
      - main

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - name: Hello
        run: echo "Workflow Triggered Successfully"
```

---

# Trigger Use Cases

| Trigger | Purpose |
|----------|----------|
| push | Run build after code push |
| pull_request | Validate pull requests |
| schedule | Timed automation |
| workflow_dispatch | Manual execution |

---

# Important Viva Questions

## What is a workflow trigger?

An event that starts a GitHub Actions workflow.

---

## Which keyword defines triggers?

```yaml
on:
```

---

## Which trigger is used for manual execution?

```yaml
workflow_dispatch
```

---

## Which trigger uses cron expressions?

```yaml
schedule
```

---

## Which trigger runs after pushing code?

```yaml
push
```

---

# Conclusion

Workflow triggers control when GitHub Actions workflows execute using events such as push, pull_request, schedule, and manual execution.

