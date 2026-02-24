## 1. Decorator Pattern

F1) F1+F2 ) F1 + F2 + F3 )


Use Case
Pizza Shop

Base Pizza 
Toppings 
Extra cheese
Mushroom 
Jalpeno
Extra Veggies

Coffee - Cream, Milk, sugar, mocha
Car - Seat Cover, AC, fog light, Matte Layer

Decorating the base pizza
The new decorator formed is also the object of same type so you can decorate it further


Why you need decorator pattern  ? 
Class Explosion 

Multiple classes formed for each permutations and combinations  of decoration we want to do for our base object. This will result in too many classes formed

abstract 
Base Pizza  <--------is-a, has - a ------- abstract Topping Decorator
   |
   |
   |
   is -a 
   | 
   Margheritta

Topping Decorator both Is-a and has-a relationship because it contains Pizza object and itself is a Pizza object after decoration so that we can add more decorator if we want.

### 2. Composite Pattern

Object inside Object

Prefer composition over Inheritance
Tree like structure 

e.g.
Company team structure
Delivery box - Product or another box - Product or smaller box 
Calculator - Airthmetic Expression 


Files System  - File or Directory - (File or subdirectory)


```
Component (operation()) Interface (FileSystem)
     |
     -------------------------------------
     |                                                             |
Leaf (operation())(File)                 Composite (operation()) ( Directory )(has a FileSystem)      

```



```
c:/Users/Download/test.txt

File, Directory 
File ( fileName)
Directory (directoryName, List<Object> objectList)
```


## Adapter Pattern 

XML to JSON 
```
Client --> <<AdapterInterface>>  ---is-a--> ConcreteAdapter --- has-a ->Adaptee
                request()                                        ExistingInterface (Adpatee)
                                               request()
```
`

## Facade 

When to use and why ? 
When we have to hide the system complexity from the client.


```
Client -> Facade(accelrate(), brake()) --> implementation
Provide functionality and hides logical complexity from client.

```


But we should not enforce client to use Facade always over calling system direct. It's a client choice.

## Bridge Design Pattern 

"Bridge pattern decouples abstraction from its implementation so that the two can vary independently"



