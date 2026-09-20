# Day 0 Java AI — Fresh Start with STS + Maven

We will restart cleanly using **Spring Tools for Eclipse (STS)** and a proper Maven/Spring Boot project structure.

Keep the old `java-ai-mastery` folder. Do not delete it. Create a new workspace for the restarted track.

## 1. Install Spring Tools (STS)

Download Spring Tools for Eclipse from the official site:

[Spring Tools downloads](https://spring.io/tools/)

Choose:

- **Mac Apple Silicon** if your Mac has an M-series chip
- **Mac x86_64** if it has an Intel chip
- **Windows x86_64** for a normal Windows laptop

Spring Boot supports Java 17+, so your Java 17 JDK is suitable. [Spring Boot requirements](https://docs.spring.io/spring-boot/system-requirements.html)

## 2. Verify Java 17

### Mac Terminal

```zsh
java -version
javac -version
```

### Windows PowerShell

```powershell
java -version
javac -version
```

Both should show version `17`.

## 3. Create a new STS workspace

When STS opens, it asks for a workspace location.

### Mac

```text
/Users/your-name/Documents/java-ai-sts-workspace
```

### Windows

```text
C:\Users\your-name\Documents\java-ai-sts-workspace
```

Click **Launch**.

A workspace is where STS keeps your Java projects and its project configuration.

## 4. Configure Java 17 in STS

In STS:

1. Open **Preferences**
2. Search for `Installed JREs`
3. Open **Java → Installed JREs**
4. Confirm Java 17 is selected as the default JRE

If Java 17 does not appear, click **Search** and select the JDK location.

## 5. Create the first proper Spring Boot project

In STS:

1. Click **File → New → Spring Starter Project**
2. Enter these values:

| Field | Value |
|---|---|
| Name | `java-ai-lab` |
| Type | Maven |
| Packaging | Jar |
| Java Version | 17 |
| Group | `com.hawk` |
| Artifact | `java-ai-lab` |
| Package | `com.hawk.javaai` |
| Description | Java, Spring Boot, Microservices, Kafka, Cloud, and AI learning lab |

3. Click **Next**
4. Add these dependencies:

```text
Spring Web
Spring Boot Actuator
```

5. Click **Finish**

STS will download dependencies. Wait until the progress bar completes.

Your project will have the professional standard structure automatically:

```text
java-ai-lab/
├── src/
│   ├── main/
│   │   ├── java/com/hawk/javaai/
│   │   │   └── JavaAiLabApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
├── pom.xml
├── mvnw
└── mvnw.cmd
```

No manual `src/main/java` configuration is needed now.

## 6. Run the application

Right-click:

```text
JavaAiLabApplication.java
```

Then choose:

```text
Run As → Spring Boot App
```

Look in the STS Console for something similar to:

```text
Started JavaAiLabApplication
Tomcat started on port 8080
```

Open this in your browser:

```text
http://localhost:8080/actuator/health
```

Expected result:

```json
{"status":"UP"}
```

That confirms Spring Boot is running correctly.

## 7. Terminal commands, if needed

STS can run Maven for you. But these commands are useful later.

### Mac

```zsh
cd ~/Documents/java-ai-sts-workspace/java-ai-lab
./mvnw spring-boot:run
```

### Windows PowerShell

```powershell
cd "$env:USERPROFILE\Documents\java-ai-sts-workspace\java-ai-lab"
.\mvnw.cmd spring-boot:run
```

Stop the running application with `Ctrl + C`, or use the red stop button in STS.

## Day 0 success checklist

- Java 17 installed
- STS opens successfully
- `java-ai-lab` Maven project created
- Project package is `com.hawk.javaai`
- `/actuator/health` returns `{"status":"UP"}`

From this restart, all Java lessons will use this STS Maven project. Day 1 Java AI will restart with Java execution, types, objects, methods, and OOP—inside the correct project structure.
