

- In the **Single Responsibility Principle (SRP)**, each class should be responsible for a single part or functionality of the system.

- In the **Open Closed principle (OCP)**, software components should be open for extension but closed for modification.

- In the **Liskov Substitution Principle (LSP)**, objects of a superclass should be replaceable with objects of its subclasses without breaking the system.

 - The **Interface Segregation Principle (ISP)** makes fine-grained interfaces that are client specific.

- The **Dependency Inversion Principle (DIP)**, ensures that the high-level modules are not dependent on low-level modules. In other words, one should depend upon abstraction and not concretion.

## Single Responsibility Principle

The **Single Responsibility Principle (SRP)** is perhaps the least understood of the SOLID concepts. The term was coined by Robert C. Martin who defines the SRP in the following way, "_A class should have only one reason to change_." This implies that any class or component in our code should only have one functionality. Everything in the class should be related to just one goal.

![[Pasted image 20241005220137.png]]


## Open Closed Principle
In 1988, Bertrand Meyer defined the **Open Closed Principle (OCP)** in the following way, “A software artifact should be open for extension but closed for modification.” This means that a system should improve easily by adding new code instead of changing the code core. This way, the core code always retains its unique identity, making it reusable.

One might think of OCP as inheritance, but remember that inheritance is only one of the OCP techniques. We use the interface because it is open for extension and closed for modification. Therefore, OCP is also defined as **polymorphic OCP.**

![[Pasted image 20241005220206.png]]


## Liskov Substitution Principle

The Liskov Substitution Principle (LSP) is one of the fundamental design principles of object-oriented design. The LSP helps guide the use of inheritance in design so that the application does not break. It states that the objects of a subclass should behave the same way as the objects of the superclass, such that they are replaceable. This rule generally applies to abstraction concepts like inheritance and polymorphism.

![[Pasted image 20241005220938.png]]


## Interface Segregation Principle

The **Interface Segregation Principle (ISP)** is a design principle that does not recommend having methods that an interface would not use and require. Therefore, it goes against having fat interfaces in classes and prefers having small interfaces with a group of methods, each serving a particular purpose.

![[Pasted image 20241005221237.png]]


## Dependency Inversion Principle 

The **Dependency Inversion Principle (DIP)** states that high-level modules should not depend on low-level modules, but rather both should depend on abstractions. The abstractions should not depend on details. Instead, the details should depend on abstractions.

![[Pasted image 20241005221521.png]]


![[Pasted image 20241005221542.png]]


