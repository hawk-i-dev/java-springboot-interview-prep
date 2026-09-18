Correct — that method is perfect.

```java
public boolean hasCompletedAtLeast(int requiredDays) {
    return completedDays >= requiredDays;
}
```

Add it inside the `AiLearningProfile` class, before its final `}`.

Then add this to `Day01App.java`, after `profile.completeDay();`:

```java
boolean readyForSpringBoot = profile.hasCompletedAtLeast(10);

System.out.println("Ready for Spring Boot: " + readyForSpringBoot);
```

Because you have completed only one day, the output will be:

```text
Ready for Spring Boot: false
```

Later, after calling `profile.completeDay()` ten times, it will become `true`.
