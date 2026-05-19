# Maven Plugins

## What are Maven Plugins?

Maven plugins are components that perform specific tasks during the build lifecycle.

Examples:
- compiling code
- running tests
- packaging applications
- creating JAR files
- Docker integration

Maven functionality is mostly implemented through plugins.

---

# Plugin Structure

Plugins are configured inside:

```xml
<build>
    <plugins>

    </plugins>
</build>
```

section of `pom.xml`.

---

# Plugin Components

## groupId

Identifies plugin organization.

---

## artifactId

Specifies plugin name.

---

## version

Defines plugin version.

---

# Maven Compiler Plugin

Used to compile Java source code.

Example:

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>

    <configuration>
        <source>17</source>
        <target>17</target>
    </configuration>

</plugin>
```

---

# Purpose of Compiler Plugin

- Compiles Java code
- Defines Java version
- Generates `.class` files

---

# Maven Surefire Plugin

Used to run unit tests.

Example:

```xml
<plugin>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>3.1.2</version>
</plugin>
```

---

# Purpose of Surefire Plugin

- Executes test cases
- Generates test reports
- Supports JUnit testing

---

# Maven Shade Plugin

Used to create:

```text
Uber JAR / Fat JAR
```

An Uber JAR contains:
- project code
- all dependencies
- executable configuration

inside a single JAR file.

---

# Shade Plugin Example

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-shade-plugin</artifactId>
    <version>3.5.0</version>
</plugin>
```

---

# Advantages of Uber JAR

- Easy deployment
- Portable execution
- Single executable file
- Simplified dependency handling

---

# Maven Wrapper (mvnw)

Maven Wrapper ensures consistent Maven version across all systems.

Files created:
- mvnw
- mvnw.cmd
- .mvn/

---

# Generate Maven Wrapper

Command:

```bash
mvn wrapper:wrapper
```

---

# Using Maven Wrapper

Linux/macOS:

```bash
./mvnw clean package
```

Windows:

```bash
mvnw.cmd clean package
```

---

# Docker Maven Plugin

Used for Docker integration with Maven.

Example:

```xml
<plugin>
    <groupId>com.spotify</groupId>
    <artifactId>dockerfile-maven-plugin</artifactId>
    <version>1.4.13</version>
</plugin>
```

---

# Advantages of Maven Plugins

- Build automation
- Test automation
- Packaging support
- Docker integration
- CI/CD compatibility

---

# Important Viva Questions

## 1. What are Maven plugins?
Plugins are components that perform specific build tasks.

---

## 2. What is the purpose of Maven Compiler Plugin?
To compile Java source code.

---

## 3. What is Maven Surefire Plugin used for?
To execute unit tests.

---

## 4. What is an Uber JAR?
A single executable JAR containing application code and dependencies.

---

## 5. What is the purpose of Maven Wrapper?
To maintain consistent Maven version across environments.

---

## 6. Which plugin is used for Docker integration?
`dockerfile-maven-plugin`

---

# Common Plugin Commands

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

## Create Wrapper

```bash
mvn wrapper:wrapper
```

---

# Conclusion

Maven plugins automate compilation, testing, packaging, and Docker integration during the build lifecycle.