# Day 2 Java AI — Control Flow, Loops, Arrays, Lists, Sets, and Maps

**Java code is the same on Mac and Windows.** Only the final compile command changes.

AI agents, Kafka consumers, Spring Boot services, and cloud applications all process collections of data. Today you learn how Java makes decisions and processes many values safely.

## 1. Control flow: `if`, `else if`, `else`

```java
int completedDays = 2;

if (completedDays >= 10) {
    System.out.println("Ready for Spring Boot.");
} else if (completedDays >= 5) {
    System.out.println("Good progress. Keep going.");
} else {
    System.out.println("Build the Java foundation first.");
}
```

Use `if` when code must choose one path.

### Important: compare strings with `.equals()`

Wrong:

```java
if (topic == "Kafka") {
}
```

Correct:

```java
if ("Kafka".equals(topic)) {
    System.out.println("Kafka topic selected.");
}
```

`==` compares whether references point to the same object. `.equals()` compares content.

## 2. Loops

### `for` loop — known number of repetitions

```java
for (int day = 1; day <= 5; day++) {
    System.out.println("Studying Day " + day);
}
```

### Enhanced `for` loop — process every item

```java
String[] topics = {"Java", "Spring Boot", "Kafka"};

for (String topic : topics) {
    System.out.println(topic);
}
```

### `while` loop — repeat while a condition is true

```java
int retries = 0;

while (retries < 3) {
    System.out.println("Trying API request...");
    retries++;
}
```

Later, retry logic will matter for Kafka consumers and unreliable external AI APIs.

## 3. Array vs List vs Set vs Map

| Structure | Use it when | Example |
|---|---|---|
| Array | Size is fixed | fixed list of 7 weekdays |
| `List` | Ordered items; duplicates allowed | chat messages |
| `Set` | Unique items only | user permissions |
| `Map` | Key → value lookup | topic → completed lessons |

## 4. Day 2 Program — Learning Progress Analyzer

Create this file:

```text
lessons/day-02-java-collections/src/main/java/com/hawk/learning/Day02App.java
```

```java
package com.hawk.learning;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class Day02App {
    public static void main(String[] args) {
        String[] coreTopics = {
                "Java basics",
                "OOP",
                "Collections",
                "Spring Boot",
                "Kafka"
        };

        System.out.println("=== Core Topics ===");

        for (int index = 0; index < coreTopics.length; index++) {
            System.out.println((index + 1) + ". " + coreTopics[index]);
        }

        List<String> completedTopics = new ArrayList<>();
        completedTopics.add("Java basics");
        completedTopics.add("OOP");
        completedTopics.add("Collections");
        completedTopics.add("OOP");

        System.out.println("\n=== Completed Topics (List) ===");

        for (String topic : completedTopics) {
            System.out.println(topic);
        }

        Set<String> uniqueTopics = new HashSet<>(completedTopics);

        System.out.println("\n=== Unique Topics (Set) ===");

        for (String topic : uniqueTopics) {
            System.out.println(topic);
        }

        Map<String, Integer> topicProgress = new HashMap<>();
        topicProgress.put("Java basics", 100);
        topicProgress.put("OOP", 80);
        topicProgress.put("Collections", 60);
        topicProgress.put("Spring Boot", 0);

        System.out.println("\n=== Topic Progress (Map) ===");

        for (Map.Entry<String, Integer> entry : topicProgress.entrySet()) {
            String topic = entry.getKey();
            int progress = entry.getValue();

            if (progress >= 80) {
                System.out.println(topic + ": " + progress + "% — Strong");
            } else if (progress > 0) {
                System.out.println(topic + ": " + progress + "% — In progress");
            } else {
                System.out.println(topic + ": " + progress + "% — Not started");
            }
        }

        int retryAttempt = 1;

        System.out.println("\n=== API Retry Simulation ===");

        while (retryAttempt <= 3) {
            System.out.println("Attempt " + retryAttempt + " to call the AI service.");
            retryAttempt++;
        }
    }
}
```

## 5. Compile and run

### Windows PowerShell

```powershell
cd "$env:USERPROFILE\Documents\java-ai-mastery\lessons\day-02-java-collections"
javac -d out src\main\java\com\hawk\learning\Day02App.java
java -cp out com.hawk.learning.Day02App
```

### Mac Terminal

```zsh
cd ~/Documents/java-ai-mastery/lessons/day-02-java-collections
javac -d out src/main/java/com/hawk/learning/Day02App.java
java -cp out com.hawk.learning.Day02App
```

## Senior-level points to remember

- Use `ArrayList` as the normal default for ordered, editable data.
- Use `HashSet` when duplicate values must be removed.
- Use `HashMap` when you need fast lookup by a meaningful key.
- Do not depend on `HashSet` or `HashMap` iteration order.
- Never modify a collection directly inside an enhanced `for` loop; we will learn safe removal patterns later.
- Do not use an array when you need to add/remove items dynamically.

## Day 2 challenge

Add this after `topicProgress` is created:

```java
topicProgress.put("Kafka", 40);
topicProgress.put("Cloud", 20);
```

Then calculate and print:

```text
Topics started: <number>
Topics not started: <number>
```

A topic counts as “started” when its progress is greater than `0`.

Next: **Day 3 Java AI — OOP deeply: inheritance, interfaces, polymorphism, abstraction, and how Spring Boot uses these ideas.**
