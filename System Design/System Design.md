## OOP

OOP is a programming style, not a tool, so despite being old, it’s vastly popular and established. This programming style involves dividing a program into pieces of objects that can communicate with each other. Every object has its own unique set of properties. These properties are later accessed and modified through the use of various operations.

The following are the essential concepts of object-oriented programming:

- Attributes
- Methods
- Classes
- Objects

The following are the four principles of object-oriented programming:

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

## Data hiding

Data hiding is an essential concept in object-oriented programming. In simple terms, it can be defined as masking a class's internal operations and only providing an interface through which other entities can interact with the class without being aware of what is happening within.

Data hiding can be divided into two primary components:

- Encapsulation
- Abstraction

### Encapsulation

Encapsulation is a fundamental programming technique used to achieve data hiding in OOP. Encapsulation in OOP refers to binding data and the methods to manipulate that data together in a single unit—class.

### Abstraction

**Abstraction** is a technique used in object-oriented programming that simplifies the program's structure. It focuses only on revealing the necessary details of a system and hiding irrelevant information to minimize its complexity. In simpler words, we can say that it means to show what an object does and hides how it does it.


| **Abstraction**                                                                | **Encapsulation**                                                   |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| It focuses on the design level of the system.                                  | It focuses on the application level of the system.                  |
| It hides unnecessary data to simplify the structure.                           | It restricts access to data to prevent its misuse.                  |
| It highlights the work that the object performs.                               | It deals with the internal working of the object.                   |
| Abstraction means to hide implementation using interface and abstract classes. | Encapsulation means to hide data using getter and setter functions. |

## Inheritance

## Definition

**Inheritance** provides a way to create a new class from an existing class. The new class is a specialized version of the existing class such that it inherits all the public attributes (variables) and methods of the existing class. The existing class is used as a starting point or base to create the new class.

## IS-A relationship
Wherever we come across an IS-A relationship between objects, we can use inheritance.
eg. Dog IS-A Animal, Square IS-A Shape

## Types of inheritance

Based on parent classes and child classes, there are _five_ types of inheritance in general, which are explained below.

### Single inheritance
In single inheritance, there is only a single class extending from a single parent class.

**Example:**

- A fuel car IS-A vehicle

### Multiple inheritance

When a class is derived from more than one base class, i.e., when a class has more than one immediate parent class, it is called multiple inheritance.

**Example:**

- The hybrid car IS-A fuel car.
    
- The hybrid car IS-A electric car as well.

Java does not support Multiple inheritance via classes

### Multi-level inheritance

When a class is derived from a class that itself is derived from another class, it is called multi-level inheritance. We can extend the classes to as many levels as we want.

**Example:**

- A fuel car IS-A vehicle
    
- A gasoline car IS-A fuel car

 

###  Hierarchical inheritance

In hierarchical inheritance, more than one class extends, as per the requirement of the design, from the same base class. The common attributes of these child classes are implemented inside the base class.



### Hybrid inheritance

A type of inheritance that is a combination of more than one type of inheritance is called **hybrid inheritance**.


## Polymorphism


The word **polymorphism** is a combination of two Greek words, “poly” meaning many, and “morph” meaning forms. In programming, polymorphism is a phenomenon that allows an object to have several different forms and behaviors.

For example, take the `Animal` class. There are many different animals, e.g., lion, deer, dog, and crocodile, etc. So, they are all animals, but their properties are different. The animal class can have a method, `makeNoise`. Its implementation should be different for a lion, deer, or any other animal as they all have different noises. This is called polymorphism.

### Types of Polymorphism

- Compile-time polymorphism(Static polymorphism)
- Runtime polymorphism(Dynamic polymorphism)


### Dynamic polymorphism

**Dynamic** **polymorphism** is the mechanism that defines the methods with the same name, return type, and parameters in the base class and derived classes. Hence, the call to an overridden method is decided at runtime. That is why dynamic polymorphism is also known as **runtime** **polymorphism**. It is achieved by method overriding.

#### Method overriding 

In object-oriented programming, if a subclass provides a specific implementation of a method that had already been defined in one of its parent classes, it is known as **method overriding**.


### Static polymorphism

**Static** **polymorphism** is also known as compile-time polymorphism, and it is achieved by method overloading or operator overloading.

#### Method overloading

Methods are said to be **overloaded** if a class has more than one method with the same name, but either the number of arguments is different, or the type of arguments is different. We have implemented method overloading using two functions with the same name but with different numbers of arguments. You can see this in the implementation below.

| **Static Polymorphism**                                                            | **Dynamic Polymorphism**                                                                              |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Polymorphism that is resolved during compile-time is known as static polymorphism. | Polymorphism that is resolved during runtime is known as dynamic polymorphism.                        |
| Method overloading is used in static polymorphism.                                 | Method overriding is used in dynamic polymorphism.                                                    |
| Mostly used to increase the readability of the code.                               | Mostly used to have a separate implementation for a method that is already defined in the base class. |
| Arguments must be different in the case of overloading.                            | Arguments must be the same in the case of overriding.                                                 |
| Return type of the method does not matter.                                         | Return type of the method must be the same.                                                           |
| Private and sealed methods can be overloaded.                                      | Private and sealed methods cannot be overridden.                                                      |
| Gives better performance because the binding is being done at compile-time.        | Gives worse performance because the binding is being done at runtime.                                 |
# [[Object-oriented Analysis and Design (OOAD)]]

