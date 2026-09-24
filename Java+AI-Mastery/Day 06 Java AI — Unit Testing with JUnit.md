# Day 6 Java AI — Unit Testing with JUnit

Today you learn how to test Java business logic automatically.

```text
Production code → src/main/java
Test code       → src/test/java
```

A test checks that your code behaves correctly before users find bugs.

## 1. Verify JUnit is available

Open `pom.xml`. Your Spring Boot project should already include:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

Do not add it again if it already exists.

## 2. Create production classes

Under:

```text
src/main/java
```

Create package:

```text
com.hawk.javaai.day06
```

Create `AiKnowledgeDocument.java`:

```java
package com.hawk.javaai.day06;

public record AiKnowledgeDocument(
        String title,
        int tokenCount,
        boolean approved
) {
}
```

Create `AiKnowledgeBaseService.java`:

```java
package com.hawk.javaai.day06;

import java.util.List;
import java.util.Optional;

public class AiKnowledgeBaseService {

    public Optional<AiKnowledgeDocument> findFirstLargeApprovedDocument(
            List<AiKnowledgeDocument> documents,
            int minimumTokenCount
    ) {
        if (minimumTokenCount < 0) {
            throw new IllegalArgumentException(
                    "Minimum token count cannot be negative."
            );
        }

        return documents.stream()
                .filter(AiKnowledgeDocument::approved)
                .filter(document ->
                        document.tokenCount() >= minimumTokenCount
                )
                .findFirst();
    }

    public int countApprovedDocuments(
            List<AiKnowledgeDocument> documents
    ) {
        return (int) documents.stream()
                .filter(AiKnowledgeDocument::approved)
                .count();
    }
}
```

## 3. Create the test class

Under:

```text
src/test/java
```

Create the same package:

```text
com.hawk.javaai.day06
```

Create `AiKnowledgeBaseServiceTest.java`:

```java
package com.hawk.javaai.day06;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertThrows;
import static org.junit.jupiter.api.Assertions.assertTrue;

import java.util.List;
import java.util.Optional;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

class AiKnowledgeBaseServiceTest {

    private AiKnowledgeBaseService service;
    private List<AiKnowledgeDocument> documents;

    @BeforeEach
    void setUp() {
        service = new AiKnowledgeBaseService();

        documents = List.of(
                new AiKnowledgeDocument(
                        "Spring Boot Basics",
                        400,
                        true
                ),
                new AiKnowledgeDocument(
                        "Kafka Event Design",
                        850,
                        true
                ),
                new AiKnowledgeDocument(
                        "Unapproved Draft",
                        1000,
                        false
                )
        );
    }

    @Test
    void findsFirstLargeApprovedDocument() {
        Optional<AiKnowledgeDocument> result =
                service.findFirstLargeApprovedDocument(documents, 700);

        assertTrue(result.isPresent());
        assertEquals("Kafka Event Design", result.orElseThrow().title());
    }

    @Test
    void returnsEmptyWhenNoLargeApprovedDocumentExists() {
        Optional<AiKnowledgeDocument> result =
                service.findFirstLargeApprovedDocument(documents, 2000);

        assertTrue(result.isEmpty());
    }

    @Test
    void countsOnlyApprovedDocuments() {
        int approvedCount = service.countApprovedDocuments(documents);

        assertEquals(2, approvedCount);
    }

    @Test
    void rejectsNegativeMinimumTokenCount() {
        assertThrows(
                IllegalArgumentException.class,
                () -> service.findFirstLargeApprovedDocument(
                        documents,
                        -1
                )
        );
    }
}
```

## 4. The testing pattern: Arrange, Act, Assert

```text
Arrange → prepare data and objects
Act     → call the method being tested
Assert  → verify the result
```

Example:

```java
// Arrange
AiKnowledgeBaseService service = new AiKnowledgeBaseService();

// Act
int approvedCount = service.countApprovedDocuments(documents);

// Assert
assertEquals(2, approvedCount);
```

## 5. Run tests in STS

Right-click:

```text
AiKnowledgeBaseServiceTest.java
```

Then choose:

```text
Run As → JUnit Test
```

You should see:

```text
Runs: 4
Failures: 0
Errors: 0
```

## Terminal commands

### Mac

```zsh
cd ~/Documents/java-ai-sts-workspace/java-ai-lab
./mvnw test
```

### Windows PowerShell

```powershell
cd "$env:USERPROFILE\Documents\java-ai-sts-workspace\java-ai-lab"
.\mvnw.cmd test
```

## Important AI-engineering rule

Unit tests should not call a real LLM, paid API, live database, or Kafka broker.

Use fixed fake data in unit tests. Later, we will learn mocks, integration tests, Testcontainers, and separate tests for real integrations.

## Day 6 challenge

Add a method to `AiKnowledgeBaseService`:

```java
public int calculateTotalApprovedTokens(
        List<AiKnowledgeDocument> documents
)
```

It must return the sum of token counts for approved documents only.

Then add two JUnit tests:

1. Returns the correct total for the current documents.
2. Returns `0` when every document is unapproved.

Next: **Day 7 Java AI — Maven deeply: dependencies, project lifecycle, build, test, package, and executable JAR files.**
