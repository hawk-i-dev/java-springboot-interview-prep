# Day 1 Java AI — Java Foundations, Classes, Objects, and Methods

**Java code is the same on Mac and Windows.** Only the compile command path separator differs.

Today you will understand how Java runs and build your first small AI-learning domain model.

## 1. How Java runs

```text
Hello.java
   ↓ javac compiles
Hello.class   ← bytecode
   ↓ JVM runs it
Output
```

- `.java` = source code you write
- `javac` = Java compiler
- `.class` = portable bytecode
- JVM = Java Virtual Machine, which runs bytecode

This is why Java code can run on Windows, Mac, Linux, cloud servers, and Docker containers.

## 2. Java is statically typed

Python allows:

```python
value = "hello"
value = 10
```

Java expects you to declare a type:

```java
String modelName = "gpt-5";
int maxTokens = 500;
double temperature = 0.7;
boolean isAvailable = true;
```

Benefits:

- More errors are caught before the program runs
- Large Spring Boot projects are easier to maintain
- IDE autocomplete and refactoring are safer
- Clear contracts between microservices

## 3. Primitive types vs reference types

### Primitive types

They store simple values:

```java
int completedDays = 1;
double temperature = 0.7;
boolean isLearning = true;
char grade = 'A';
```

### Reference types

They refer to objects:

```java
String topic = "Kafka";
AiLearningProfile profile = new AiLearningProfile(...);
```

An object is created with `new`.

```java
AiLearningProfile profile = new AiLearningProfile(
    "hawk",
    "Java AI"
);
```

`profile` refers to the actual object in memory.

## 4. Class vs object

```text
Class  = blueprint
Object = real item created from the blueprint
```

Example:

```java
class AiLearningProfile {
    String name;
    String track;
}
```

This defines a blueprint. Then:

```java
AiLearningProfile profile = new AiLearningProfile(...);
```

creates an object from it.

In real projects:

- `User` class → one user object
- `Order` class → one order object
- `KafkaEvent` class → one event object
- `RagDocument` class → one uploaded document object
- `AgentTask` class → one AI-agent task object

## 5. Encapsulation: protect object data

Do not let any code change important fields freely.

Bad:

```java
public int completedDays;
```

Better:

```java
private int completedDays;
```

`private` means only code inside that class can directly modify the field. Public methods control safe changes.

This is called **encapsulation**, a core OOP principle.

## 6. Constructor and methods

- **Constructor**: runs when an object is created.
- **Method**: behavior an object can perform.
- `static`: belongs to the class itself, not to a particular object.
- `main` is static because Java needs a starting point before any object exists.

# Day 1 Program

Inside `java-ai-mastery`, create:

```text
lessons/
└── day-01-java-basics/
    └── src/
        └── main/
            └── java/
                └── com/
                    └── hawk/
                        └── learning/
                            ├── AiLearningProfile.java
                            └── Day01App.java
```

If you use a different package name, change it consistently in both files and commands.

## File 1: `AiLearningProfile.java`

```java
package com.hawk.learning;

public class AiLearningProfile {
    private final String name;
    private final String track;
    private int completedDays;

    public AiLearningProfile(String name, String track) {
        if (name == null || name.isBlank()) {
            throw new IllegalArgumentException("Name cannot be blank.");
        }

        if (track == null || track.isBlank()) {
            throw new IllegalArgumentException("Track cannot be blank.");
        }

        this.name = name;
        this.track = track;
        this.completedDays = 0;
    }

    public void completeDay() {
        completedDays++;
    }

    public String buildLearningPrompt(String topic) {
        if (topic == null || topic.isBlank()) {
            throw new IllegalArgumentException("Topic cannot be blank.");
        }

        return "Teach " + topic
                + " deeply for " + name
                + " with Java, Spring Boot, microservices, and AI examples.";
    }

    public String getSummary() {
        return "Learner: " + name
                + " | Track: " + track
                + " | Completed days: " + completedDays;
    }
}
```

Important details:

- `private` protects fields.
- `final` means `name` and `track` cannot be reassigned after construction.
- `this.name` means “this object’s `name` field.”
- `throw` stops invalid data early—this is essential in professional applications.

## File 2: `Day01App.java`

```java
package com.hawk.learning;

public class Day01App {
    public static void main(String[] args) {
        AiLearningProfile profile = new AiLearningProfile(
                "hawk",
                "Java + Spring Boot + Microservices + AI"
        );

        profile.completeDay();

        System.out.println(profile.getSummary());
        System.out.println(profile.buildLearningPrompt("Java classes and objects"));
    }
}
```

## Compile and run

### Windows PowerShell

From `java-ai-mastery\lessons\day-01-java-basics`:

```powershell
javac -d out src\main\java\com\hawk\learning\AiLearningProfile.java src\main\java\com\hawk\learning\Day01App.java
java -cp out com.hawk.learning.Day01App
```

### Mac Terminal

From `java-ai-mastery/lessons/day-01-java-basics`:

```zsh
javac -d out src/main/java/com/hawk/learning/AiLearningProfile.java src/main/java/com/hawk/learning/Day01App.java
java -cp out com.hawk.learning.Day01App
```

Expected output:

```text
Learner: hawk | Track: Java + Spring Boot + Microservices + AI | Completed days: 1
Teach Java classes and objects deeply for hawk with Java, Spring Boot, microservices, and AI examples.
```

## Day 1 challenge

Add a method to `AiLearningProfile`:

```java
public boolean hasCompletedAtLeast(int requiredDays)
```

It should return `true` only when `completedDays` is greater than or equal to `requiredDays`.

Then call it from `Day01App` and print whether you are ready to start Spring Boot after completing at least `10` days.

Next: **Day 2 Java AI — control flow, loops, arrays, collections, and how Java handles groups of data in AI/microservice applications.**
