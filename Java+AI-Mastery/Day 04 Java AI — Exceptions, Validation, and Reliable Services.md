# Day 4 Java AI — Exceptions, Validation, and Reliable Services

Today you learn how a Java service handles invalid input safely.

```text
Invalid request
   ↓
Validate it
   ↓
Throw a clear exception
   ↓
Catch it at the application boundary
   ↓
Return a helpful message
```

This is essential for Spring Boot APIs, Kafka consumers, and AI-agent tools.

## 1. Create the package

Create:

```text
com.hawk.javaai.day04
```

Create these files:

```text
InvalidAiRequestException.java
UnsupportedCapabilityException.java
AiRequestService.java
Day04Exceptions.java
```

## 2. Custom validation exception

`InvalidAiRequestException.java`

```java
package com.hawk.javaai.day04;

public class InvalidAiRequestException extends RuntimeException {
    public InvalidAiRequestException(String message) {
        super(message);
    }
}
```

## 3. Custom unsupported-capability exception

`UnsupportedCapabilityException.java`

```java
package com.hawk.javaai.day04;

public class UnsupportedCapabilityException extends RuntimeException {
    public UnsupportedCapabilityException(String message) {
        super(message);
    }
}
```

Both extend `RuntimeException`, so they are unchecked exceptions. We use them for invalid business input.

## 4. Service with validation

`AiRequestService.java`

```java
package com.hawk.javaai.day04;

import java.util.Locale;
import java.util.logging.Logger;

public class AiRequestService {
    private static final Logger LOGGER =
            Logger.getLogger(AiRequestService.class.getName());

    public String process(String capability, String request) {
        validate(capability, request);

        String normalizedCapability = capability.trim()
                .toLowerCase(Locale.ROOT);

        String cleanRequest = request.trim();

        LOGGER.info(() -> "Processing request with capability: "
                + normalizedCapability);

        return switch (normalizedCapability) {
            case "rag" -> "RAG response: searched approved documents for: "
                    + cleanRequest;
            case "agent" -> "Agent response: created a safe tool plan for: "
                    + cleanRequest;
            case "sql" -> "SQL response: would query an approved database for: "
                    + cleanRequest;
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

## 5. Run valid and invalid requests safely

`Day04Exceptions.java`

```java
package com.hawk.javaai.day04;

public class Day04Exceptions {
    public static void main(String[] args) {
        AiRequestService service = new AiRequestService();

        runRequest(
                service,
                "rag",
                "Explain why Kafka is useful in microservices."
        );

        runRequest(
                service,
                "agent",
                "Create a plan to analyze monthly expenses."
        );

        runRequest(service, "rag", "   ");

        runRequest(
                service,
                "image-generator",
                "Create a cloud architecture."
        );
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
            System.out.println(
                    "Validation error: " + exception.getMessage()
            );

        } catch (UnsupportedCapabilityException exception) {
            System.out.println(
                    "Capability error: " + exception.getMessage()
            );

        } finally {
            System.out.println("Request processing finished.\n");
        }
    }
}
```

## 6. Understand `try`, `catch`, and `finally`

```java
try {
    // code that may fail
} catch (SpecificException exception) {
    // handle a known failure safely
} finally {
    // always runs, whether it succeeds or fails
}
```

Never silently ignore errors:

```java
catch (Exception exception) {
    // Do not leave this empty.
}
```

It hides real bugs and makes production failures hard to diagnose.

## 7. Run in STS

Right-click:

```text
Day04Exceptions.java → Run As → Java Application
```

You should see:

- Successful RAG request
- Successful Agent request
- Validation error for blank request
- Capability error for unsupported `image-generator`
- “Request processing finished” after every request

## Day 4 challenge

Add support for:

```text
summarizer
```

Requirements:

- Add a `case "summarizer"` in `AiRequestService`.
- Return a summary-style response.
- Do not add a new `catch` block.
- Test it by calling:

```java
runRequest(
        service,
        "summarizer",
        "Summarize the benefits of Spring Boot."
);
```

Next: **Day 5 Java AI — generics, `Optional`, lambdas, streams, and clean data processing.**
