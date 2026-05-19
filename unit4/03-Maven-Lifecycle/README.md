# Maven Lifecycle

## What is Maven Lifecycle?

Maven Lifecycle is a sequence of predefined phases used to build and manage a project.

Each phase performs a specific task during project development.

Example:
- compiling code
- testing
- packaging
- deployment

---

# Types of Maven Lifecycles

Maven provides three built-in lifecycles:

1. Default Lifecycle
2. Clean Lifecycle
3. Site Lifecycle

---

# 1. Default Lifecycle

Used for:
- compilation
- testing
- packaging
- deployment

This is the most commonly used lifecycle.

---

# Important Default Lifecycle Phases

## validate

Checks project correctness and verifies required information.

Command:

```bash
mvn validate
```

---

## compile

Compiles source code.

Command:

```bash
mvn compile
```

---

## test

Runs unit tests.

Command:

```bash
mvn test
```

---

## package

Packages application into:
- JAR
- WAR

Command:

```bash
mvn package
```

---

## verify

Checks package validity and quality.

Command:

```bash
mvn verify
```

---

## install

Installs package into local Maven repository.

Command:

```bash
mvn install
```

Repository location:

```text
~/.m2/repository
```

---

## deploy

Deploys package to remote repository.

Command:

```bash
mvn deploy
```

---

# 2. Clean Lifecycle

Used to remove previously generated build files.

---

## clean

Deletes target directory.

Command:

```bash
mvn clean
```

---

# 3. Site Lifecycle

Used to generate project documentation.

---

## site

Creates project documentation website.

Command:

```bash
mvn site
```

---

# Maven Lifecycle Flow

```text
validate
   ↓
compile
   ↓
test
   ↓
package
   ↓
verify
   ↓
install
   ↓
deploy
```

---

# Important Concept

When a later phase is executed,
all previous phases run automatically.

Example:

```bash
mvn package
```

Automatically runs:
- validate
- compile
- test
- package

---

# Target Directory

Maven stores generated files inside:

```text
target/
```

Contains:
- compiled classes
- JAR files
- reports

---

# Advantages of Maven Lifecycle

- Standardized build process
- Reduced manual work
- Better automation
- Easy project management
- CI/CD integration support

---

# Important Viva Questions

## 1. What is Maven Lifecycle?
A predefined sequence of phases used to build and manage projects.

---

## 2. What are the three Maven lifecycles?
- Default
- Clean
- Site

---

## 3. What does mvn compile do?
Compiles project source code.

---

## 4. What does mvn package do?
Packages application into JAR or WAR file.

---

## 5. What is the purpose of mvn clean?
Deletes previously generated build files.

---

## 6. Where are Maven build files stored?
Inside the `target/` directory.

---

## 7. What happens when mvn install is executed?
Package is installed into local Maven repository.

---

# Common Maven Lifecycle Commands

## Clean Project

```bash
mvn clean
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

## Build JAR File

```bash
mvn package
```

---

## Install Project

```bash
mvn install
```

---

# Conclusion

Maven Lifecycle automates project build, testing, packaging, and deployment using predefined phases.