# POM Structure in Maven

## What is POM?

POM stands for:

```text
Project Object Model
```

It is the core configuration file in Maven projects.

The POM file is stored as:

```text
pom.xml
```

Maven uses this file to:
- manage dependencies
- configure plugins
- define project information
- control build process

---

# Basic Structure of pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>demo-app</artifactId>
    <version>1.0-SNAPSHOT</version>

</project>
```

---

# Important POM Elements

## 1. modelVersion

```xml
<modelVersion>4.0.0</modelVersion>
```

Specifies POM model version.

---

## 2. groupId

```xml
<groupId>com.example</groupId>
```

Identifies organization or company name.

Example:
- com.google
- org.apache

---

## 3. artifactId

```xml
<artifactId>demo-app</artifactId>
```

Represents project name.

---

## 4. version

```xml
<version>1.0-SNAPSHOT</version>
```

Defines project version.

### SNAPSHOT
Indicates project is under development.

---

## 5. packaging

```xml
<packaging>jar</packaging>
```

Defines output type.

Common values:
- jar
- war
- pom

---

# Dependencies

Dependencies are external libraries required by the project.

Example:

```xml
<dependencies>

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>

</dependencies>
```

---

# Build Section

Used to configure plugins and build process.

Example:

```xml
<build>
    <plugins>

    </plugins>
</build>
```

---

# Maven Coordinates

Every Maven project is uniquely identified using:

```text
groupId + artifactId + version
```

Example:

```text
com.example:demo-app:1.0-SNAPSHOT
```

---

# Parent POM

A Parent POM provides common configuration for multiple projects.

Example:

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.2.0</version>
</parent>
```

---

# Advantages of POM

- Centralized configuration
- Easy dependency management
- Build standardization
- Plugin configuration
- Better maintainability

---

# Important Viva Questions

## 1. What is pom.xml?
It is the main Maven configuration file.

---

## 2. What is groupId?
It identifies organization or project group.

---

## 3. What is artifactId?
It identifies project name.

---

## 4. What is version in Maven?
Defines project release version.

---

## 5. What is SNAPSHOT version?
Indicates project is under development.

---

## 6. What is packaging in Maven?
Defines output format such as JAR or WAR.

---

## 7. What is Parent POM?
A Parent POM provides shared configuration across projects.

---

# Conclusion

The POM file is the heart of Maven projects and controls dependencies, plugins, and build configuration.