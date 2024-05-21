## Types of Exceptions
- Checked - handle properly - java compiler checks at compile time
- Unchecked - runtime exception - nullPointerException, arithmeticException, illegalArgumentException, indexOutOfBoundsException, IllegalStateException
- Error - external out of applications.

## Exception Hierarchy

Throwable
Exception  Error
Runtime Exception under exception

## Catching multiple exceptions

```java
public static void show() {  
try {  
var reader = new FileReader("file.txt");  
var value = reader.read();  
new SimpleDateFormat().parse("");  
} catch (IOException | ParseException e) {  
System.out.println("Could not read data");  
}  
}
```

## The finally Block

finally block always got executed.


