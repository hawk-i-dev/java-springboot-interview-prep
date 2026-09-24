# Day 5 Java AI — Generics, `Optional`, Lambdas, and Streams

**Same on Mac and Windows in STS.**

Today’s concepts process data cleanly—useful for AI documents, API results, Kafka events, database records, and RAG pipelines.

```text
List<AiDocument>
     ↓ stream()
filter approved documents
     ↓
map to titles
     ↓
collect/count/sum/find
```

## 1. Create the package

Create:

```text
com.hawk.javaai.day05
```

Create these files:

```text
AiDocument.java
Day05Streams.java
```

## 2. Generics

```java
List<AiDocument> documents
```

`List` is a generic type. It means this list accepts only `AiDocument` objects.

This prevents mistakes like:

```java
documents.add("Hello"); // Compile error
```

## 3. `AiDocument.java`

A `record` is a compact immutable data class. Java 17 supports records.

```java
package com.hawk.javaai.day05;

public record AiDocument(
        String id,
        String title,
        String category,
        int tokenCount,
        boolean approved
) {
    public AiDocument {
        if (id == null || id.isBlank()) {
            throw new IllegalArgumentException("Document ID cannot be blank.");
        }

        if (title == null || title.isBlank()) {
            throw new IllegalArgumentException("Document title cannot be blank.");
        }

        if (tokenCount < 0) {
            throw new IllegalArgumentException("Token count cannot be negative.");
        }
    }
}
```

A record automatically provides:

```java
document.id()
document.title()
document.category()
document.tokenCount()
document.approved()
```

## 4. `Day05Streams.java`

```java
package com.hawk.javaai.day05;

import java.util.List;
import java.util.Map;
import java.util.Optional;
import java.util.stream.Collectors;

public class Day05Streams {
    public static void main(String[] args) {
        List<AiDocument> documents = List.of(
                new AiDocument(
                        "doc-1",
                        "Spring Boot Basics",
                        "backend",
                        450,
                        true
                ),
                new AiDocument(
                        "doc-2",
                        "Kafka Event Design",
                        "microservices",
                        850,
                        true
                ),
                new AiDocument(
                        "doc-3",
                        "Unapproved Internal Draft",
                        "internal",
                        300,
                        false
                ),
                new AiDocument(
                        "doc-4",
                        "RAG Architecture",
                        "ai",
                        700,
                        true
                ),
                new AiDocument(
                        "doc-5",
                        "Cloud Deployment Guide",
                        "cloud",
                        600,
                        true
                )
        );

        List<AiDocument> approvedDocuments = documents.stream()
                .filter(AiDocument::approved)
                .toList();

        System.out.println("Approved documents:");

        approvedDocuments.forEach(document ->
                System.out.println("- " + document.title())
        );

        List<String> approvedTitles = documents.stream()
                .filter(AiDocument::approved)
                .map(AiDocument::title)
                .toList();

        System.out.println("\nApproved titles:");
        approvedTitles.forEach(System.out::println);

        int totalApprovedTokens = documents.stream()
                .filter(AiDocument::approved)
                .mapToInt(AiDocument::tokenCount)
                .sum();

        System.out.println(
                "\nTotal tokens in approved documents: "
                        + totalApprovedTokens
        );

        Map<String, Long> documentsByCategory = documents.stream()
                .filter(AiDocument::approved)
                .collect(Collectors.groupingBy(
                        AiDocument::category,
                        Collectors.counting()
                ));

        System.out.println("\nApproved documents by category:");
        documentsByCategory.forEach((category, count) ->
                System.out.println(category + ": " + count)
        );

        Optional<AiDocument> kafkaDocument = documents.stream()
                .filter(AiDocument::approved)
                .filter(document -> document.title().contains("Kafka"))
                .findFirst();

        String kafkaDocumentTitle = kafkaDocument
                .map(AiDocument::title)
                .orElse("No approved Kafka document found.");

        System.out.println("\nKafka document: " + kafkaDocumentTitle);
    }
}
```

## 5. Understand the stream pipeline

```java
documents.stream()
        .filter(AiDocument::approved)
        .map(AiDocument::title)
        .toList();
```

| Part | Meaning |
|---|---|
| `stream()` | Start processing the collection |
| `filter(...)` | Keep only matching values |
| `map(...)` | Transform each value |
| `toList()` | Produce a final list |

A lambda is a small function:

```java
document -> document.title().contains("Kafka")
```

It means: “receive one `document`, return whether its title contains Kafka.”

Method reference:

```java
AiDocument::approved
```

This is a shorter form of:

```java
document -> document.approved()
```

## 6. Why `Optional` matters

A search might not find a document.

Bad:

```java
AiDocument document = kafkaDocument.get();
```

This can crash if no value exists.

Safe:

```java
String title = kafkaDocument
        .map(AiDocument::title)
        .orElse("No approved Kafka document found.");
```

## 7. Run it in STS

Right-click:

```text
Day05Streams.java → Run As → Java Application
```

Expected important results:

```text
Approved documents: 4
Total tokens in approved documents: 2600
Kafka document: Kafka Event Design
```

## Senior-level rule

Streams are powerful, but do not force everything into a stream.

Use a normal `for` loop when logic has many steps, mutation, complicated error handling, or is harder to read as a stream.

## Day 5 challenge

Find the first approved document with at least `700` tokens.

Use:

```java
Optional<AiDocument>
```

Then print only its title. If no matching document exists, print:

```text
No large approved document found.
```

Next: **Day 6 Java AI — unit testing with JUnit, test design, assertions, and testing AI/business logic safely.**
