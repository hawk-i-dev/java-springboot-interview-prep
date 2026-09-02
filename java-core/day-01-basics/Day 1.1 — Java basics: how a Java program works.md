Absolutely. We’ll build from first principles, then move gradually to interview-level depth. No gaps, no assumptions.

# Day 1.1 — Java basics: how a Java program works

## 1. What is Java?

Java is a programming language used to build backend applications, APIs, enterprise systems, Android applications, and microservices.

A Java program is written once and can run on different operating systems because of the JVM.

```text
Java source code (.java)
        ↓
Java compiler (javac)
        ↓
Bytecode (.class)
        ↓
JVM runs the bytecode
        ↓
Application runs on Windows / Mac / Linux
```

Important terms:

- **JDK**: Java Development Kit. Used to write, compile, and run Java.
- **JRE**: Java Runtime Environment. Components needed to run Java programs.
- **JVM**: Java Virtual Machine. Executes compiled Java bytecode.
- **Bytecode**: Intermediate code created after compilation.

Interview one-liner:

> Java is platform-independent at the bytecode level: Java source is compiled to bytecode, and the JVM for each operating system executes that bytecode.

---

## 2. Your first Java program

```java
public class HelloWorld {

    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

Explanation:

- `public class HelloWorld`: creates a class named `HelloWorld`.
- A Java file containing this public class must be named `HelloWorld.java`.
- `main(...)`: the starting point of the program.
- `System.out.println(...)`: prints a line to the console.

```java
public static void main(String[] args)
```

Break it down:

- `public`: JVM can access this method.
- `static`: JVM can call it without creating an object.
- `void`: the method returns no value.
- `main`: special method name where the program begins.
- `String[] args`: command-line inputs passed to the program.

---

## 3. Variables: storing data

A variable is a named location for storing a value.

```java
int experience = 7;
String company = "Oracle";
double salary = 12.5;
boolean isPreparingForInterview = true;
```

Common data types:

| Type | Stores | Example |
|---|---|---|
| `int` | Whole numbers | `int age = 28;` |
| `long` | Large whole numbers | `long accountId = 123456789L;` |
| `double` | Decimal numbers | `double rating = 4.8;` |
| `boolean` | True/false | `boolean active = true;` |
| `char` | One character | `char grade = 'A';` |
| `String` | Text | `String name = "Hari";` |

Use `String` for text, even if it contains digits:

```java
String phoneNumber = "9876543210";
String employeeId = "EMP-123";
```

Do not use `double` for money because of precision issues. In real backend applications use `BigDecimal`.

---

## 4. Operators

Operators perform calculations or comparisons.

```java
int a = 10;
int b = 3;

System.out.println(a + b); // 13
System.out.println(a - b); // 7
System.out.println(a * b); // 30
System.out.println(a / b); // 3
System.out.println(a % b); // 1, remainder
```

Comparison operators return `true` or `false`:

```java
int experience = 7;

System.out.println(experience > 5);   // true
System.out.println(experience == 7);  // true
System.out.println(experience != 10); // true
```

Important difference:

```java
// Assigns a value
int age = 25;

// Compares values
age == 25
```

---

## 5. Conditions: making decisions

Use `if` when code should run only under a condition.

```java
int experience = 7;

if (experience >= 5) {
    System.out.println("Eligible for senior roles");
} else {
    System.out.println("Build more experience");
}
```

Use `else if` for multiple conditions:

```java
int score = 85;

if (score >= 90) {
    System.out.println("Excellent");
} else if (score >= 60) {
    System.out.println("Good");
} else {
    System.out.println("Needs improvement");
}
```

---

## 6. Loops: repeating work

A `for` loop repeats a known number of times.

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Day " + i);
}
```

Output:

```text
Day 1
Day 2
Day 3
Day 4
Day 5
```

A `while` loop runs while a condition is true.

```java
int attempt = 1;

while (attempt <= 3) {
    System.out.println("Attempt: " + attempt);
    attempt++;
}
```

---

## 7. Methods: reusable blocks of code

A method performs a specific task.

```java
public static void greet() {
    System.out.println("Welcome to Java");
}
```

Call it from `main`:

```java
public static void main(String[] args) {
    greet();
}
```

A method can accept input:

```java
public static void greet(String name) {
    System.out.println("Welcome, " + name);
}
```

```java
greet("Hari");
```

A method can return a value:

```java
public static int add(int firstNumber, int secondNumber) {
    return firstNumber + secondNumber;
}
```

```java
int total = add(10, 20);
System.out.println(total); // 30
```

---

## Today’s small practice

Create a class named `InterviewPreparation` and write a program that:

1. Stores your name, years of experience, and current company.
2. Prints them.
3. Checks whether experience is at least 5 years.
4. Uses a loop to print `Preparing day 1` through `Preparing day 7`.
5. Creates an `add` method that accepts two numbers and returns their total.

Expected style:

```java
public class InterviewPreparation {

    public static void main(String[] args) {
        // Your code here
    }

    public static int add(int firstNumber, int secondNumber) {
        // Your code here
    }
}
```

Once you understand this, Day 1.2 will cover **classes, objects, constructors, and OOP**—the most important basic Java foundation for Spring Boot.
