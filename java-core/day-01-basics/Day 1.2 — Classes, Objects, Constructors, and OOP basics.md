# Day 1.2 — Classes, Objects, Constructors, and OOP basics

A Java backend application is built from classes and objects.

## 1. What is a class?

A class is a blueprint or template.

For example, every employee can have:

- Name
- Employee ID
- Company
- Experience
- A behavior such as `introduce()`

```java
public class Employee {

    String name;
    int experience;
    String company;

    void introduce() {
        System.out.println(
            "I am " + name +
            ", with " + experience +
            " years of experience at " + company
        );
    }
}
```

`Employee` is a class. It defines what an employee object will contain and do.

---

## 2. What is an object?

An object is a real instance created from a class blueprint.

```java
Employee employee1 = new Employee();

employee1.name = "Hari";
employee1.experience = 7;
employee1.company = "Oracle";

employee1.introduce();
```

Output:

```text
I am Hari, with 7 years of experience at Oracle
```

Here:

```java
Employee employee1 = new Employee();
```

- `Employee`: class/type.
- `employee1`: variable that refers to the object.
- `new Employee()`: creates the object in memory.

You can create many objects from one class:

```java
Employee employee1 = new Employee();
Employee employee2 = new Employee();
```

Each object has its own data.

```java
employee1.name = "Hari";
employee2.name = "Ravi";
```

---

## 3. Fields and methods

A class normally has:

- **Fields**: data of the object.
- **Methods**: behavior/actions of the object.

```java
public class BankAccount {

    String accountHolder;
    double balance;

    void deposit(double amount) {
        balance = balance + amount;
    }

    void showBalance() {
        System.out.println("Balance: " + balance);
    }
}
```

Usage:

```java
BankAccount account = new BankAccount();

account.accountHolder = "Hari";
account.balance = 1000;

account.deposit(500);
account.showBalance();
```

Output:

```text
Balance: 1500.0
```

---

## 4. Constructor

A constructor initializes an object when `new` is used.

```java
public class Employee {

    String name;
    int experience;
    String company;

    public Employee(String name, int experience, String company) {
        this.name = name;
        this.experience = experience;
        this.company = company;
    }
}
```

Create an object:

```java
Employee employee = new Employee("Hari", 7, "Oracle");
```

The constructor:

```java
public Employee(String name, int experience, String company)
```

has:

- Same name as its class: `Employee`.
- No return type—not even `void`.
- Inputs called parameters.
- Code that sets initial values.

### What does `this` mean?

`this` refers to the current object.

```java
this.name = name;
```

- `this.name`: field belonging to the current object.
- `name`: value passed into the constructor.

Without `this`, Java cannot clearly distinguish the object field from the parameter when both have the same name.

---

## 5. Default constructor

If you do not write any constructor, Java gives a default no-argument constructor.

```java
public class Employee {
    String name;
}
```

This works:

```java
Employee employee = new Employee();
```

But if you create any constructor yourself:

```java
public Employee(String name) {
    this.name = name;
}
```

Java no longer creates the no-argument constructor automatically.

So this fails:

```java
Employee employee = new Employee(); // Compile error
```

unless you explicitly write one:

```java
public Employee() {
}
```

This is important later in Spring Boot and JPA/Hibernate, where frameworks may require a no-argument constructor.

---

## 6. Encapsulation

Encapsulation means protecting object data and allowing controlled access to it.

Bad design:

```java
public class BankAccount {
    public double balance;
}
```

Anyone can set an invalid balance:

```java
account.balance = -100000;
```

Better design:

```java
public class BankAccount {

    private String accountHolder;
    private double balance;

    public BankAccount(String accountHolder, double openingBalance) {
        this.accountHolder = accountHolder;
        this.balance = openingBalance;
    }

    public void deposit(double amount) {
        if (amount <= 0) {
            System.out.println("Deposit amount must be positive");
            return;
        }

        balance = balance + amount;
    }

    public boolean withdraw(double amount) {
        if (amount <= 0 || amount > balance) {
            return false;
        }

        balance = balance - amount;
        return true;
    }

    public double getBalance() {
        return balance;
    }
}
```

Usage:

```java
BankAccount account = new BankAccount("Hari", 1000);

account.deposit(500);

boolean withdrawn = account.withdraw(300);

System.out.println(account.getBalance()); // 1200.0
System.out.println(withdrawn);            // true
```

`private` means the field can be accessed only inside the same class.

This is one of the most important OOP concepts. The class controls its own valid state and business rules.

---

## 7. Access modifiers

| Modifier | Accessible from |
|---|---|
| `private` | Only inside the same class |
| No modifier | Same package |
| `protected` | Same package and child classes |
| `public` | Anywhere |

A general backend rule:

- Keep fields `private`.
- Expose only needed public methods.
- Do not create getters and setters automatically without thinking about whether they allow invalid state.

---

## 8. The four OOP pillars

You do not need to master all of these today, but know the meaning.

| Concept | Meaning | Example |
|---|---|---|
| Encapsulation | Protect data and rules | Private `balance`, controlled `withdraw()` |
| Inheritance | Child class reuses parent behavior | `Manager extends Employee` |
| Polymorphism | Same interface, different behavior | `Payment.process()` for card/UPI |
| Abstraction | Show essential behavior, hide internal complexity | `PaymentService.pay()` |

We have covered encapsulation today. Inheritance, polymorphism, interfaces, and abstraction come next.

---

## Practice task

Create a `Course` class:

```java
public class Course {
    // private fields:
    // title
    // durationInDays
    // completedDays

    // Constructor:
    // Course(String title, int durationInDays)

    // Methods:
    // studyOneDay()
    // getProgress()
    // isCompleted()
}
```

Expected behavior:

```java
Course course = new Course("Java Interview Preparation", 30);

course.studyOneDay();
course.studyOneDay();

System.out.println(course.getProgress());
System.out.println(course.isCompleted());
```

`studyOneDay()` must not allow `completedDays` to become greater than `durationInDays`.

When this is clear, Day 1.3 will cover **inheritance, method overriding, interfaces, abstraction, and polymorphism**—concepts used constantly in Spring Boot.
