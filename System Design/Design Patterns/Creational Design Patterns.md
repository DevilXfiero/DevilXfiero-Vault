# 🏭 FACTORY PATTERNS — COMPLETE & CLEAR GUIDE

## There are **4 commonly discussed factory styles**:

1. **Simple Factory** (NOT a GoF pattern)
2. **Factory Method** ✅ (GoF)
3. **Abstract Factory** ✅ (GoF)
4. **Static Factory Method** (Java-style, not GoF)


---

# 1️⃣ Simple Factory (NOT a Design Pattern)

⚠️ Important: **This is NOT an official GoF pattern**, but interviewers still mention it.

## 🔹 Problem it solves

- Centralizes object creation
- Avoids `new` scattered everywhere

## 🔹 Example

```java
class NotificationFactory {      
public static Notification create(String type) {         
if (type.equals("EMAIL")) return new EmailNotification();         
if (type.equals("SMS")) return new SmsNotification();         
throw new IllegalArgumentException("Unknown type");     } 
}
```


## ❌ Problems

- Violates **Open/Closed Principle**
- Every new type modifies factory
- Grows into big `if-else`
    

## 🧠 Interview line

> “Simple Factory is okay for small, stable systems but doesn’t scale well.”

---

# 2️⃣ Factory Method (GoF Pattern) ✅

## 🔹 Core idea

> **Let subclasses decide which object to create**

Creation is **polymorphic**, not conditional.

---

## 🔹 Example

### Product

`interface Notification {     void send(); }`

### Factory

`interface NotificationFactory {     Notification create(); }`

### Concrete Factory

`class EmailFactory implements NotificationFactory {     public Notification create() {         return new EmailNotification();     } }`

### Client

```java
NotificationFactory factory = new EmailFactory(); 
Notification notification = factory.create(); notification.send();
```


## ✅ Advantages

- Open for extension
- No `if-else`
- Runtime substitution
    

## 🧠 Interview line

> “Factory Method solves the problem of growing conditional creation logic.”

---

# 3️⃣ Abstract Factory (GoF Pattern) ✅

This is where **most candidates get confused**.

## 🔹 Core idea

> **Factory of factories**

Creates **families of related objects**, not just one.

---

## 🔹 When you NEED Abstract Factory

When:

- Objects must be used **together**
- Variants must stay **consistent**


Example:

- UI themes (Windows / Mac)
- Cloud providers (AWS / GCP)
- Databases (MySQL / Mongo)

---

## 🔹 Example: UI Toolkit

### Products

`interface Button {} interface Checkbox {}`

### Abstract Factory

`interface UIFactory {     Button createButton();     Checkbox createCheckbox(); }`

### Concrete Factory

`class WindowsUIFactory implements UIFactory {     public Button createButton() { return new WindowsButton(); }     public Checkbox createCheckbox() { return new WindowsCheckbox(); } }`

### Client

`UIFactory factory = new WindowsUIFactory(); Button btn = factory.createButton(); Checkbox cb = factory.createCheckbox();`

## ✅ Benefits

- Guarantees compatible objects
- Enforces consistency
- Easy to switch families
    

## 🧠 Interview line

> “Abstract Factory ensures that related objects are created together correctly.”

---

# 4️⃣ Static Factory Method (Java-style)

This is **not GoF**, but **VERY common in Java interviews**.

## 🔹 Example

```java
class Expense {      
public static Expense createEqual(...) { ... }     
public static Expense createExact(...) { ... } 
}
```

## ✅ Benefits

- Clear naming
- Validation inside
- No extra factory class
- Encapsulation
    

## ❌ Limitation

- No polymorphic override
- Cannot be replaced at runtime
    

## 🧠 Interview line

> “Static factories are great for simple creation logic but lack polymorphism.”

---

# 🧠 VERY IMPORTANT INTERVIEW COMPARISON TABLE

|Pattern|What it creates|Key Use Case|
|---|---|---|
|Simple Factory|One object|Small systems|
|Factory Method|One object|Extensible creation|
|Abstract Factory|Related objects|Consistent families|
|Static Factory|One object|Clean APIs|

---

# 🎯 INTERVIEW TRAP QUESTIONS (READ CAREFULLY)


### ❓ Can Abstract Factory use Factory Method internally?

✅ YES  
This is a **great bonus answer**.

---

### ❓ Where did you use these in your work?

Your answers:

- **Splitwise** → Static Factory Method
- **Notification System** → Factory Method
- **UI / Cloud Provider** → Abstract Factory
    

---

# 🧠 FINAL TAKEAWAY (MEMORIZE)

> - Use **Simple Factory** for small problems
> - Use **Factory Method** when creation logic grows
> - Use **Abstract Factory** when objects must work together
> - Use **Static Factory** for clean APIs



## 5️⃣ Builder Pattern

### Intent
Construct complex immutable objects step by step.

### Problem It Solves

- Telescoping constructors
- Unsafe setters
- Poor readability
    

### Core Idea

> Separate **construction** from **final object**.

### When to Use

- Mandatory + optional fields
- Immutability required
- Validation needed
    

### When NOT to Use

- Simple objects
    
- Few fields
    

### Minimal Code Example

```java
class Expense {
    private final User paidBy;
    private final double amount;
    private final String description;

    private Expense(Builder b) {
        this.paidBy = b.paidBy;
        this.amount = b.amount;
        this.description = b.description;
    }

    static class Builder {
        private final User paidBy;
        private final double amount;
        private String description;

        Builder(User paidBy, double amount) {
            this.paidBy = paidBy;
            this.amount = amount;
        }

        Builder description(String desc) {
            this.description = desc;
            return this;
        }

        Expense build() {
            if (amount <= 0) throw new IllegalArgumentException();
            return new Expense(this);
        }
    }
}

```

### Usage


```java
Expense e = new Expense.Builder(user, 500)
        .description("Dinner")
        .build();
```

### Pros / Cons

**Pros**
- Immutable objects
- Clean APIs

**Cons**
- Boilerplate
- Overkill for simple cases
    

### Real Usage

- Splitwise Expense
- HTTP Requests
- Config objects