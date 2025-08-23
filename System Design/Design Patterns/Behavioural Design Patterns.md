## 1. Strategy Design Pattern

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

##  2. Observer Design Pattern


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

## 3. Null Object Design Pattern 

Avoid check 
if(object != null) 

- A null Object replaces NULL return type
- No need to put if check 
- Null Object reflects do Nothing or Default behaviour


Abstract Object 
method() 
       |
       |
   -----------
   |                  |
   |                  |
Real Object   Null Object
method()         method()

## 4. State Design Pattern 

e.g Vending Machine

| State              | Operation                                      |
| ------------------ | ---------------------------------------------- |
| 1. Idle            | Press Insert Cash Button                       |
| 2. HasMoney        | Insert Coin, Select Product, Refund Button     |
| 3. Selection State | Choose Product, Cancel / Refund, Return Change |
| 4. Dispensing      | Product Dispense                               |

Specific operations are allowed in different states - State Design Pattern 

Design TV 


Product ------> has a ----> << Interface>> State (contain all options)
                              |
                        Concrete States (State1, State2, State3) with only options and implemented that to be performed at that state.
                         Contains Product object also to update the state of the project




 
