
For every object we should define its list.

Poor Solution
Using objects as type but now it can store any value as object is parent of every reference types.
But now we have to cast to primitive as it store only objects and we can also get ClassCastException for casting wrong object to primitive type. 

- We cannot use primitives e.g int, double, char with Generics.
## ClassCastException

```java
List numbers = new ArrayList();  
numbers.add(1);  
numbers.add("2");  
for(Object number: numbers) {  
System.out.println((String) number);  // casting integer to string
}


  
// Comparable number = 10;  
// number.compareTo("10");  
  
Comparable<Integer> number = 10;  
System.out.println(number.compareTo(10));
```

GenericLIst
```java 
public class GenericList<T>{  
private T[] items = (T[]) new Object[10];  
private int count;  
  
public void add(T item) {  
items[count++] = item;  
}  
  
public T get(int index) {  
return items[index];  
}   
}
```


```java
GenericList<Integer> numbers = new GenericList<Integer>();  
numbers.add(1); // Boxing - Java compiler create instance of Integer class to store primitve types
int number = numbers.get(0); // Unboxing
```


## Constraints
```java
public class GenericList<T extends Number>
```

## Type Parameter and Type Argument


Generic Type Naming Convention

E  E - element
K- key, V- value
N - Number
T - Type


## Generic Classes

```java
public class Box<T> {  
private T t;  
  
public void set(T t) {  
this.t = t;  
}  
  
public T get() {  
return this.t;  
}  
}
```

## Generic Methods

```java
static <T> void print(T[] array) {  
for(T e : array) {  
System.out.println(  
e.getClass().getName() + "-" + e  
);  
}  
} // if function returns something than it should be of type T
```

## Bounded Type Parameters 

To create more generic to be more restrict types

T extends Comparable T
use can use any class 

### Multiple Bounds

```java
interface A {}  
interface B {}  
  
static <T extends Comparable<T> & A & B> void method() {  
  // class should be pass before interface for multiple bounds
  // you can extends only one class and multiple interfaces

}
```

## Wildcards

? Wildcards

Unbounded Wildcards
```java
public static void main(String[] args) {  
List<Object> list1 = Arrays.asList(1,2);  
List<Integer> list2 = Arrays.asList(1,2);  
  
print(list1);  
print(list2);  
}  
  
static void print(List<?> list) {  
list.forEach(System.out::println);  
}
```

UpperBounded Wildcards
```java
static void print(List<? extends Number> list) {  
list.forEach(System.out::println);  
}
```

LowerBounded Wildcards
```java
static void print(List<? super Number> list) {  
list.forEach(System.out::println);  
// must be of type number or its superclass  
}
```

