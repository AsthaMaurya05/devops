# Practical 02 — Java Maven CI with GitHub Actions

## Aim

To automate Java Maven project build and testing using GitHub Actions CI pipeline.

---

# Tools & Technologies Used

- Java
- Maven
- GitHub Actions
- GitHub
- VS Code

---

# Project Structure

```text
java-ci-demo/
│
├── pom.xml
├── src/
├── .github/
│   └── workflows/
│       └── ci.yml
```

---

# Step 1 — Create Maven Project

Created Java Maven project manually with:

- `pom.xml`
- `App.java`
- `AppTest.java`

---

# Step 2 — Configure GitHub Actions Workflow

Created workflow file:

```text
.github/workflows/ci.yml
```

Workflow performs:

- Checkout Repository
- Setup JDK 21
- Cache Maven Dependencies
- Build Project
- Run Tests
- Upload Artifact

---

# Step 3 — Build Project Locally

Command:

```bash
mvn clean install
```

Result:

```text
BUILD SUCCESS
```

---

# Step 4 — Run Tests

Command:

```bash
mvn test
```

Result:

```text
BUILD SUCCESS
```

---

# Step 5 — Push Project to GitHub

Commands used:

```bash
git init
git add .
git commit -m "Add Java Maven CI workflow"
git branch -M main
git remote add origin https://github.com/AsthaMaurya05/java-maven-ci-demo.git
git push -u origin main
```

---

# Step 6 — GitHub Actions Execution

GitHub Actions automatically triggered CI pipeline.

Pipeline stages:

- Checkout Repository
- Setup JDK
- Cache Maven Packages
- Build with Maven
- Run Tests
- Upload Artifact

---

# Output

- Maven build completed successfully.
- Tests executed successfully.
- GitHub Actions workflow executed successfully.
- Build artifact uploaded successfully.

---

# Conclusion

Successfully implemented Continuous Integration (CI) pipeline for Java Maven project using GitHub Actions.