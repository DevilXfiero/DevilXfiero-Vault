What is Java ? 
Object Oriented Programming language
Java is a compiled/interpreted language

Why compiled and interpreted both?

source code -> compiled -> bytecode -> interpreted -> JVM (executes the source code)

bytecode can run on any machine not dependent on OS  (Platform Independent)
Compile time checking for errors 

JVM 
1. class loader ( Scan (classpath)) Initializingm Linking
2. bytecode verifier
3. Each thread has its own **JVM Stack** 
4. Method area 
5. Each thread has its own PC Register to maintain address of executable.
6. JIT Compiler ( Just in time ) 
 

Static vs Dynamic Type checking

Compile Time(Static check)
Run-time (dynamic check)

## Running java from terminal

```terminal
javac Main.java // converts to bytecode Main.class
java Main // to run code by Jvm
```

Reserved keywords - public static etc

## Primitives

int, long, short, char, float, double, boolean


Numeric literals with underscore 

int num = 1_000_007;

## References

### String

```java
String brand = "DevilXfiero";  
System.out.println(brand.toUpperCase());  
System.out.println(brand.substring(0 , 6));  
System.out.println(" ".isEmpty());  
System.out.println(" ".isBlank());  
System.out.println(" a ".trim());
```




## Memory stack
- Stack memory in Java is used for static memory allocation and the execution of a thread
- LIFO - Last In First Out

## Frame
- A stack frame contains all the data for one function call
- The stack frame only exist during the execution time of a function including any references

## Heap
- Space is used to store objects and JRE classes at runtime.
- New objects are always created in heap space.
- References to these objects are stored in stack memory.
stored in RAM only , but sharable resource between every threads

In heap we need to free memory while deleting objects.  **Garbage collection**

public static void main (String[] args) 

What is args ? 
reference to the List string arguments you pass while running this java code

```
javac Test.java // compile to bytecode java.class
java Test 12 34 // 12 34 are the args pass
```

## Java is always Pass by value



But for Reference types like object var reference is stored in stack so it copy the value to new var therefore when we change any of them the value stored at reference got changed.

## Arrays

```java
int[] numbers = new int[3];  
numbers[0] = 1;  
numbers[1] = 2;  
numbers[2] = 7;  
System.out.println(Arrays.toString(numbers));  
System.out.println(numbers.length);  
  
int[] numbers2 = {0, 5, 6, 7};  
System.out.println(numbers2.length);
```

Default value - 0 for primitives , null for Reference types

```java
int[] nums = new int[3];
Arrays.fill(nums, 2);
System.out.println(Arrays.toString(nums));
String[] names = new String[3];
names[0] = "DevilXfiero";
System.out.println(Arrays.toString(names));
```

Fully qualified name for two same package name imports 

e.g
java.util.Date
java.sql.Date

for first we can do by Date date
but for second we have to use fully qualified name  java.sql.Date date

No import required for java.lang because it is default package in java.



## Access Modifiers

Access level
how classes, methods, attributes of classes and constructors can be accessed

Values
default, public, private & protected

public - accessible by everyone
private - only accessible by anything within the scope of defined class.
default - Accessible by anything within the same package

## Static Keyword

Anything which is defined as static belongs to the Class and not the Instance itself.

In static context you're only allowed to use anything which has static keyword to it.

Parameter - In method definitions
Arguments - values that you pass while invoking method

## Type inference with Var

Introduced in Java 10
To automatically detect variable type by its value.

- Can only be used for local variables only.

```java
 var name ="DevilXfiero";
 System.out.println(name);
```


## Final Keyword

Allows you to create constants, prevent Inheritance and method overriding

```java
public static final String NAME = "DevilXFiero";
```

 
## Enums
```java
enum Gender {
    MALE, FEMALE
}

enum TShirtSize {
    S, M, L, XL
}
```


## Typecasting

Convert one datatype to other

```java
// Implicit Type (Widening) Casting
int balance = 100;  
double balanceInDouble = balance;  
// Explicit Type (Narrowing) Casting  
double remainingBalance = 100.5;  
int remainingBalanceInt = (int) remainingBalance;
```

## Wrapper Classes

have many different methods provided.
```java
Integer a = 10;  
Integer b = 30;  
Boolean equal = a.equals(b);  
var str = "20";  
int num = Integer.parseInt(str);  
System.out.println(Integer.min(20, 5));  
System.out.println(Integer.sum(a, b));  
System.out.println(Integer.toString(num));  
System.out.println(Integer.MAX_VALUE);
```

## String

How strings are stored in memory 

Store in String Pool inside heap.

String Pool - Special memory region where Strings are stored by JVM.


```java
String name = "DevilXfiero";  
String name2 = "DevilXfiero";
```

Find in the String pool if same name exists then point to that same reference and if we change 
to new value create new and then point to that.

- String are immutable
value not changes what changes really is the reference.

String Literal vs String Object

```java
String name = "DevilXfiero"; // String Literal
String newName = new String("Harshita"); // String Object - stored in heap not in String Pool
```

```java
String name1 = "DevilXfiero"; // String Literal  
String newName = new String("DevilXfiero");  
String name2 = "DevilXfiero";  
System.out.println(name1 == name2); // true  
System.out.println(name1 == newName); // false  
// To compare by content  
System.out.println(name1.equals(name2)); // true  
System.out.println(name1.equals(newName)); // true
```

- == signs compare by reference
- Always use String.equals() method to compare string content

```java
String number = String.valueOf(1);  
System.out.println(number);  
String format = String.format("Number %s", number);  
System.out.println(format);  
String[] names = {"DevilXfiero", "Abhishek"};  
String join = String.join(",", names);  
System.out.println(join);
```

## LocalDateTime

```java
LocalDateTime now = LocalDateTime.now();  
System.out.println(now);  
System.out.println(now.getMonth());  
System.out.println(now.getDayOfYear());  
System.out.println(now.getDayOfWeek());  
System.out.println(now.getHour());  
System.out.println(now.getMinute());  
System.out.println(now.getSecond());  
System.out.println(now.minusDays(5));  
  
LocalDate localDate = LocalDate.now();  
LocalTime localTime = LocalTime.now();  
System.out.println(localDate);  
System.out.println(localTime);  
  
LocalDateTime someDate = LocalDateTime.of(  
2000,  
Month.DECEMBER,  
1,  
14,  
55  
);  
LocalDate someDate2 = LocalDate.of(  
2000,  
Month.DECEMBER,  
1  
);  
  
System.out.println(someDate);  
System.out.println(localDate);
// Other Date classes  
System.out.println(ZonedDateTime.now());  
System.out.println(Instant.now());
```



## The Problem With double

- Always use BigDecimal for handling money transactions
```java
double number1 = 0.02;  
double number2 = 0.03;  
double result = number2 - number1;  
System.out.println(result); // 0.009999999999999998  
  
BigDecimal num1 = new BigDecimal("0.02");  
BigDecimal num2 = new BigDecimal("0.03");  
BigDecimal res = num2.subtract(num1);  
System.out.println(res); // 0.01  
  
BigDecimal number = BigDecimal.TEN;  
System.out.println(number);  
System.out.println(number.add(BigDecimal.ONE));  
System.out.println(number.max(BigDecimal.ZERO));  
System.out.println(number.compareTo(BigDecimal.ONE)); // 1 if number > , -1 if number < , 0 if equal
```


## Scanner


```java
System.out.println("Hello what is your name?");  
Scanner scanner = new Scanner(System.in);  
String input = scanner.nextLine();  
System.out.println("Hello " + input);  
  
System.out.println("What is your age?");  
int age = scanner.nextInt();  
if(age < 16) {  
System.out.println("You are a child");  
} else {  
System.out.println("You are an adult");  
}
```

## Exception

```java
try {  
int number = Integer.parseInt("1x");  
System.out.println(number);  
} catch (NumberFormatException | ArithmeticException e) {  
System.out.println(e.getMessage());  
e.printStackTrace();  
}
```

When you don't know exception type
### The Exception Class
```java
try {  
int number = Integer.parseInt("1x");  
System.out.println(number);  
} catch (Exception e) {  
System.out.println(e.getMessage());  
e.printStackTrace();  
}
```

The Finally Keyword
```java
try {  
int number = Integer.parseInt("1x");  
System.out.println(number);  
} catch (Exception e) {  
System.out.println(e.getMessage());  
e.printStackTrace();  
} finally {  
System.out.println("Finally always runs"); // use for cleanup purposes  
}
```


![[Screenshot 2024-04-15 at 11.05.15 PM.png]]

### Unchecked Exception 

Runtime Exception

Exceptions that occur during the Normal Execution of the method.

### Checked Exceptions

e.g IOException
Exceptions must dealt before compile time in constructor or method.

try/catch - want that method to deal with exception
throws  - to pass responsibility to the method that uses the given method

If a client can reasonably be expected to recover from an exception, make it checked exception.
If client cannot do anything to recover from the exception, make it an unchecked exception.


## File

createFile
```java
private static File createFile(String path) {  
try {  
File file = new File(path);  
if (!file.exists()) {  
file.createNewFile();  
}  
return file;  
  
} catch (IOException e) {  
System.out.println(e.getMessage());  
throw new IllegalStateException(e);  
}  
}
```

writeToFile
```java
private static void writeToFile(File file, boolean append, String value) {  
try {  
FileWriter fileWriter = new FileWriter(file, append); // pass second parameter to append into the file by default it will override  
PrintWriter writer = new PrintWriter(fileWriter);  
  
writer.println(value);  
  
writer.flush();// flush contents into the file  
writer.close();  
} catch (IOException e) {  
System.out.println(e.getMessage());  
throw new IllegalStateException(e);  
}  
}  
```

readFile
```java

File file = createFile("src/foo.txt");  
writeToFile(file, true, "Hello Programmer");  
try {  
Scanner scanner = new Scanner(file);  
while(scanner.hasNext()) {  
System.out.println(scanner.nextLine());  
}  
} catch (FileNotFoundException e) {  
System.out.println(e.getMessage());  
throw new RuntimeException(e);  
}  
}  
```

try with resources
```java
// no need to do flush and close every time
try (FileWriter fileWriter = new FileWriter(file, append);  
PrintWriter writer = new PrintWriter(fileWriter)) {  
  
writer.println(value);  
  
} catch (IOException e) {  
System.out.println(e.getMessage());  
throw new IllegalStateException(e);  
}
```


### TypeReference

```java
userList = objectMapper.readValue(users, new TypeReference<List<User>>() {}); // to resolve generic type(User) in List before deserializing it from json to User object
```

## Java Functions

Functions are first class citizen that means functions can be passed as parameters and arguments and they can be used.

Functional Interface

A ****functional interface in Java**** is an interface that contains only one abstract method. Functional interfaces can have multiple ****default**** or ****static**** methods, but ****only one abstract method****. [****Runnable****](https://www.geeksforgeeks.org/runnable-interface-in-java/), [****ActionListener****](https://www.geeksforgeeks.org/java-actionlistener-in-awt/)****,**** and [****Comparator****](https://www.geeksforgeeks.org/comparator-interface-java/) are common examples of ****Java**** ****functional interfaces****.

****Functional Interface is additionally recognized as**** ****Single Abstract Method Interfaces****. In short, they are also known as ****SAM interfaces****.

****Java SE 8 included four main kinds of functional interfaces**** which can be applied in multiple situations as mentioned below:

1. ****Consumer****
2. ****Predicate****
3. ****Function**** 
4. ****Supplier****


# EventLoop vs Thread Pool

## Event Loop

## Overview:

- _Event Loop_: An event loop is a programming construct that waits for and dispatches events or messages in a program. It is central to the concurrency model of event-driven frameworks like Vert.x.
- _Single-Threaded_: The event loop typically runs on a single thread. This thread continuously checks for new events and processes them one at a time.
- _Non-Blocking I/O_: Operations that would block the thread (like I/O) are handled asynchronously. Callbacks, promises, or reactive streams are used to handle the results of these operations.

## How It Works:

1. _Event Queue_: Events (e.g., incoming network requests, I/O completions) are placed in an event queue.
2. _Event Loop_: The event loop continuously retrieves and processes events from the queue.
3. _Callbacks_: Each event has an associated callback function that gets executed. If an event involves a long-running or blocking operation, the operation is initiated, and the callback is registered to handle the completion of the operation asynchronously.
4. _Continuation_: Once the operation completes, the callback is invoked, allowing the application to continue processing.

# Multithread Architecture

## Overview:

- _Multi-Threading_: Multiple threads are used to handle concurrent tasks. Each thread can execute independently, allowing multiple operations to be processed in parallel.
- _Blocking I/O_: Traditional multi-threaded applications often use blocking I/O, where each thread waits for I/O operations to complete.

## How It Works:

1. _Thread Pool:_ A pool of threads is created at application startup. Each thread can handle a separate task or request.
2. _Task Queue_: Incoming tasks (e.g., web requests) are placed in a queue and dispatched to available threads in the pool.
3. _Synchronization_: Threads may need to access shared resources, requiring synchronization mechanisms (e.g., locks, semaphores) to ensure data consistency.
4. _Blocking Operations_: Threads can perform blocking operations since each thread operates independently. If one thread blocks, others can continue processing.

## Proxy Pattern

**Proxy** is one of the structural patterns in Gang of Four (GoF), that provides a substitute or placeholder for another object to control access. The proxy pattern allows you to perform some logic either before or after invoking the original object.

On adding @_Cacheable_ annotation, spring creates a new caching proxy class. This class will be in charge of adding Caching behavior and will be used for dependency injection.

## 1. What is a Dynamic Proxy?

A dynamic proxy in Java is an object that implements one or more interfaces and delegates method calls to an underlying object or performs additional operations. Unlike static proxies, which are created at compile-time, dynamic proxies are generated at runtime.

In Spring, dynamic proxies are primarily used in two ways:  
  
**JDK Dynamic Proxies** : These proxies are created using the java.lang.reflect.Proxy class and can only proxy interfaces.  
  
**CGLIB Proxies** : These proxies are created using the CGLIB library and can proxy classes without requiring an interface.
# [[Java Classes And Objects]]

# [[ Java Intermediate]]

# [[Java Collections]]

