# Day 3 Java AI — OOP Deeply: Interface, Abstraction, Inheritance, and Polymorphism

Today’s concepts are the backbone of Spring Boot, microservices, Kafka consumers, cloud services, and AI-agent systems.

```text
Interface    → contract: what a component can do
Abstract class → shared base behavior
Inheritance  → a child class reuses a parent class
Polymorphism → one interface, many implementations
```

## 1. Why this matters in real systems

An AI application may support multiple capabilities:

```text
RAG capability       → answers from documents
Agent capability     → performs multi-step tool workflows
SQL capability       → queries a database safely
```

All can follow one shared contract:

```java
String execute(String request);
```

Your application does not need to know every internal implementation. It just calls `execute()`.

That is how Spring Boot commonly works: a controller depends on an interface, and Spring provides a concrete service implementation later.

## 2. Add the Day 3 source folder to VS Code settings

Open Workspace Settings JSON and add this line to `java.project.sourcePaths`:

```json
"lessons/day-03-java-oop/src/main/java"
```

Your full settings should now be:

```json
{
  "java.project.sourcePaths": [
    "hello-java/src/main/java",
    "lessons/day-01-java-basics/src/main/java",
    "lessons/day-02-java-collections/src/main/java",
    "lessons/day-03-java-oop/src/main/java"
  ],
  "java.debug.settings.console": "internalConsole"
}
```

Save, then run **Developer: Reload Window**.

## 3. Create this structure

```text
lessons/
└── day-03-java-oop/
    └── src/
        └── main/
            └── java/
                └── com/
                    └── hawk/
                        └── learning/
                            ├── AiCapability.java
                            ├── BaseAiCapability.java
                            ├── RagCapability.java
                            ├── AgentCapability.java
                            └── Day03App.java
```

All files use:

```java
package com.hawk.learning;
```

## 4. Interface — the contract

Create `AiCapability.java`:

```java
package com.hawk.learning;

public interface AiCapability {
    String getName();

    String execute(String request);
}
```

Any class that implements this interface promises to provide both methods.

## 5. Abstract class — shared behavior

Create `BaseAiCapability.java`:

```java
package com.hawk.learning;

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

- `abstract` means this class is incomplete; you cannot create it directly with `new`.
- `protected` means child classes can use the method, but unrelated classes cannot.
- Every AI capability shares `name` and request validation.

## 6. RAG implementation

Create `RagCapability.java`:

```java
package com.hawk.learning;

public class RagCapability extends BaseAiCapability {
    public RagCapability() {
        super("RAG Capability");
    }

    @Override
    public String execute(String request) {
        String cleanedRequest = validateAndCleanRequest(request);

        return "RAG result: searched approved documents for: "
                + cleanedRequest;
    }
}
```

`extends` means `RagCapability` inherits from `BaseAiCapability`.

`super("RAG Capability")` calls the parent constructor.

## 7. AI-agent implementation

Create `AgentCapability.java`:

```java
package com.hawk.learning;

public class AgentCapability extends BaseAiCapability {
    public AgentCapability() {
        super("Agent Capability");
    }

    @Override
    public String execute(String request) {
        String cleanedRequest = validateAndCleanRequest(request);

        return "Agent result: created a plan and selected tools for: "
                + cleanedRequest;
    }
}
```

Both classes implement the same contract, but each behaves differently.

## 8. Polymorphism in action

Create `Day03App.java`:

```java
package com.hawk.learning;

import java.util.List;

public class Day03App {
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

This line is polymorphism:

```java
List<AiCapability> capabilities
```

The list stores different concrete objects (`RagCapability`, `AgentCapability`) as the common interface type `AiCapability`.

At runtime, Java calls the correct `execute()` implementation for each object.

## 9. Compile and run

### Windows PowerShell

```powershell
cd "$env:USERPROFILE\Documents\java-ai-mastery\lessons\day-03-java-oop"
javac -d out src\main\java\com\hawk\learning\AiCapability.java src\main\java\com\hawk\learning\BaseAiCapability.java src\main\java\com\hawk\learning\RagCapability.java src\main\java\com\hawk\learning\AgentCapability.java src\main\java\com\hawk\learning\Day03App.java
java -cp out com.hawk.learning.Day03App
```

### Mac Terminal

```zsh
cd ~/Documents/java-ai-mastery/lessons/day-03-java-oop
javac -d out src/main/java/com/hawk/learning/AiCapability.java src/main/java/com/hawk/learning/BaseAiCapability.java src/main/java/com/hawk/learning/RagCapability.java src/main/java/com/hawk/learning/AgentCapability.java src/main/java/com/hawk/learning/Day03App.java
java -cp out com.hawk.learning.Day03App
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

It must:

- Extend `BaseAiCapability`
- Return `"SQL Capability"` from its constructor through `super(...)`
- Implement `execute()`
- Return a message saying it would safely query an approved database
- Be added to the `capabilities` list in `Day03App`

Next: **Day 4 Java AI — exceptions, custom exceptions, validation, logging mindset, and reliable service behavior.**
