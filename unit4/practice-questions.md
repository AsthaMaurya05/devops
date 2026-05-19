# Unit 4 Practice Questions and Exercises

## Basic Concepts

### Question 1: Maven Fundamentals
**Q:** What is Apache Maven and what are its three main advantages over traditional build systems?

**A:** Apache Maven is a build automation tool and project management framework for Java projects. Three main advantages are:
1. Convention over Configuration - Uses sensible defaults, reducing configuration needed
2. Automatic Dependency Management - Handles project dependencies automatically
3. Consistent Build Process - Provides standardized project structure across teams

---

### Question 2: Maven Coordinates
**Q:** Identify the three coordinates in the following Maven dependency:
```
com.google.guava:guava:31.0.1-jre
```

**A:**
- **GroupId**: com.google.guava
- **ArtifactId**: guava
- **Version**: 31.0.1-jre

---

## POM Structure

### Question 3: POM Elements
**Q:** What does POM stand for and list 5 essential sections in a pom.xml file.

**A:** POM stands for **Project Object Model**. Five essential sections are:
1. `<modelVersion>` - POM version
2. `<groupId>`, `<artifactId>`, `<version>` - Project identification
3. `<dependencies>` - External libraries
4. `<properties>` - Reusable values
5. `<build>` - Build configuration

---

### Question 4: POM Inheritance
**Q:** What is a parent POM and how does it benefit multi-module projects?

**A:** A parent POM is a common pom.xml file that contains shared configuration, dependencies, and properties. Benefits:
- Eliminates duplicate configuration
- Ensures consistent versions across modules
- Simplifies dependency management
- Facilitates consistent build process

---

## Maven Lifecycle

### Question 5: Build Phases
**Q:** List the 7 main phases of Maven's default lifecycle in order.

**A:**
1. validate
2. compile
3. test
4. package
5. verify
6. install
7. deploy

---

### Question 6: Maven Commands
**Q:** What command would you use to clean the project, run all tests, and package without deploying?

**A:** `mvn clean test package`

---

### Question 7: Skip Tests
**Q:** How would you build a Maven project while skipping all tests?

**A:** Use one of these approaches:
- `mvn clean package -DskipTests`
- `mvn clean package -Dmaven.test.skip=true`

---

## Dependency Management

### Question 8: Dependency Scopes
**Q:** Match each scope with its description:

| Scope | Description |
|-------|-------------|
| compile | Only needed for test compilation and execution |
| test | Available in all classpaths |
| provided | Not needed for compilation, only at runtime |
| runtime | Expected to be provided by JDK or runtime |

**A:**
- compile → Available in all classpaths
- test → Only needed for test compilation and execution
- provided → Expected to be provided by JDK or runtime
- runtime → Not needed for compilation, only at runtime

---

### Question 9: Transitive Dependencies
**Q:** What are transitive dependencies and why are they important in Maven?

**A:** Transitive dependencies are dependencies that your project's dependencies depend on. They're important because:
- Maven automatically manages them
- Reduces configuration overhead
- Helps prevent version conflicts
- Ensures all required libraries are available

---

### Question 10: Dependency Tree
**Q:** What Maven command would you use to view all dependencies including transitive ones?

**A:** `mvn dependency:tree`

---

## Maven Plugins

### Question 11: Plugins vs. Plugins Goals
**Q:** Explain the difference between a Maven plugin and a plugin goal.

**A:**
- **Plugin**: A software component that provides reusable goals (e.g., maven-compiler-plugin)
- **Goal**: A specific task executed by a plugin (e.g., compile goal of compiler plugin)

---

### Question 12: Plugin Configuration
**Q:** Write a Maven plugin configuration to set Java compilation source and target to version 11.

**A:**
```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <version>3.8.1</version>
  <configuration>
    <source>11</source>
    <target>11</target>
  </configuration>
</plugin>
```

---

## Maven Docker Integration

### Question 13: Multi-stage Docker Build
**Q:** What are the benefits of using a multi-stage Docker build for Java applications?

**A:** Benefits include:
- Smaller final image size (build dependencies excluded)
- Faster deployment (only runtime needed)
- Enhanced security (no build tools in production)
- Cleaner separation of concerns
- More efficient use of Docker layers

---

### Question 14: Build Process
**Q:** Describe the typical workflow to build and containerize a Java application using Maven and Docker.

**A:**
1. Write source code and pom.xml
2. Run `mvn clean package` to build JAR/WAR
3. Create Dockerfile with appropriate base image
4. Build Docker image: `docker build -t app:1.0 .`
5. Test container: `docker run -p 8080:8080 app:1.0`
6. Push to registry (optional): `docker push registry/app:1.0`

---

### Question 15: Maven Plugin for Docker
**Q:** Name two Maven plugins that can automatically build Docker images and describe one.

**A:** 
1. **Spotify Docker Maven Plugin** - Allows building Docker images from Maven using plugin configuration
2. **Google Jib Maven Plugin** - Builds optimized Docker images without requiring a Docker daemon

---

## Hands-on Exercises

### Exercise 1: Create and Build a Maven Project
Create a Maven project from scratch with:
- GroupId: `org.mycompany`
- ArtifactId: `hello-app`
- Version: `2.0.0`
- Add JUnit dependency for testing
- Build the project and verify the JAR is created

---

### Exercise 2: Dependency Management
1. Create a pom.xml with multiple Spring Boot dependencies
2. Run `mvn dependency:tree` to view the dependency tree
3. Identify and exclude an unnecessary transitive dependency
4. Verify the exclusion works

---

### Exercise 3: Maven Plugins
Configure the following plugins in a pom.xml:
1. Maven Compiler Plugin (Java 11)
2. Maven JAR Plugin (with main class specified)
3. Maven Assembly Plugin (create fat JAR)

Build the project and verify all artifacts are created.

---

### Exercise 4: Docker Integration
1. Create a Spring Boot application using Maven
2. Write a multi-stage Dockerfile
3. Build the Docker image
4. Run the container and verify it works
5. Push to a Docker registry (Docker Hub or private)

---

## Advanced Questions

### Question 16: Version Management
**Q:** How would you manage consistent versions across multiple dependencies in a pom.xml?

**A:** Use properties:
```xml
<properties>
  <spring.version>5.3.9</spring.version>
</properties>

<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-core</artifactId>
  <version>${spring.version}</version>
</dependency>
```

---

### Question 17: Repository Configuration
**Q:** How do you configure a private Maven repository in pom.xml?

**A:**
```xml
<repositories>
  <repository>
    <id>private-repo</id>
    <url>https://nexus.example.com/repository/maven-releases/</url>
    <credentials>
      <username>user</username>
      <password>password</password>
    </credentials>
  </repository>
</repositories>
```

---

### Question 18: Continuous Integration
**Q:** How would you set up a Maven project for CI/CD pipeline?

**A:**
1. Use consistent pom.xml versioning
2. Configure automated tests in Maven
3. Use Maven profiles for different environments
4. Implement dependency management
5. Set up automated builds on code push
6. Configure automated Docker image creation
7. Push artifacts to repository automatically

---

## Answer Key Summary

**Key Concepts to Remember:**
- Maven follows Convention over Configuration
- Dependencies are managed through pom.xml
- Build lifecycle has 7 main phases
- Plugins extend Maven functionality
- Docker integrates with Maven for containerization
- Use properties for version management
- Parent POMs reduce configuration duplication
- Transitive dependencies are automatically managed

**Common Commands:**
```
mvn clean package          # Build project
mvn dependency:tree        # View dependencies
mvn clean install          # Build and install
mvn test                   # Run tests only
mvn help:describe          # Get plugin help
```

---

## References

- [Apache Maven Official Documentation](https://maven.apache.org/)
- [Maven POM Reference](https://maven.apache.org/pom.html)
- [Maven Plugin Documentation](https://maven.apache.org/plugins/)
- [Docker Best Practices with Java](https://docs.docker.com/language/java/)
