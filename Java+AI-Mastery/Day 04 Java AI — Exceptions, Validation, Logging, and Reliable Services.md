# Day 4 Java AI — Exceptions, Validation, Logging, and Reliable Services

Today you learn how a professional Java service handles bad input without crashing.

```text
Bad request
   ↓
Validation
   ↓
Custom exception
   ↓
Catch at application boundary
   ↓
Clear error response + useful log
```

This is exactly what Spring Boot APIs, Kafka consumers, AI agents, and cloud services need.

## 1. Core idea

Do not let invalid data silently continue.

```java
if (request == null || request.isBlank()) {
    throw new InvalidAiRequestException("Request cannot be blank.");
}
```

`throw` stops the current operation and sends a clear failure signal.

## 2. Checked vs unchecked exceptions

| Type | Example | Use |
|---|---|---|
| Checked exception | `IOException` | Caller must handle/declare it |
| Unchecked exception | `IllegalArgumentException`, `RuntimeException` | Invalid data or programming/business-rule failures |

For validation failures in our web services, we commonly use custom **unchecked** exceptions extending `RuntimeException`.

## 3. Add Day 4 to VS Code source paths

Add this to the `java.project.sourcePaths` list:

```json
"lessons/day-04-java-exceptions/src/main/java"
```

## 4. Create this structure

```text
lessons/
└── day-04-java-exceptions/
    └── src/main/java/com/hawk/learning/
        ├── InvalidAiRequestException.java
        ├── UnsupportedCapabilityException.java
        ├── AiRequestService.java
        └── Day04App.java
```

## File 1 — `InvalidAiRequestException.java`

```java
package com.hawk.learning;

public class InvalidAiRequestException extends RuntimeException {
    public InvalidAiRequestException(String message) {
        super(message);
    }
}
```

## File 2 — `UnsupportedCapabilityException.java`

```java
package com.hawk.learning;

public class UnsupportedCapabilityException extends RuntimeException {
    public UnsupportedCapabilityException(String message) {
        super(message);
    }
}
```

## File 3 — `AiRequestService.java`

```java
package com.hawk.learning;

import java.util.Locale;
import java.util.logging.Logger;

public class AiRequestService {
    private static final Logger LOGGER =
            Logger.getLogger(AiRequestService.class.getName());

    public String process(String capability, String request) {
        validate(capability, request);

        String normalizedCapability = capability.trim().toLowerCase(Locale.ROOT);
        String cleanedRequest = request.trim();

        LOGGER.info(() -> "Processing AI request using capability: "
                + normalizedCapability);

        return switch (normalizedCapability) {
            case "rag" -> "RAG response: searched approved documents for: "
                    + cleanedRequest;
            case "agent" -> "Agent response: created a safe tool plan for: "
                    + cleanedRequest;
            case "sql" -> "SQL response: would query an approved database for: "
                    + cleanedRequest;
            default -> throw new UnsupportedCapabilityException(
                    "Unsupported capability: " + capability
            );
        };
    }

    private void validate(String capability, String request) {
        if (capability == null || capability.isBlank()) {
            throw new InvalidAiRequestException(
                    "Capability cannot be blank. Use rag, agent, or sql."
            );
        }

        if (request == null || request.isBlank()) {
            throw new InvalidAiRequestException(
                    "AI request cannot be blank."
            );
        }
    }
}
```

## File 4 — `Day04App.java`

```java
package com.hawk.learning;

import java.util.logging.Logger;

public class Day04App {
    private static final Logger LOGGER =
            Logger.getLogger(Day04App.class.getName());

    public static void main(String[] args) {
        AiRequestService service = new AiRequestService();

        runRequest(
                service,
                "rag",
                "Explain why Kafka is useful in microservices."
        );

        runRequest(service, "agent", "Create a plan to analyze expenses.");

        runRequest(service, "rag", "   ");

        runRequest(service, "image-generator", "Create a cloud architecture.");
    }

    private static void runRequest(
            AiRequestService service,
            String capability,
            String request
    ) {
        try {
            String result = service.process(capability, request);
            System.out.println("Success: " + result);
        } catch (InvalidAiRequestException exception) {
            LOGGER.warning("Validation failed: " + exception.getMessage());
            System.out.println("Request rejected: " + exception.getMessage());
        } catch (UnsupportedCapabilityException exception) {
            LOGGER.warning("Capability failed: " + exception.getMessage());
            System.out.println("Request rejected: " + exception.getMessage());
        } finally {
            System.out.println("Request processing finished.\n");
        }
    }
}
```

## What `try`, `catch`, and `finally` mean

```java
try {
    // Code that may fail
} catch (SpecificException exception) {
    // Recover or return a useful error
} finally {
    // Runs whether it succeeds or fails
}
```

Do not do this in professional applications:

```java
catch (Exception exception) {
    // ignore it
}
```

Ignoring an exception hides the root cause and creates difficult production bugs.

## Run it

### Windows PowerShell

```powershell
cd "$env:USERPROFILE\Documents\java-ai-mastery\lessons\day-04-java-exceptions"
javac -d out src\main\java\com\hawk\learning\InvalidAiRequestException.java src\main\java\com\hawk\learning\UnsupportedCapabilityException.java src\main\java\com\hawk\learning\AiRequestService.java src\main\java\com\hawk\learning\Day04App.java
java -cp out com.hawk.learning.Day04App
```

### Mac Terminal

```zsh
cd ~/Documents/java-ai-mastery/lessons/day-04-java-exceptions
javac -d out src/main/java/com/hawk/learning/InvalidAiRequestException.java src/main/java/com/hawk/learning/UnsupportedCapabilityException.java src/main/java/com/hawk/learning/AiRequestService.java src/main/java/com/hawk/learning/Day04App.java
java -cp out com.hawk.learning.Day04App
```

## Day 4 challenge

Add support for a `"summarizer"` capability.

It must:

- Return a summary-style response for valid requests.
- Reject unknown capability names.
- Reject blank requests.
- Run through the same `try/catch/finally` flow without adding a new `catch` block.

Next: **Day 5 Java AI — generics, `Optional`, streams, lambdas, and clean data processing for APIs and AI pipelines.**
