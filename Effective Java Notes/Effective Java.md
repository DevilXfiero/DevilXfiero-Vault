
## Chapter 1 - Introduction

## Chapter 2 - Creating and Destroying Objects


Item 1 : Consider static factory method instead of constructors

public constructor - way to prove instance of a class

Advantages
 - unlike constructors static factory method have names.
 - they are not required to create new object each time they're invoked.

```java
public static Boolean valueOf(boolean b) {
   return b ? Boolean.TRUE : Boolean.FALSE;
}
```
it never creates an object

Improve performance for objects that are expensive to create.

- they can return object of any subtype of their return type.

As of Java 8, Interfaces can contain static methods.
e.g BigInteger(int, int, Random) BigInteger.probablePrime

- class of the returned object can vary from call to call as function of the input parameters.

e.g EnusSet class has only static factories.
Clients neither know nor care about the class of the object they get back from the factory; they care only that it is some subclass of EnumSet.

- Class of the returned object need not exist when the class containing the method is written.
e.g service provider frameworks 
  JDBC
Three essential component
1. service interface
2. provider registration API 
3. service access API
4. service provider interface 

Limitations 

- classes without public or protected constructors cannot be subclassed.
Impossible to subclass any of the convenience implementation classes in the Collections framework. Enforce to use composition instead of implementation

- hard for programmers to find.

Some common static factory methods

from - type-conversion method
```java
Date d = Date.from(instant);
```

of - aggregation method
```java
Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
```

valueOf - verbose alternative to from

instance or getInstance - Returns the instance that is described by its parameters(if any)

create or newInstance - Like instance or getInstance, except that method guarantees that each call returns the new instance

getType - Like getInstance, but used if the factory method is in different class. Type is the type of object returned by the factory method,
```java
FilStore fs = Files.getFileStore(path);
```

newType - Like newInstance, but used if the factory method is in different class. Type is the type of object returned by the factory method
```java
BufferedReader br = Files.newBufferedReader(path);
```

type - A concise alternative to getType and newType
```java
List<Complaint> litany = Collections.list(legacyLitany);
```

Item 2: Consider a builder when faced with many constructor parameters

Static factories and constructors share a limitation: they do not scale well to large number of optional parameters.

e.g Nutrition Facts label on package foods.

1. *telescoping constructor* pattern - provide constructor with only the required parameters, another with single optional parameter, a third with two optional parameters.
2. *JavaBeans* pattern - parameterless constructor to create the object and then call setter methods to set each required parameter.
JavaBeans pattern precludes the possibility of making a class immutable and requires added effort on part of the programmer to ensure thread safety.

 3. *Builder* pattern - Instead of making the desired object directly, the client calls a constructor(or static factory) with all of the required parameters and gets a builder object. Then client calls setter-like methods on the builder object to set each optional parameter of interest. 

```java
public class NutritionFacts {  
    private final int servingSize;  
    private final int servings;  
    private final int calories;  
    private final int fat;  
    private final int sodium;  
    private final int carbohydrates;  
  
    public static class Builder {  
        // Required parameters  
        private final int servingSize;  
        private final int servings;  
  
        // Optional parameters  
        private int calories;  
        private int fat;  
        private int sodium;  
        private int carbohydrates;  
  
        public Builder(int servingSize, int servings) {  
            this.servingSize = servingSize;  
            this.servings = servings;  
        }  
  
        public Builder calories(int val) {  
            calories = val;  
            return this;        }  
        public Builder fat(int val) {  
            fat = val; return this;  
        }  
        public Builder sodium(int val) {  
            sodium = val; return this;  
        }  
  
        public Builder carbohydrates(int val) {  
            carbohydrates = val; return this;  
        }  
  
        public NutritionFacts build() {  
            return new NutritionFacts(this);  
        }  
    }  
  
    private NutritionFacts(Builder builder) {  
        servingSize = builder.servingSize;  
        servings = builder.servings;  
        calories = builder.calories;  
        fat = builder.fat;  
        sodium = builder.sodium;  
        carbohydrates = builder.carbohydrates;  
    }  
}


NutritionFacts nutritionFacts = new NutritionFacts.Builder(240, 8).calories(70).sodium(50).carbohydrates(30).build();
```

The Builder pattern is well suited to class hierarchies.

The technique, wherein a subclass method is declared to return a subtype of the return type declared in the superclass, is know as *covariant return typing*.

Item 3: Enforce the singleton property with a private constructor or an enum type


Making a class singleton can make it difficult to test its clients.

```java
// Singleton with public final field
public class Elvis {
  public static final Elvis INSTANCE = new Elvis();
  private Elvis() { ... }
  public void leaveTheBuilding() { ... }
}

// Singleton with static factory 
public class Elvis {
   private static final Elvis INSTANCE = new Elvis();
   private Elvis() { ... }
   public static Elvis getInstance() { return INSTANCE; }
   public void leaveTheBuilding() { ... }
}

// Enum singleton - the preferred approach
public enum Elvis {
  INSTANCE;
  public void leaveTheBuilding() { ... }
}
```

Enum Approach provides the serialization machinery for free, and provides an ironclad guarantee against multiple instantiation. 
a-single-element enum type is often the best way to implement a singleton.
