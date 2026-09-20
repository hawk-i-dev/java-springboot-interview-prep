# Day 1 Java AI — Java Basics Inside STS

Today: Java execution, variables, types, classes, objects, constructors, methods, and encapsulation.

```text
.java source code
      ↓ compiler
.class bytecode
      ↓ JVM
running application
```

Java is statically typed:

```java
String modelName = "gpt-5";
int maxTokens = 500;
double temperature = 0.7;
boolean active = true;
```

## 1. Create the Day 1 package in STS

Inside `java-ai-lab`:

1. Expand `src/main/java`
2. Right-click → **New → Package**
3. Enter:

```text
com.hawk.javaai.day01
```

4. Right-click that package → **New → Class**
5. Create `AiLearningProfile`
6. Create one more class: `Day01JavaBasics`
7. For `Day01JavaBasics`, tick **public static void main(String[] args)**

Your structure:

```text
src/main/java/
└── com/hawk/javaai/day01/
    ├── AiLearningProfile.java
    └── Day01JavaBasics.java
```

## 2. Create `AiLearningProfile.java`

```java
package com.hawk.javaai.day01;

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

    public boolean hasCompletedAtLeast(int requiredDays) {
        return completedDays >= requiredDays;
    }

    public String buildLearningPrompt(String topic) {
        return "Teach " + topic
                + " deeply for " + name
                + " using Java, Spring Boot, microservices, and AI examples.";
    }

    public String getSummary() {
        return "Learner: " + name
                + " | Track: " + track
                + " | Completed days: " + completedDays;
    }
}
```

## 3. Create `Day01JavaBasics.java`

```java
package com.hawk.javaai.day01;

public class Day01JavaBasics {
    public static void main(String[] args) {
        AiLearningProfile profile = new AiLearningProfile(
                "Hawk",
                "Java + Spring Boot + Microservices + Kafka + Cloud + AI"
        );

        profile.completeDay();

        System.out.println(profile.getSummary());
        System.out.println(
                "Ready for Spring Boot: "
                        + profile.hasCompletedAtLeast(10)
        );
        System.out.println(
                profile.buildLearningPrompt("Java classes and objects")
        );
    }
}
```

## 4. Understand the code

```java
private final String name;
```

- `String` is the type.
- `name` is the field.
- `private` prevents other classes from changing it directly.
- `final` means it cannot be reassigned after construction.

```java
AiLearningProfile profile = new AiLearningProfile(...);
```

- `AiLearningProfile` = class/blueprint
- `profile` = reference variable
- `new AiLearningProfile(...)` = actual object

```java
public void completeDay()
```

A method that performs an action but returns nothing.

```java
public boolean hasCompletedAtLeast(int requiredDays)
```

A method that returns either `true` or `false`.

## 5. Run in STS

Right-click `Day01JavaBasics.java`:

```text
Run As → Java Application
```

Expected output:

```text
Learner: Hawk | Track: Java + Spring Boot + Microservices + Kafka + Cloud + AI | Completed days: 1
Ready for Spring Boot: false
Teach Java classes and objects deeply for Hawk using Java, Spring Boot, microservices, and AI examples.
```

## Day 1 challenge

Add this method inside `AiLearningProfile`:

```java
public String getProgressMessage() {
    if (completedDays >= 10) {
        return "Ready to begin Spring Boot.";
    }

    return "Complete more Java foundation days first.";
}
```

Then print it in `Day01JavaBasics`.

Next: **Day 2 Java AI — conditions, loops, arrays, lists, sets, maps, and data processing.**
