# Day 2 Java AI — Conditions, Loops, Arrays, Lists, Sets, and Maps

Today you learn how Java processes groups of data—the base of AI pipelines, Kafka events, database results, and API responses.

## 1. Create the Day 2 package

In STS:

```text
src/main/java → Right-click → New → Package
```

Package name:

```text
com.hawk.javaai.day02
```

Create a class:

```text
Day02Collections
```

Tick:

```text
public static void main(String[] args)
```

## 2. Key collection types

| Type | Use |
|---|---|
| Array | Fixed number of values |
| `List` | Ordered values; duplicates allowed |
| `Set` | Unique values only |
| `Map` | Key → value lookup |

Example:

```java
String[] fixedTopics = {"Java", "Spring Boot"};

List<String> messages = new ArrayList<>();

Set<String> permissions = new HashSet<>();

Map<String, Integer> progress = new HashMap<>();
```

## 3. Create `Day02Collections.java`

```java
package com.hawk.javaai.day02;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class Day02Collections {
    public static void main(String[] args) {
        String[] coreTopics = {
                "Java Basics",
                "OOP",
                "Collections",
                "Spring Boot",
                "Kafka"
        };

        System.out.println("=== Core Topics (Array) ===");

        for (int index = 0; index < coreTopics.length; index++) {
            System.out.println((index + 1) + ". " + coreTopics[index]);
        }

        List<String> completedTopics = new ArrayList<>();
        completedTopics.add("Java Basics");
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
        topicProgress.put("Java Basics", 100);
        topicProgress.put("OOP", 80);
        topicProgress.put("Collections", 60);
        topicProgress.put("Spring Boot", 0);
        topicProgress.put("Kafka", 40);
        topicProgress.put("Cloud", 20);

        int topicsStarted = 0;
        int topicsNotStarted = 0;

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

            if (progress > 0) {
                topicsStarted++;
            } else {
                topicsNotStarted++;
            }
        }

        System.out.println("\nTopics started: " + topicsStarted);
        System.out.println("Topics not started: " + topicsNotStarted);

        int retryAttempt = 1;

        System.out.println("\n=== AI API Retry Simulation ===");

        while (retryAttempt <= 3) {
            System.out.println("Attempt " + retryAttempt + " to call the AI service.");
            retryAttempt++;
        }
    }
}
```

## 4. Important concepts

```java
for (String topic : completedTopics)
```

This means: “For every topic in the list, run this code.”

```java
Map<String, Integer>
```

Means: “Each key is a `String`; each value is an `Integer`.”

```java
if (progress > 0)
```

This makes a decision based on a condition.

```java
while (retryAttempt <= 3)
```

This repeats until the condition becomes false. Later, retry patterns will matter for Kafka and external AI APIs.

## 5. Run it in STS

Right-click `Day02Collections.java`:

```text
Run As → Java Application
```

Expected final counts:

```text
Topics started: 5
Topics not started: 1
```

The order of `HashSet` and `HashMap` values may differ each time. Do not rely on their display order.

## Day 2 challenge

Add two more progress entries:

```java
topicProgress.put("Docker", 0);
topicProgress.put("Microservices", 70);
```

Then print this additional result:

```text
Topics with strong progress: <number>
```

A topic is strong when its progress is `80` or more.
