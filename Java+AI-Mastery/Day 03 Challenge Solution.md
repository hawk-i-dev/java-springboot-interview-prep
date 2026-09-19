Excellent — your `SqlCapability` works correctly and proves you understand the Day 3 goal:

- `SqlCapability` extends `BaseAiCapability`
- It inherits shared validation
- It implements `execute()`
- It is stored as `AiCapability` in the same list as RAG and Agent implementations
- Java selects the correct `execute()` method at runtime: polymorphism

Your output confirms all three capabilities run correctly.

Use this slightly polished version in the actual file:

```java
package com.hawk.learning;

public class SqlCapability extends BaseAiCapability {
    public SqlCapability() {
        super("SQL Capability");
    }

    @Override
    public String execute(String request) {
        String cleanRequest = validateAndCleanRequest(request);

        return "SQL result: would query the approved database safely for: "
                + cleanRequest;
    }
}
```

And your list is correct:

```java
List<AiCapability> capabilities = List.of(
        new RagCapability(),
        new AgentCapability(),
        new SqlCapability()
);
```

