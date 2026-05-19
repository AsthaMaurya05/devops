# Dependency Management in Maven

## What is Dependency Management?

Dependency management is the process of handling external libraries required by a project.

In Maven, dependencies are declared inside:

```xml
<dependencies>
</dependencies>
```

section of `pom.xml`.

Maven automatically:
- downloads dependencies
- manages versions
- resolves dependency conflicts

---

# Example Dependency

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
```

---

# Dependency Components

## groupId

Identifies organization or library provider.

Example:

```xml
<groupId>junit</groupId>
```

---

## artifactId

Represents library name.

Example:

```xml
<artifactId>junit</artifactId>
```

---

## version

Specifies library version.

Example:

```xml
<version>4.13.2</version>
```

---

## scope

Defines where dependency is available.

Example:

```xml
<scope>test</scope>
```

---

# Dependency Scopes

## 1. compile

Default scope.

Available:
- compile time
- test time
- runtime

Example:
- Spring Core libraries

---

## 2. provided

Available during:
- compile
- test

NOT included at runtime.

Example:
- Servlet API provided by Tomcat

---

## 3. runtime

Required only during runtime.

Example:
- JDBC drivers

---

## 4. test

Available only during testing.

Example:
- JUnit
- Mockito

---

## 5. system

Uses local system JAR path.

Not recommended.

---

# Transitive Dependencies

Maven automatically downloads dependencies required by other dependencies.

Example:

```text
Project → Spring Boot → Logging Libraries
```

No need to manually add all libraries.

---

# Dependency Conflict

Sometimes multiple versions of same library exist.

Example:

```text
Library A → log4j 1.0
Library B → log4j 2.0
```

This creates version conflict.

---

# Conflict Resolution

Maven uses:

```text
Nearest Definition Wins
```

Nearest dependency in dependency tree is selected.

---

# Excluding Dependencies

Unwanted dependencies can be removed using:

```xml
<exclusions>
    <exclusion>
        <groupId>com.example</groupId>
        <artifactId>old-lib</artifactId>
    </exclusion>
</exclusions>
```

---

# Dependency Management Section

Used to centrally manage dependency versions.

Example:

```xml
<dependencyManagement>
    <dependencies>

    </dependencies>
</dependencyManagement>
```

---

# Advantages of Dependency Management

- Automatic dependency download
- Reduced manual work
- Better version control
- Easy project maintenance
- Faster project setup

---

# Important Viva Questions

## 1. What is dependency management in Maven?
Dependency management handles external libraries required by a project.

---

## 2. Where are dependencies declared?
Inside `pom.xml`.

---

## 3. What is dependency scope?
It defines where a dependency is available.

---

## 4. What are transitive dependencies?
Dependencies automatically downloaded by Maven for other dependencies.

---

## 5. What is dependency conflict?
When multiple versions of same library exist.

---

## 6. How does Maven resolve dependency conflicts?
Using nearest definition wins strategy.

---

## 7. What is the purpose of exclusions?
To remove unwanted transitive dependencies.

---

# Common Dependency Commands

## Download Dependencies

```bash
mvn dependency:resolve
```

---

## View Dependency Tree

```bash
mvn dependency:tree
```

---

## Clean and Install

```bash
mvn clean install
```

---

# Conclusion

Maven dependency management simplifies handling of external libraries and automatically resolves dependencies and version conflicts.