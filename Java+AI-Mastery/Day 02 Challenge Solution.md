Correct—your Day 2 challenge solution is logically right.

With your data, the output counts will be:

```text
Topics started: 5
Topics not started: 1
```

`Spring Boot` is the only topic with `0`, so it is not started.

Your counting inside the existing conditions is good:

```java
if (progress >= 80) {
    topicsStarted++;
} else if (progress > 0) {
    topicsStarted++;
} else {
    topicsNotStarted++;
}
```

A slightly cleaner version separates the display decision from the counting decision:

```java
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

System.out.println("Topics started: " + topicsStarted);
System.out.println("Topics not started: " + topicsNotStarted);
```

Both versions are correct. Your original version proves you understand `Map`, `entrySet()`, loops, `if / else if / else`, and counters.
