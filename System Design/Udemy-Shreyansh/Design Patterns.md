
## Strategy Design Pattern

Inheritance Is-a 
Composition has-a

Whenever there is a situation when child using capability that is not common in parents but common between childs it results in duplication of and code reusability issue

eg. 
Vehicle 
method - drive(), display()

OffRoadVehicle extends Vehicle
display(), drive() some other logic

SportyVehicle
display(), drive() some other logic than parent but same as OffRoadVehicle

When these classes(child) grows in other it types it results more and more duplication.

Solution 

Create Interface 
DriveStrategy with method drive() 

Create classes implements DriveStrategy 
Two type Normal Drive, Special Drive 

Now add object of DriveStrategy inside Vehicle 
Vehicle HAS-A drive strategy now we can assign required drive method base on strategy for different vehicles.

## Observer Design Pattern


Observable - state change (update all the observer)
Observer


ObservableInterface
```java
List<ObservableInterface> obsInterfaceList
```
add(ObserverInterface) - register
remove(ObserverInterface)
notify()

ObserverInterface
update()


Real life eg - 
Notify me for the products listed in ecommerce website

## Decorator Pattern

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




