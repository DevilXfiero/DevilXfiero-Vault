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


