# Day 0 Java AI — Setup for Spring Boot, Microservices, Kafka, Cloud, and AI

We will use the same tools on both systems:

```text
Java 21 LTS + VS Code + Spring Boot + Maven Wrapper + Docker
```

Java code is the same on Mac and Windows. Only installation and terminal commands differ.

Spring Boot requires Java 17 or later; Java 21 LTS is our practical baseline. [Spring Boot system requirements](https://docs.spring.io/spring-boot/system-requirements.html)

## 1. Create the workspace

### Windows PowerShell

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\Documents\java-ai-mastery"
cd "$env:USERPROFILE\Documents\java-ai-mastery"
```

### Mac Terminal

```zsh
mkdir -p ~/Documents/java-ai-mastery
cd ~/Documents/java-ai-mastery
```

## 2. Install Java 21 JDK

A **JDK** includes the Java compiler (`javac`), not only the Java runtime.

### Windows PowerShell

First check:

```powershell
java -version
javac -version
```

If Java 21 is missing:

```powershell
winget install -e --id EclipseAdoptium.Temurin.21.JDK
```

Close and reopen PowerShell, then verify again:

```powershell
java -version
javac -version
```

### Mac Terminal

First check:

```zsh
java -version
javac -version
```

If Java 21 is missing:

```zsh
brew install --cask temurin@21
```

Close and reopen Terminal, then verify:

```zsh
java -version
javac -version
```

You should see Java version `21`.

## 3. VS Code extensions

Open the `java-ai-mastery` folder in VS Code and install:

- **Extension Pack for Java** — Microsoft
- **Spring Boot Extension Pack** — VMware
- **Docker** — Microsoft
- **GitLens** — GitKraken, optional but useful

Use VS Code for this track since you already know it. IntelliJ IDEA is also popular for Java, but is not required.

## 4. Install Docker Desktop

We will use Docker for PostgreSQL/MySQL containers, Kafka, Redis, microservices, and deployments.

Install **Docker Desktop** for your operating system, launch it, and wait until Docker says it is running. [Docker Desktop installation](https://docs.docker.com/get-started/get-docker/)

Then verify:

```bash
docker --version
docker compose version
```

This command is the **same on Mac and Windows**.

Do not install Kafka manually today. Later, Docker will run Kafka locally on port `9092`; Kafka officially supports this local Docker workflow. [Kafka Docker quickstart](https://kafka.apache.org/quickstart/)

## 5. Git check

```bash
git --version
```

If Git is missing, install it from [Git’s official download page](https://git-scm.com/downloads), then reopen your terminal.

## 6. Create the Java project structure

Create these folders in VS Code Explorer:

```text
java-ai-mastery/
├── lessons/
├── projects/
├── docs/
└── hello-java/
    └── src/
        └── main/
            └── java/
                └── com/
                    └── yourname/
                        └── learning/
                            └── HelloJava.java
```

Create `HelloJava.java` with this code:

```java
package com.yourname.learning;

public class HelloJava {
    public static void main(String[] args) {
        System.out.println("Java AI environment is ready.");

        String goal = "Spring Boot, Microservices, Kafka, Cloud, and AI";
        System.out.println("Learning goal: " + goal);
    }
}
```

Replace `yourname` consistently with your own lowercase name, for example:

```text
com.hemanth.learning
```

## 7. Compile and run the first Java program

Run these commands from inside the `hello-java` folder.

### Windows PowerShell

```powershell
cd .\hello-java
javac -d out src\main\java\com\yourname\learning\HelloJava.java
java -cp out com.yourname.learning.HelloJava
```

### Mac Terminal

```zsh
cd hello-java
javac -d out src/main/java/com/yourname/learning/HelloJava.java
java -cp out com.yourname.learning.HelloJava
```

Expected output:

```text
Java AI environment is ready.
Learning goal: Spring Boot, Microservices, Kafka, Cloud, and AI
```

## What we will not install today

- Kafka manually
- Kubernetes
- Cloud accounts or paid cloud services
- AI API keys
- Global Maven installation

Spring Boot projects come with a **Maven Wrapper** (`mvnw`), so each project controls its own Maven version. This avoids “works on my machine” issues.

After Java and Docker verification works, we start **Day 1 Java AI: Java execution model, classes, objects, methods, variables, types, and OOP foundations.**
