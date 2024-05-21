
## Dependency Injection

When we want to use services like CarDAO, EmailService, MOTService and we create new instance of these service in CarService constructor it become tightly couple with these services
whenever one of the service will be down car service will also go down.

Injecting dependency to the class in use rather than defining inside and making it tightly coupled.

// dependencies
CarDAO carDAO = new CardDAO();

// inject
CarService carService = new CarService(carDAO);

```java
public class CarService {  
  
public CarDAO carDAO;  
  
public CarService(CarDAO carDAO) {  
this.carDAO = carDAO;  
}  
}
```

if we have MOTService and CarService both wants EmailService so if we have huge codebase it will be difficult to initialize and set same instance to all the required services in correct manner so this will cause creation of multiple duplicate instances into the heap.


Solution - Singleton Pattern

Instantiate your class just once.



## Null pointer exception

when to try to access methods or properties of a object which is point to null or having no reference.

The wrong way of dealing with Null

1. if(brand == null) 
2. try catch 

Better way
1. Optional Class
```java
String brand = "DevilXfiero";  
Optional<String> brandOptional = Optional.ofNullable(brand);  
if(brandOptional.isEmpty()) {  
System.out.println("Brand is empty");  
} else {  
System.out.println(brandOptional.get());  
}  
  
brandOptional.ifPresentOrElse(b -> {  
System.out.println(b.toUpperCase());  
}, () -> {  
System.out.println("Brand is empty");  
});  
  
var result = brandOptional.orElse("Programmer"); // if present than actual otherwise default which is provided  
System.out.println(result);
```

