

## Class

```java
public class Cat {  
  
private String name;  
private Integer age;  
private String color;  
  
public Cat(String name, Integer age, String color) {  
this(name, age); // the inside constructor  
this.color = color;  
}  
public Cat(String name, Integer age) {  
this.name = name;  
this.age = age;  
}  
  
public Cat(String name) {  
this.name = name;  
}  
public void meow() {  
System.out.println(name + ": meow...");  
}  
public void setName(String name) {  
this.name = name;  
}  
  
public String getName() {  
return this.name;  
}  
  
@Override  
public String toString() {  
return "Cat{" +  
"name='" + name + '\'' +  
", age=" + age +  
", color='" + color + '\'' +  
'}';  
}  
}
```


# Everything in Java is an Object

Object class is parent of all objects.


## @Override
It's  for readability to tell that method has overridden from parent class.


Comparing objects with ==

```java
Cat rose1 = new Cat("Rose");  
Cat rose2 = new Cat("Rose");  
  
System.out.println(rose1 == rose2); // false
System.out.println(rose1.equals(rose2)); // false
```

False because values are same but == perform equality on what is stored in stack i.e the reference of the object which is different for both the object.

In case of equals result will be false because it uses equals method of Object class which is parent for all the objects and in objects following statement is used for comparison this == obj
which again uses == so this also compare by reference.


We have to override equal method of parent class to implement custom equal check for the class.

```java
@Override  
public boolean equals(Object o) {  
if (this == o) return true;  
if (o == null || getClass() != o.getClass()) return false;  
Cat cat = (Cat) o;  
return Objects.equals(name, cat.name) && Objects.equals(age, cat.age) && Objects.equals(color, cat.color);  
}
```


POJO - Plain old java object
Object have no association with any framework and doesn't implement or extend any interface or class.

Java Bean - class that has to obey 3 contracts so that other frameworks can do certain things with it.
1. Class must have NoArgsConstructor
2. All fields must be private and can be accessible through getters and setters 
3. Class must implements Serializable interface. (objects can be written to streams(files, databases))

## Static Keyword

Either a property or method belongs to class itself rather than the instance.
 
## When to use static ?


If we want same property or method for every object of class and we don't declare it static it will create new stack object every time we create new instance of class but if we use static it will only created one time.
It's use for memory management and attach to a method or property if you're writing a utility class and they're not supposed to change.

Code than needs to shared around without having an instance

If we have method in class that does not require instance for using it then it must be declared as static . e.g Math.pow(), PI ,abs


## Static Block Initializer



```java
public static int count;  

static {  
// whenever the class is initialized it will run no need to create an instance  
System.out.println("start: static initialization");  
count = 0;  
System.out.println("end: static initialization"); // can access only static fields inside this block  
}
```

Order => static block as per the object initialized -> constructor()
## Instance Block Initializer

Invoked once per instance

{} add this block inside class 


## Static import

```java
import static java.lang.Math.max; // now we can use max instead of Math.max
```


# OOPS

## Encapsulation

 - The process of binding an object state and behaviour together into one unit
 - Wrapping data and code acting on that data together
 - We can make class attributes hidden from other classes using encapsulation
 - Prevent classes from become being tightly coupled
 - Easily modify inner workings of a class without affecting the rest of the program or consumers
 - Robust to changes


```java
public class BankAccount {  
private String name;  
private BigDecimal balance;  
private boolean hasOverdraft;  
  
public BankAccount(String name, BigDecimal balance, Boolean hasOverdraft) {  
this.name = name;  
this.balance = balance;  
this.hasOverdraft = hasOverdraft;  
}  
  
public BigDecimal withdraw(BigDecimal amount) {  
if(balance.subtract(amount).compareTo(BigDecimal.ZERO) >=0 ) {  
this.balance = this.balance.subtract(amount);  
return amount;  
}  
return BigDecimal.ZERO;  
}  
}
```


## Inheritance 

Inheritance allows us to create a new class from existing class.


extends keyword
use parent constructor using super() keyword
we can also call parent class method using super keyword

Protected modifiers - can be access by class itself and its subclasses.

## Abstract Keyword on Classes

if we attach abstract keyword on class we cannot create instance of that class.

## Abstract Keyword on Methods

to not make default method for all subclasses  just provide structure all the subclasses should able to define their own implementation for that method.

Abstract Methods
- have no method body
- Class should be abstract to use abstract methods 
- Abstract methods should only exists within abstract classes or interfaces.

```java
abstract public class Animal {  
  
private String name;  
  
public Animal(String name) {  
this.name = name;  
}  
  
public abstract void makeSound();  
}
```

Avoids code duplication and increase reusability

The purpose of an abstract class is to function as a base for subclass.

## Polymorphism 

Many forms

## Interface

can contain 3 things
1. static immutable fields
2. abstract methods 
3. default methods


```java
public interface Vehicle {  
  
// constants  
double PURCHASE_RATE = 0.5;  
  
// abstract methods  
void move(int amount);  
void applyBrakes();  
int getCurrentSpeed();  
  
// default methods  
// method that we don't want to force other classes to implement  
// other class can override if they want to have their own impl  
default double milesToKm(int speed) {  
return getCurrentSpeed()*1.609;  
};  
  
}
```



