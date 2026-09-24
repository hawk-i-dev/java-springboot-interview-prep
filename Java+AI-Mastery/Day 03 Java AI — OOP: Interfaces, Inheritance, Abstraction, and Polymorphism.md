# Day 3 Java AI — OOP: Interfaces, Inheritance, Abstraction, and Polymorphism

Today’s idea:

```text
Interface       → what a component promises to do
Abstract class  → shared reusable behavior
Child class     → a specific implementation
Polymorphism    → one type, many behaviors
```

This is used everywhere in Spring Boot:

```text
Controller → Service interface → Service implementation
```

It is also useful for AI systems:

```text
RAG capability
Agent capability
SQL capability
```

## 1. Create the package

In STS:

```text
src/main/java → Right-click → New → Package
```

Create:

```text
com.hawk.javaai.day03
```

Create these classes/files:

```text
AiCapability.java
BaseAiCapability.java
RagCapability.java
AgentCapability.java
Day03Oop.java
```

## 2. `AiCapability.java`

```java
package com.hawk.javaai.day03;

public interface AiCapability {
    String getName();

    String execute(String request);
}
```

An interface is a contract. Every AI capability must have a name and execute a request.

## 3. `BaseAiCapability.java`

```java
package com.hawk.javaai.day03;

public abstract class BaseAiCapability implements AiCapability {
    private final String name;

    protected BaseAiCapability(String name) {
        this.name = name;
    }

    @Override
    public String getName() {
        return name;
    }

    protected String validateAndCleanRequest(String request) {
        if (request == null || request.isBlank()) {
            throw new IllegalArgumentException("Request cannot be blank.");
        }

        return request.trim();
    }
}
```

Important:

- `abstract` means this class cannot be created directly.
- `protected` means child classes can use the method.
- `implements AiCapability` means this class follows the interface contract.

## 4. `RagCapability.java`

```java
package com.hawk.javaai.day03;

public class RagCapability extends BaseAiCapability {
    public RagCapability() {
        super("RAG Capability");
    }

    @Override
    public String execute(String request) {
        String cleanRequest = validateAndCleanRequest(request);

        return "RAG result: searched approved documents for: "
                + cleanRequest;
    }
}
```

`extends` means this class inherits code from `BaseAiCapability`.

## 5. `AgentCapability.java`

```java
package com.hawk.javaai.day03;

public class AgentCapability extends BaseAiCapability {
    public AgentCapability() {
        super("Agent Capability");
    }

    @Override
    public String execute(String request) {
        String cleanRequest = validateAndCleanRequest(request);

        return "Agent result: created a plan and selected tools for: "
                + cleanRequest;
    }
}
```

## 6. `Day03Oop.java`

When creating this class, tick:

```text
public static void main(String[] args)
```

```java
package com.hawk.javaai.day03;

import java.util.List;

public class Day03Oop {
    public static void main(String[] args) {
        List<AiCapability> capabilities = List.of(
                new RagCapability(),
                new AgentCapability()
        );

        String request = "Explain how Kafka supports microservices.";

        for (AiCapability capability : capabilities) {
            System.out.println("=== " + capability.getName() + " ===");
            System.out.println(capability.execute(request));
            System.out.println();
        }
    }
}
```

This is polymorphism:

```java
List<AiCapability> capabilities
```

The list treats RAG and Agent as the shared `AiCapability` type, but Java calls each class’s own `execute()` method.

## 7. Run it

Right-click `Day03Oop.java`:

```text
Run As → Java Application
```

Expected output:

```text
=== RAG Capability ===
RAG result: searched approved documents for: Explain how Kafka supports microservices.

=== Agent Capability ===
Agent result: created a plan and selected tools for: Explain how Kafka supports microservices.
```

## Day 3 challenge

Create `SqlCapability.java`.

Requirements:

- Package: `com.hawk.javaai.day03`
- Extend `BaseAiCapability`
- Call `super("SQL Capability")`
- Implement `execute(String request)`
- Use `validateAndCleanRequest(request)`
- Return a message saying it would safely query an approved database
- Add `new SqlCapability()` to the `capabilities` list

Next: **Day 4 Java AI — exceptions, validation, logging, and resilient services.**
